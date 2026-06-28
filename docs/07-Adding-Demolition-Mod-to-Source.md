# Adding Demolition Mod to Source

This document describes the source changes needed to support the example Demolition mod in *No One Lives Forever 2*.

For this example, Demolition replaces Team Deathmatch. The other multiplayer modes are also hidden from the menus.

## Overview

At a high level, the source changes do the following:

- add new transmission strings for Demolition gameplay
- force Team Deathmatch server options to behave like Demolition
- simplify the Team Deathmatch host options UI
- remove unused Team Deathmatch SCMD options
- rename Team Deathmatch to Demolition in the UI
- remove other game modes from the front-end menus
- restrict playable maps to levels using the `DE_` prefix
- enable revive behavior and asymmetric respawn timing
- reuse Doomsday radio messages for Demolition

## 1. Add Demolition Transmission Strings

The Demolition mod uses transmissions to tell the player what to do.

Open:

- `game\clientres\to2\lang\en\clientres.rc`

In the AppStudio resource editor in DevStudio, find the transmission strings. Add the following entries after `IDS_TRANSMISSIONS_7095`.

| Label | Value | String |
| --- | --- | --- |
| `IDS_TRANSMISSIONS_7096` | `7096` | `Find the bomb and plant it on the designated target!` |
| `IDS_TRANSMISSIONS_7097` | `7097` | `Prevent the enemy team from planting the bomb!` |
| `IDS_TRANSMISSIONS_7098` | `7098` | `Your team has planted the bomb! Don't let the enemy defuse it!` |
| `IDS_TRANSMISSIONS_7099` | `7099` | `The enemy has planted a bomb! Find it and defuse it before it goes off!` |
| `IDS_TRANSMISSIONS_7100` | `7100` | `The enemy has defused the bomb! We'll need to try again.` |
| `IDS_TRANSMISSIONS_7101` | `7101` | `The bomb was successfully defused. Stop them from planting another!` |
| `IDS_TRANSMISSIONS_7102` | `7102` | `The bomb has detonated. Blue Team wins the round!` |
| `IDS_TRANSMISSIONS_7103` | `7103` | `The bomb has detonated. Red Team wins the round!` |
| `IDS_TRANSMISSIONS_7104` | `7104` | `Time limit reached. The Red team has successfully defended their base!` |
| `IDS_TRANSMISSIONS_7105` | `7105` | `Time limit reached. The Blue team has successfully defended their base!` |

## 2. Force Team Deathmatch Server Rules to Behave Like Demolition

Open:

- `game\objectdll\objectshared\TeamDeathMatchMissionMgr.cpp`

### `CTeamDeathMatchMissionMgr::StartGame`

This removes the score limit, removes the time limit, and forces rounds to be even and at least `2`.

Change this:

```cpp
sms.m_nScoreLimit = sgo.GetTeamDeathmatch().m_nScoreLimit;
sms.m_nTimeLimit = sgo.GetTeamDeathmatch().m_nTimeLimit;
sms.m_nRounds = sgo.GetTeamDeathmatch().m_nRounds;
```

to this:

```cpp
sms.m_nScoreLimit = 0;
sms.m_nTimeLimit = 0;
sms.m_nRounds = (sgo.GetTeamDeathmatch().m_nRounds & 1) ?
    sgo.GetTeamDeathmatch().m_nRounds + 1 : sgo.GetTeamDeathmatch().m_nRounds;
sms.m_nRounds = Max(sms.m_nRounds, (uint8)2);
```

### `CTeamDeathMatchMissionMgr::HandleMultiplayerOptions()`

Change this:

```cpp
sms.m_nScoreLimit = sgo.GetTeamDeathmatch().m_nScoreLimit;
sms.m_nTimeLimit = sgo.GetTeamDeathmatch().m_nTimeLimit;
```

to this:

```cpp
sms.m_nScoreLimit = 0;
sms.m_nTimeLimit = 0;
```

## 3. Simplify the Team Deathmatch Host Options Screen

Open:

- `game\clientshelldll\to2\ScreenHostTDMOptions.cpp`

### `CScreenHostTDMOptions::CScreenHostTDMOptions()`

Change this:

```cpp
m_nScoreLimit = 25;
m_nTimeLimit = 10;
m_nRounds = 1;
```

to this:

```cpp
m_nScoreLimit = 0;
m_nTimeLimit = 0;
m_nRounds = 2;
```

### `CScreenHostTDMOptions::Build`

Remove the score and time sliders and leave only the rounds slider.

Change this:

```cpp
pSlider = AddSlider(IDS_FRAG_LIMIT, IDS_FRAG_LIMIT_HELP, kColumn, kSlider, -1, &m_nScoreLimit);
pSlider->SetSliderRange(0, kMaxScoreLimit);
pSlider->SetSliderIncrement(10);
pSlider->SetNumericDisplay(LTTRUE);

pSlider = AddSlider(IDS_TIME_LIMIT, IDS_TIME_LIMIT_HELP, kColumn, kSlider, -1, &m_nTimeLimit);
pSlider->SetSliderRange(0, kMaxTimeLimit);
pSlider->SetSliderIncrement(5);
pSlider->SetNumericDisplay(LTTRUE);

pSlider = AddSlider(IDS_ROUNDS, IDS_ROUNDS_HELP, kColumn, kSlider, -1, &m_nRounds);
pSlider->SetSliderRange(1, kMaxRounds);
pSlider->SetSliderIncrement(1);
pSlider->SetNumericDisplay(LTTRUE);
```

to this:

```cpp
pSlider = AddSlider(IDS_ROUNDS, IDS_ROUNDS_HELP, kColumn, kSlider, -1, &m_nRounds);
pSlider->SetSliderRange(2, kMaxRounds);
pSlider->SetSliderIncrement(2);
pSlider->SetNumericDisplay(LTTRUE);
```

## 4. Remove Score and Time Limit from SCMD

### Server side

Open:

- `Game\ObjectDLL\ObjectShared\ScmdServer.cpp`

#### `ScmdServer_Impl::HandleListGameOptions()`

Change this:

```cpp
case eGameTypeTeamDeathmatch:
{
    cMsg.Writeuint8(sms.m_nRunSpeed);
    cMsg.Writeuint8(sms.m_nScoreLimit);
    cMsg.Writeuint8(sms.m_nTimeLimit);
    cMsg.Writeuint8(sms.m_nRounds);
    cMsg.Writebool(sms.m_bFriendlyFire);
}
break;
```

to this:

```cpp
case eGameTypeTeamDeathmatch:
{
    cMsg.Writeuint8(sms.m_nRunSpeed);
    cMsg.Writeuint8(sms.m_nRounds);
    cMsg.Writebool(sms.m_bFriendlyFire);
}
break;
```

#### `ScmdServer_Impl::HandleSetGameOption()`

Change this:

```cpp
case eGameTypeTeamDeathmatch:
{
    switch (nGameOption)
    {
        // Runspeed.
        case 0:
        {
            SetGameOption(sms.m_nRunSpeed, atoi(szVal), 100, 150);
        }
        break;

        // Score limit.
        case 1:
        {
            SetGameOption(sms.m_nScoreLimit, atoi(szVal), 0, 255);
        }
        break;

        // Time limit.
        case 2:
        {
            SetGameOption(sms.m_nTimeLimit, atoi(szVal), 0, 255);
        }
        break;

        // Rounds.
        case 3:
        {
            SetGameOption(sms.m_nRounds, atoi(szVal), 1, 255);
        }
        break;

        // Friendly fire.
        case 4:
        {
            SetGameOption(sms.m_bFriendlyFire, (bool)(!!atoi(szVal)), false, true);
        }
        break;

        default:
        {
            bOk = false;
        }
        break;
    }
}
break;
```

to this:

```cpp
case eGameTypeTeamDeathmatch:
{
    switch (nGameOption)
    {
        // Runspeed.
        case 0:
        {
            SetGameOption(sms.m_nRunSpeed, atoi(szVal), 100, 150);
        }
        break;

        // Rounds.
        case 1:
        {
            SetGameOption(sms.m_nRounds, atoi(szVal), 1, 255);
        }
        break;

        // Friendly fire.
        case 2:
        {
            SetGameOption(sms.m_bFriendlyFire, (bool)(!!atoi(szVal)), false, true);
        }
        break;

        default:
        {
            bOk = false;
        }
        break;
    }
}
break;
```

### Client side

Open:

- `Game\Shared\ScmdConsole.cpp`

#### `ScmdConsoleCommandHandler_ListGameOptions::Receive`

Change this:

```cpp
case eGameTypeTeamDeathmatch:
{
    ScmdConsole::Instance().GetScmdConsoleDriver().WriteStringResId(IDS_TEAMDEATHMATCH);
    uint32 nIndex = 0;
    WriteOutGameOption(nIndex++, "%d", IDS_RUN_SPEED, msg.Readuint8());
    WriteOutGameOption(nIndex++, "%d", IDS_FRAG_LIMIT, msg.Readuint8());
    WriteOutGameOption(nIndex++, "%d", IDS_TIME_LIMIT, msg.Readuint8());
    WriteOutGameOption(nIndex++, "%d", IDS_ROUNDS, msg.Readuint8());
    WriteOutGameOption(nIndex++, "%d", IDS_FRIENDLY_FIRE, msg.Readbool());
}
break;
```

to this:

```cpp
case eGameTypeTeamDeathmatch:
{
    ScmdConsole::Instance().GetScmdConsoleDriver().WriteStringResId(IDS_TEAMDEATHMATCH);
    uint32 nIndex = 0;
    WriteOutGameOption(nIndex++, "%d", IDS_RUN_SPEED, msg.Readuint8());
    WriteOutGameOption(nIndex++, "%d", IDS_ROUNDS, msg.Readuint8());
    WriteOutGameOption(nIndex++, "%d", IDS_FRIENDLY_FIRE, msg.Readbool());
}
break;
```

## 5. Rename Team Deathmatch to Demolition

### Menu text

Open:

- `Shared\Lang\EN\ResShared.rc`

Change `IDS_TEAMDEATHMATCH` from:

- `Team Deathmatch`

to:

- `Demolition`

### GameSpy Arcade text

Open:

- `Game\shared\netdefs.cpp`

Change this:

```cpp
static const char* g_kaGameTypeString[] =
{
    "Single",
    "Cooperative",
    "Deathmatch",
    "TeamDeathmatch",
    "DoomsDay"
};
```

to this:

```cpp
static const char* g_kaGameTypeString[] =
{
    "Single",
    "Cooperative",
    "Deathmatch",
    "Demolition",
    "DoomsDay"
};
```

### Default server name

Open:

- `game\clientres\shared\lang\en\clientresshared.rc`

Change `IDS_HOST_NAME_TDM_DEFAULT` from:

- `NOLF 2 Team Deathmatch`

to:

- `NOLF 2 Demolition`

## 6. Remove Other Game Modes from the Front-End

Open:

- `Game\ClientShellDLL\TO2\ScreenMain.cpp`

### `CScreenMain::Build`

Change this:

```cpp
CLTGUITextCtrl* pCtrl = CreateTextItem(IDS_COOPERATIVE, CMD_COOP, 0);
m_pGameType->AddControl(pCtrl);

pCtrl = CreateTextItem(IDS_DEATHMATCH, CMD_DM, 0);
m_pGameType->AddControl(pCtrl);

pCtrl = CreateTextItem(IDS_TEAMDEATHMATCH, CMD_TEAM_DM, 0);
m_pGameType->AddControl(pCtrl);

pCtrl = CreateTextItem(IDS_DOOMSDAY, CMD_DOOM, 0);
m_pGameType->AddControl(pCtrl);
```

to this:

```cpp
CLTGUITextCtrl* pCtrl = CreateTextItem(IDS_TEAMDEATHMATCH, CMD_TEAM_DM, 0);
m_pGameType->AddControl(pCtrl);
```

## 7. Restrict Playable Maps to `DE_` Levels

Demolition levels should use the prefix `DE_`.

### `CScreenHostLevels::MakeDefaultMissionList()`

Open:

- `game\clientshelldll\to2\screenhostlevels.cpp`

Change this:

```cpp
switch (g_pGameClientShell->GetGameType())
{
    case eGameTypeDeathmatch:
    case eGameTypeTeamDeathmatch:
        if (strnicmp(szWorldTitle, "DM_", 3) == 0)
        {
            AddMissionToList(nMission);
        }
        break;

    case eGameTypeDoomsDay:
        if (strnicmp(szWorldTitle, "DD_", 3) == 0)
        {
            AddMissionToList(nMission);
        }
        break;

    default:
        AddMissionToList(nMission);
        break;
}
```

to this:

```cpp
switch (g_pGameClientShell->GetGameType())
{
    case eGameTypeDeathmatch:
        if (strnicmp(szWorldTitle, "DM_", 3) == 0)
        {
            AddMissionToList(nMission);
        }
        break;

    case eGameTypeTeamDeathmatch:
        if (strnicmp(szWorldTitle, "DE_", 3) == 0)
        {
            AddMissionToList(nMission);
        }
        break;

    case eGameTypeDoomsDay:
        if (strnicmp(szWorldTitle, "DD_", 3) == 0)
        {
            AddMissionToList(nMission);
        }
        break;

    default:
        AddMissionToList(nMission);
        break;
}
```

### `CScreenHostMission::NewCampaign()`

Open:

- `game\clientshelldll\to2\screenhostmission.cpp`

Make the same `DM_` to `DE_` Team Deathmatch split shown above.

### `CScreenHost::CreateDefaultCampaign()`

Open:

- `game\clientshelldll\to2\screenhost.cpp`

Make the same `DM_` to `DE_` Team Deathmatch split shown above.

### `CScreenMulti::CreateDMMissionFile()`

Open:

- `game\clientshelldll\to2\screenmulti.cpp`

Change this:

```cpp
if (ptr->m_Type == TYPE_FILE)
{
    if (strnicmp(ptr->m_pBaseFilename, "DM_", 3) == 0 || strnicmp(ptr->m_pBaseFilename, "DD_", 3) == 0)
    {
```

to this:

```cpp
if (ptr->m_Type == TYPE_FILE)
{
    if (strnicmp(ptr->m_pBaseFilename, "DE_", 3) == 0)
    {
```

## 8. Enable Revives and Add Asymmetric Respawn Timing

Demolition should behave like Doomsday in one important way: players should be able to revive teammates.

The respawn delay is more complicated. For gameplay reasons, only the defending team should get the longer respawn delay.

### Enable revive support

Open:

- `game\shared\clientservershared.cpp`

In `IsRevivePlayerGameType()`, change this:

```cpp
bool IsRevivePlayerGameType()
{
    switch (GetGameType())
    {
        case eGameTypeCooperative:
        case eGameTypeDoomsDay:
            return true;
        break;

        default:
            return false;
        break;
    }
}
```

to this:

```cpp
bool IsRevivePlayerGameType()
{
    switch (GetGameType())
    {
        case eGameTypeCooperative:
        case eGameTypeDoomsDay:
        case eGameTypeTeamDeathmatch:
            return true;
        break;

        default:
            return false;
        break;
    }
}
```

### Track which team is attacking

Open:

- `Game\Shared\TeamMgr.h`
- `Game\Shared\TeamMgr.cpp`

Add a `m_bAttackingTeam` flag to `CTeam`, along with these accessors:

```cpp
void SetAttacking(bool bValue) { m_bAttackingTeam = bValue; }
bool GetAttacking() const { return m_bAttackingTeam; }
```

Initialize `m_bAttackingTeam` to `false` in:

- `CTeam::CTeam()`
- `CTeam::Init(uint8 nID, const char* szName, uint32 nModel)`
- `CTeam::Init(uint8 nID, ILTMessage_Read* pMsg)`

Also update `CTeam::WriteData` and `CTeam::ReadData` so the attacking-team flag is serialized.

Then replace `CTeamMgr::UpdateClient` with an overload pair:

```cpp
void CTeamMgr::UpdateClient(HCLIENT hClient)
{
    UpdateClient(hClient, false);
}

void CTeamMgr::UpdateClient(HCLIENT hClient, bool bScoreOnly)
{
    TeamArray::iterator iter = m_teams.begin();
    while (iter != m_teams.end())
    {
        (*iter)->UpdateClient(bScoreOnly, hClient);
        iter++;
    }
}
```

Add these helpers under the `UpdateClient` functions:

```cpp
void CTeamMgr::SetAttackingTeam(uint8 nTeamId, bool bValue)
{
    CTeam* pTeam = GetTeam(nTeamId);
    if (!pTeam)
        return;

    TeamArray::iterator iter = m_teams.begin();
    for (; iter != m_teams.end(); iter++)
    {
        CTeam* pTeam = *iter;
        pTeam->SetAttacking((pTeam->GetID() == nTeamId));
    }

    UpdateClient(NULL, false);
}

bool CTeamMgr::GetAttackingTeam(uint8 nTeamId)
{
    CTeam* pTeam = GetTeam(nTeamId);
    if (!pTeam)
        return false;

    return pTeam->GetAttacking();
}
```

### Add a `WorldProperties` command to switch the attacking team

Open:

- `Game\ObjectDLL\ObjectShared\WorldProperties.cpp`

In the `CMDMGR_BEGIN_REGISTER_CLASS` block, add:

```cpp
CMDMGR_ADD_MSG(ATTACKINGTEAM, 2, NULL, "ATTACKINGTEAM <0 or 1>")
```

In `WorldProperties::OnTrigger`, add a token:

```cpp
static CParsedMsg::CToken s_cTok_AttackingTeam("AttackingTeam");
```

Then add handling for that trigger so it calls:

```cpp
CTeamMgr::Instance().SetAttackingTeam(nTeamId, true);
```

The intent is:

- accept `AttackingTeam <teamid>`
- validate the team ID
- update `CTeamMgr`
- notify clients

### Use the attacking-team flag when choosing respawn delay

Open:

- `game\clientshelldll\clientshellshared\playermgr.cpp`

In `CPlayerMgr::HandleMsgPlayerStateChange`, split `eGameTypeTeamDeathmatch` away from normal Deathmatch and use:

- the normal respawn delay for the attacking team
- the Doomsday-style delay for defenders when appropriate

The important lookup chain is:

1. get `CClientInfoMgr`
2. get the local client
3. get the local client’s team
4. check `CTeam::GetAttacking()`

If the local player is on the attacking team, use:

```cpp
g_vtRespawnWaitTime.GetFloat()
```

Otherwise use the Doomsday-style team-based delay:

```cpp
g_vtDoomsdayRespawnWaitTime.GetFloat()
```

## 9. Use Doomsday Radio Messages

Open:

- `source\Game\ClientShellDLL\TO2\HUDRadio.cpp`

### `CHUDRadio::Show()`

Change this:

```cpp
switch (g_pGameClientShell->GetGameType())
{
    case eGameTypeTeamDeathmatch:
        m_pText[i]->GetColumn(1)->SetString(LoadTempString(g_TDMRadioArray[i]));
        break;

    case eGameTypeDoomsDay:
        m_pText[i]->GetColumn(1)->SetString(LoadTempString(g_DDRadioArray[i]));
        break;

    default:
        m_pText[i]->GetColumn(1)->SetString(LoadTempString(g_CoopRadioArray[i]));
        break;
}
```

to this:

```cpp
switch (g_pGameClientShell->GetGameType())
{
    case eGameTypeTeamDeathmatch:
    case eGameTypeDoomsDay:
        m_pText[i]->GetColumn(1)->SetString(LoadTempString(g_DDRadioArray[i]));
        break;

    default:
        m_pText[i]->GetColumn(1)->SetString(LoadTempString(g_CoopRadioArray[i]));
        break;
}
```

### `CHUDRadio::Choose()`

Change this:

```cpp
switch (g_pGameClientShell->GetGameType())
{
    case eGameTypeTeamDeathmatch:
        g_pClientMultiplayerMgr->DoTaunt(nLocalID, g_TDMRadioArray[nChoice]);
        break;

    case eGameTypeDoomsDay:
        g_pClientMultiplayerMgr->DoTaunt(nLocalID, g_DDRadioArray[nChoice]);
        break;

    default:
        g_pClientMultiplayerMgr->DoTaunt(nLocalID, g_CoopRadioArray[nChoice]);
        break;
}
```

to this:

```cpp
switch (g_pGameClientShell->GetGameType())
{
    case eGameTypeTeamDeathmatch:
    case eGameTypeDoomsDay:
        g_pClientMultiplayerMgr->DoTaunt(nLocalID, g_DDRadioArray[nChoice]);
        break;

    default:
        g_pClientMultiplayerMgr->DoTaunt(nLocalID, g_CoopRadioArray[nChoice]);
        break;
}
```

## 10. Build and Package the Mod

Once the edits are complete, rebuild the files needed for distribution.

You only need to build:

- `clientres`
- `clientshelldll`
- `object`
- any dependencies they require

This produces:

- `cres.dll`
- `cshell.dll`
- `object.lto`

Build the `Final` targets for distribution.

For build instructions, see:

- [Building the No One Lives Forever 2 Game](11-Building-the-No-One-Lives-Forever-2-Game.md)

For packaging instructions, see:

- [Content Packs and Modifications](05-Content-Packs-and-Modifications.md)
