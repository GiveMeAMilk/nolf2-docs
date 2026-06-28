# Creating the Demolition mod

NO ONE LIVES FOREVER 2

Creating fun new mods for Nolf 2 can be a lot easier than you might think. This tutorial will take you step by step through the process of creating a mod that will replace one of the existing team modes with something completely different. We’ll call this new mode “Demolition”, as the object of the game is to blow up an object in the enemy base, or defend your base from being blown up.

The first part of this tutorial will cover the level design aspects of the mod. In order to complete this project, you’ll need have basic level editing and/or design skills in DEdit. If you are new to DEdit, you should to complete the **DEdit tutorial** before you attempt to modify or create levels for Demolition.

The second part of this tutorial deals with changes to the NOLF2 code that should be made in order for Demolition mode to work as intended. In order to complete this portion of the projects, you should have a working knowledge of C++, and Developer Studio v6.0 or higher installed on your computer.

For your convenience, the completed mod, before and after versions of a sample demolition level, and all required prefabs have been included with this release. If you run into any problems when building your own versions of these files, you can use these files for reference.

Demolition mode is a team-based game where the attacking team attempts to plant a bomb on one of five pre-specified targets, and then prevent the defenders from defusing it until it goes off. The defending team must try to prevent the attackers from planting the bomb, and in the case of failure, defuse the bomb before it goes off.

When the level begins, the attacking team is informed of the location of the time bomb, and of the intended target via icons on the radar screen. The defending team does not know where the bomb is to be planted at first, but can see all five possible bomb locations in the level itself. If the attacking team manages to plant a bomb on the correct target, its location becomes visible to the defending team, who must then defuse it before it goes off. If they are successful, the attacking team must try again. This continues until the bomb goes off, or 10 minutes passes without a detonation. If the bomb goes off, the attackers win the round. If the time limit runs out, the defending team wins the round.

The attacking/defending team for each round is dependent on the round itself. On odd numbered rounds, the blue team acts as the attackers, and on even numbered rounds, the red team attacks. The number of possible rounds in each level is limited to multiples of 2 to ensure that both teams get to play as both attacker and defender at least once per level.

Every demolition level must contain certain objects and sets of objects as follows:

*Bomb Targets* : These are visible indicators that are placed around the defender’s base, preferably in intuitive places such as fuel tanks, ammunition stores, etc. A standard Demolition level will have 5 possible locations for the attacking team to place the bomb. A startup command will activate one of these targets randomly at the beginning of each round. An “X” icon on the radar screen will indicate where the bomb is to be placed. Only the attacking team will see this icon until the bomb is planted for the first time, at which point the icon will become visible to all players.

*Display Timers* : A large display timer will appear at the top center of the screen at the beginning of each round. This indicates how much time the attackers have to successfully plant the bomb. Once a bomb is planted, this timer will pause, and a red or blue bomb timer will appear in the upper right hand corner of the screen. The color of this timer reflects the color of the team that must now diffuse the bomb before it goes off. When a colored timer reaches 0, the bomb will go off, and the attacking team will win the round. If the bomb is diffused, the bomb timer will disappear and the main timer will resume its countdown. If the main timer reaches 0, the defending team will win the round.

Unlike Doomsday or Team Deathmatch, the start points for each team in Demolition are not always the same. Instead, the start points for each team will be swapped at the start of each round. Odd-numbered rounds will start the blue team at the attacking start points, and even-numbered rounds will start the red team in these positions. The game start points are also responsible for sending a message to each player that’s joining the game to inform them of their team’s objective for the current round.

*Startup Commands :* Each Demolition level must 2 sets of startup commands that set up the level for the current round. One set of commands will be set at the start of each odd-numbered round, and the other will be sent at the start of each even-numbered round.

*Time bomb Pickups* : A standard demolition level will have 5 places where the time bomb pickups can spawn. The actual location is determined randomly at the start of each round. An “X” icon on the radar screen will indicate where the time bomb is located. Only the attacking team will see this icon. When a player picks up the time bomb, another will spawn in 15 seconds. More than one player can have a time bomb, and defenders as well as attackers can pick them up.

Most of the objects described in the previous section are actually groups of objects, triggers, and messages. Some of these can be grouped together to form prefabs. In the following sections, you will learn how to create each of these components from the ground up, and then package them as prefabs for easy placement in levels.

First, you’ll need to create a folder in which to store demolition prefabs so that a level designer can easily find them. From your main Nolf 2 installation folder, open the game/prefabs directory and create a new subfolder labeled “Demolition_Mod”. Next, copy in the “DirTypeWorlds” and “DirTypePrefab” files from any of the existing prefab folders into this new folder so that any prefabs placed within will show up in DEdit. When this is done, just fire up DEdit and you’re ready to begin.

**Note:** For reference, the completed prefabs have been included in the `Tools/Docs/Demolition_Final/Prefabs/Demolition_mod` folder.

The first prefab will consist of global objects, including the main timer display, time limit reached triggers and startup commands. In DEdit, create a new world called “GlobalObjects.ltc” and save it in the folder you just created. Next, from the world menu, add the following objects to the level:

1 DisplayTimer

12 StartupCommands

10 Triggers

How you arrange these objects within the level isn’t very important since they will not be visible at runtime. However, you should space them out enough so that they are distinguishable from each other in case you need to make changes in the future. Once this is done, you’ll need to modify each object for it’s specific purpose by selecting the object in a viewport or checking it in the node tree. When the object has been selected, click on the “Properties” tab, and modify the object as described below. DO NOT change any options except for those specified for each object or you may get unexpected results.

You will see error messages from DEdit indicating that it cannot find the objects you are referring to in your commands. This is ok for now, as the other objects will not exist until all of the necessary prefabs have been placed in an actual map. Make sure that you modify ONLY the specified properties to avoid unexpected results.

This is the object that controls the main timer that appears at the top of the screen at the start of a round and counts down to 0 as the level progresses. Modify it’s properties as follows:

Name DisplayTimer_Main

EndCommand msg #.TimeLimit_Reached_Blue trigger; msg #.TimeLimit_Reached_Red trigger

This sends a command to start the main DisplayTimer object.

Name Startup_MainDisplayTimer

SafeExecute TRUE

Command msg #.DisplayTimer_Main (start 600.00)

This will set up the bomb targets so that only the Blue team may plant bombs and see the location of the correct target on radar. Set it’s options like this:

Name Startup_BombTargets_Blue:

SafeExecute TRUE

RoundCondition Odd

Command Rand5 (msg BombTarget00.SelectTarget_Blue trigger) (msg BombTarget01.SelectTarget_Blue trigger) (msg

BombTarget02.SelectTarget_Blue trigger) (msg BombTarget03.SelectTarget_Blue trigger) (msg BombTarget04.SelectTarget_Blue trigger)

This will set up the bomb targets so that only the Red team may plant bombs and see the location of the correct target on radar.

Name Startup_BombTargets_Red

SafeExecute TRUE

RoundCondition Even

Command Rand5 (msg BombTarget00.SelectTarget_Red trigger) (msg BombTarget01.SelectTarget_Red trigger) (msg

BombTarget02.SelectTarget_Red trigger) (msg BombTarget03.SelectTarget_Red trigger) (msg BombTarget04.SelectTarget_Red trigger)

This sets up the time bomb pickups so that only the Blue team sees their location on radar

Name Startup_BombPickups_Blue

SafeExecute TRUE

RoundCondition Odd

Command Rand5 (msg BombPickup00.SelectLocation_Blue trigger) (msg BombPickup01.SelectLocation_Blue trigger)

(msg BombPickup02.SelectLocation_Blue trigger) (msg BombPickup03.SelectLocation_Blue trigger) (msg BombPickup04.SelectLocation_Blue trigger)

This sets up the time bomb pickups so that only the Red team sees their location on radar.

Name Startup_BombPickups_Red:

SafeExecute TRUE

RoundCondition Odd

Command Rand5 (msg BombPickup00.SelectLocation_Red trigger) (msg BombPickup01.SelectLocation_Red trigger)

(msg BombPickup02.SelectLocation_Red trigger) (msg BombPickup03.SelectLocation_Red trigger) (msg BombPickup04.SelectLocation_Red trigger)

On odd rounds, this will lock the trigger that gives the Blue team points for winning a round if the time limit runs out.

Name Startup_TimeLimitLock_Blue

SafeExecute TRUE

RoundCondition Odd

Command msg #.TimeLimit_Reached_Blue lock

On even rounds, this will lock the trigger that gives the Red team points for winning a round if the time limit runs out.

Name Startup_TimeLimitLock_Red

SafeExecute TRUE

RoundCondition Even

Command msg #.TimeLimit_Reached_Red lock

This will modify the team properties of the game start points so that the blue team starts on the attacking side of the level, and the red team starts on the defending side.

Name Startup_GameStartPoints_Odd

SafeExecute FALSE

RoundCondition Odd

Command msg #.StartPoints_OddRound_Attacking trigger; msg #.StartPoints_OddRound_Defending trigger

This will modify the team properties of the game start points so that the red team starts on the attacking side of the level, and the blue team starts on the defending side.

Name Startup_GameStartPoints_Even

SafeExecute FALSE

RoundCondition Even

Command msg #.StartPoints_EvenRound_Attacking trigger; msg #.StartPoints_EvenRound_Defending trigger

This object will initialize the Demolition_GameState variable to 0 at the start of each round.

Name Init_Gamestate

SafeExecute FALSE

RoundCondition All

Command SET Demolition_GameState 0

**Important:** Before using any variable in a command in DEdit, you must first declare the variable as either global or level-specific in `attributes/commands.txt`. In this case, add the following line under `globals`, and then save the file.

cmd40 = "int Demolition_GameState 0"

This will inform the WorldProperties object that the Red team acts as the Attackers at the start of each Even-numbered round.

Name Startup_WorldProperties_Even

SafeExecute FALSE

RoundCondition Even

Command msg worldproperties0 (AttackingTeam 1)

This will inform the WorldProperties object that the Blue team acts as the Defenders at the start of each Even-numbered round.

Name Startup_WorldProperties_Odd

SafeExecute FALSE

RoundCondition Odd

Command msg worldproperties0 (AttackingTeam 0)

Set up the properties of the first 2 trigger objects as follows. One of these will be activated when the main DisplayTimer reaches 0.

Name Timelimit_Reached_Blue

Command1 msg player (transmission 7105 0)

Command2 msg worldproperties0 (RoundWon 0)

Command3 Delay 3.0 (msg worldproperties0 nextround)

PlayerTriggerable False

Name Timelimit_Reached_Red

Command1 msg player (transmission 7104 0)

Command2 msg worldproperties0 (RoundWon 1)

Command3 Delay 3.0 (msg worldproperties0 nextround)

PlayerTriggerable False

These triggers are called by the GameStartPoint objects and send appropriate transmission messages to players based on their team’s current objectives as they join the game or start a new round. These commands also give an extra weapon to Attackers each time they spawn in for game-balancing purposes. Set them up like this:

Name Blue_Attacking_Msg

Command1 msg activeplayer (acquireweapon silencedsterling)

Command2 msg activeplayer (acquireammo 9mm fmj)

Command3 IF (Demolition_GameState == 0) THEN (msg activeplayer (transmission 7096 0 0))

Command4 IF (Demolition_GameState == 1) THEN (msg activeplayer (transmission 7098 0 0))

Command5 IF (Demolition_GameState == 2) THEN (msg activeplayer (transmission 7100 0 0))

PlayerTriggerable False

Locked True

Name Red_Attacking_Msg

Command1 msg activeplayer (acquireweapon silencedsterling)

Command2 msg activeplayer (acquireammo 9mm fmj)

Command3 IF (Demolition_GameState == 0) THEN (msg activeplayer (transmission 7096 0 1))

Command4 IF (Demolition_GameState == 1) THEN (msg activeplayer (transmission 7098 0 1))

Command5 IF (Demolition_GameState == 2) THEN (msg activeplayer (transmission 7100 0 1))

PlayerTriggerable False

Locked True

Name Blue_Defending_Msg

Command1 IF (Demolition_GameState == 0) THEN (msg activeplayer (transmission 7097 0 0))

Command2 IF (Demolition_GameState == 1) THEN (msg activeplayer (transmission 7099 0 0))

Command3 IF (Demolition_GameState == 2) THEN (msg activeplayer (transmission 7101 0 0))

PlayerTriggerable False

Locked True

Name Red_Defending_Msg

Command1 IF (Demolition_GameState == 0) THEN (msg activeplayer (transmission 7097 0 1))

Command2 IF (Demolition_GameState == 1) THEN (msg activeplayer (transmission 7099 0 2))

Command3 IF (Demolition_GameState == 2) THEN (msg activeplayer (transmission 7101 0 3))

PlayerTriggerable False

Locked True

These are called by the Startup_GameStartPoints startup command objects at the beginning of each round, and are used to set up each game start point for the team they will be utilized by during that round. Modify the final four triggers as follows:

Name StartPoints_OddRound_Attacking

Command1 msg AttackingStartPoint00.gamestartpoint0 (team 0)

Command2 msg AttackingStartPoint01.gamestartpoint0 (team 0)

Command3 msg AttackingStartPoint02.gamestartpoint0 (team 0)

Command4 msg AttackingStartPoint03.gamestartpoint0 (team 0)

Command5 msg AttackingStartPoint04.gamestartpoint0 (team 0)

Command6 msg AttackingStartPoint05.gamestartpoint0 (team 0)

Command7 msg AttackingStartPoint06.gamestartpoint0 (team 0)

Command8 msg AttackingStartPoint07.gamestartpoint0 (team 0)

Command9 msg #.Blue_Attacking_Msg unlock

PlayerTriggerable False

Name StartPoints_OddRound_Defending

Command1 msg DefendingStartPoint00.gamestartpoint0 (team 1)

Command2 msg DefendingStartPoint01.gamestartpoint0 (team 1)

Command3 msg DefendingStartPoint02.gamestartpoint0 (team 1)

Command4 msg DefendingStartPoint03.gamestartpoint0 (team 1)

Command5 msg DefendingStartPoint04.gamestartpoint0 (team 1)

Command6 msg DefendingStartPoint05.gamestartpoint0 (team 1)

Command7 msg DefendingStartPoint06.gamestartpoint0 (team 1)

Command8 msg DefendingStartPoint07.gamestartpoint0 (team 1)

Command9 msg #.Red_Defending_Msg unlock

PlayerTriggerable False

Name StartPoints_EvenRound_Attacking

Command1 msg AttackingStartPoint00.gamestartpoint0 (team 1)

Command2 msg AttackingStartPoint01.gamestartpoint0 (team 1)

Command3 msg AttackingStartPoint02.gamestartpoint0 (team 1)

Command4 msg AttackingStartPoint03.gamestartpoint0 (team 1)

Command5 msg AttackingStartPoint04.gamestartpoint0 (team 1)

Command6 msg AttackingStartPoint05.gamestartpoint0 (team 1)

Command7 msg AttackingStartPoint06.gamestartpoint0 (team 1)

Command8 msg AttackingStartPoint07.gamestartpoint0 (team 1)

Command9 msg #.Red_Attacking_Msg unlock

PlayerTriggerable False

Name StartPoints_EvenRound_Defending

Command1 msg DefendingStartPoint00.gamestartpoint0 (team 0)

Command2 msg DefendingStartPoint01.gamestartpoint0 (team 0)

Command3 msg DefendingStartPoint02.gamestartpoint0 (team 0)

Command4 msg DefendingStartPoint03.gamestartpoint0 (team 0)

Command5 msg DefendingStartPoint04.gamestartpoint0 (team 0)

Command6 msg DefendingStartPoint05.gamestartpoint0 (team 0)

Command7 msg DefendingStartPoint06.gamestartpoint0 (team 0)

Command8 msg DefendingStartPoint07.gamestartpoint0 (team 0)

Command9 msg #.Blue_Defending_Msg unlock

PlayerTriggerable False

When you are done entering and modifying the properties of each of the Global Objects listed above, you can save the level. It is not necessary (or possible) to process prefab levels, so close the level to complete the prefab. However, you may want to move the StartupCommands and Triggers into separate container nodes to organize things a little before saving.

If you now click on the prefabs tab and open the Demolition_Mod folder, you should see the GlobalObjects prefab there, ready to be placed in a level. However, there are several other prefabs that must be built before we can do this.

The BombTarget prefab contains all of the necessary objects and commands needed for each of the 5 bomb targets that will be placed on the defending side of a demolition map. In DEdit, create a new world called “BombTarget.ltc” and add the following objects:

1 Bombable

1 RadarObject

1 Explosion

2 DisplayTimers

8 Triggers

Leave the Bombable and Explosion objects at position 0,0,0. The other objects do not appear in the game at runtime, so they should be moved away from the origin in some sort of organized manner.

This is the actual target object that the players will interact with. It appears as a translucent red bomb in the game. First, make sure the object’s name is set to “Bombable0” and then set the following parameters:

Team Team0

GadgetTargetName Bombable0

DefuseTime 6.00

DetonateTime 60.00

PlantedCommand msg #.BombPlanted_Red trigger; msg #.BombPlanted_Blue trigger; msg #.RadarObject0 (team -1);

SET Demolition_GameState 1

DefusedCommand msg #.BombDiffused_Red trigger; msg #.BombDiffused_Blue trigger; SET Demolition_GameState 2

DetonatedCommand msg #.BombDetonated_Blue trigger; msg #.BombDetonated_Red trigger;

This object marks the location of the target on the radar screen by pointing to the bombable object. Make sure the object’s name is set to “RadarObject0” and set the following options:

Type Destination

StartON False

Target #.Bombable0

This is the damage and associated FX that occurs when the bomb goes off. Leave the object name as “Explosion0”, and then modify the parameters like this:

ImpactFXName ExplosiveCharge

DamageType Explode

DamageRadius 200

MaxDamage 200

These objects will display the bomb countdown timer in the upper right hand corner of the screen when a bomb is planted. The color of the display timer will change depending on which team is defending the base. Name one of these “DisplayTimer_Blue” and set it’s properties like this:

RemoveWhenDone False

Team Team0

Now name the other timer “DisplayTimer_Red”, and then modify it’s properties the same way, except change the “Team” property to “Team1”. Note that both timers send commands to both of the Detonate triggers. This is intentional, as only one of these will be unlocked when the command is sent. This is covered further below.

The Startup_BombTargets_Blue StartupCommand calls this trigger when the round begins. It activates the bombable and radar objects, sets them up for the Blue team, and unlocks the red bomb target triggers. Set this up as follows:

Name SelectTarget_Blue

Command1 msg #.Bombable0 on

Command2 msg #.RadarObject0 on

Command3 msg #.Bombable0 (team 0)

Command4 msg #.RadarObject0 (team 0)

Command5 msg #.BombPlanted_Red unlock

Command6 msg #.BombDiffused_Red unlock

Command7 msg #.BombDetonated_Red unlock

PlayerTriggerable False

Rename this trigger “SelectTarget_Red”. The Startup_BombTargets_Red StartupCommand calls this trigger when the round begins. It activates the bombable and radar objects, sets them up for the Red team, and unlocks the blue bomb target triggers. Set this up as follows:

Name SelectTarget_Red

Command1 msg #.Bombable0 on

Command2 msg #.RadarObject0 on

Command3 msg #.Bombable0 (team 1)

Command4 msg #.RadarObject0 (team 1)

Command5 msg #.BombPlanted_Blue unlock

Command6 msg #.BombDiffused_Blue unlock

Command7 msg #.BombDetonated_Blue unlock

PlayerTriggerable False

Rename this trigger “BombPlanted_Blue”. The Bombable object activates this trigger when the red team plants a bomb. It pauses the main timer, starts the blue bomb timer, sends appropriate transmissions to each time to indicate the bomb has been set, and adds 5 to the score of the player who set the bomb. Set its properties like this:

Name BombPlanted_Blue

Locked True

Command1 msg GlobalObjects00.DisplayTimer_Main pause

Command2 msg #.DisplayTimer_Blue (start 60.0)

Command3 msg player (transmission 7098 0 1)

Command4 msg player (transmission 7099 0 0)

Command5 msg ActivePlayer (score 5)

PlayerTriggerable False

The Bombable object activates this trigger when the blue team plants a bomb. It pauses the main timer, starts the red bomb timer, sends appropriate transmissions to each time to indicate the bomb has been set, and adds 5 to the score of the player who set the bomb. Set its properties like this:

Name BombPlanted_Red

Locked True

Command1 msg GlobalObjects00.DisplayTimer_Main pause

Command2 msg #.DisplayTimer_Red (start 60.0)

Command3 msg player (transmission 7098 0 0)

Command4 msg player (transmission 7099 0 1)

Command5 msg ActivePlayer (score 5)

PlayerTriggerable False

The bombable object activates this trigger when the blue team diffuses the bomb. It restarts the main timer, turns off the blue bomb timer, sends appropriate text messages to each team to indicate that the bomb was diffused, and gives 5 points to the player who diffused the bomb. Set the options as follows:

Name BombDiffused_Blue

Locked True

Command1 msg GlobalObjects00.DisplayTimer_Main resume

Command2 msg #.DisplayTimer_Blue kill

Command3 msg player (transmission 7100 0 1)

Command4 msg player (transmission 7101 0 0)

Command5 msg ActivePlayer (score 5)

PlayerTriggerable False

The bombable object activates this trigger when the red team diffuses the bomb. It restarts the main timer, turns off the red bomb timer, sends appropriate text messages to each team to indicate that the bomb was diffused, and gives 5 points to the player who diffused the bomb. Set the options as follows:

Name BombDiffused_Red

Locked True

Command1 msg GlobalObjects00.DisplayTimer_Main resume

Command2 msg #.DisplayTimer_Red kill

Command3 msg player (transmission 7100 0 0)

Command4 msg player (transmission 7101 0 1)

Command5 msg ActivePlayer (score 5)

PlayerTriggerable False

The active detonation countdown DisplayTimer calls this trigger when it reaches 0. It locks the TimeLimit trigger for the Blue team (to avoid potential problems with photo-finishes), sets off the explosion, sends a transmission to all players that the bomb has detonated, awards the round to the red team, and starts the next round after a 3 second delay. Set it’s options like this:

Name BombDetonated_Blue

Locked True

Command1 msg GlobalObjects00.TimeLimit_Reached_Blue lock

Command2 msg #.explosion0 start;

Command3 msg player (transmission 7103 0)

Command4 msg worldproperties0 (RoundWon 1)

Command5 Delay 3.0 (msg worldproperties0 nextround)

PlayerTriggerable False

The active detonation countdown DisplayTimer calls this trigger when it reaches 0. It locks the TimeLimit trigger for the Red team (to avoid potential problems with photo-finishes), sets off the explosion, sends a transmission to all players that the bomb has detonated, awards the round to the Blue team, and starts the next round after a 3 second delay. Set it’s options like this:

Name BombDetonated_Red

Locked True

Command1 msg GlobalObjects00.TimeLimit_Reached_Red lock

Command2 msg #.explosion0 start;

Command3 msg player (transmission 7102 0)

Command4 msg worldproperties0 (RoundWon 0)

Command5 Delay 3.0 (msg worldproperties0 nextround)

PlayerTriggerable False

When you are done creating and modifying the objects for the BombTarget prefab, save the level and move on to the next section.

The BombPickup prefab contains all of the necessary objects and commands needed for each of the 5 bomb pickups that will be placed on the attacking side of a demolition map. In DEdit, create a new world called “BombPickup.ltc” and add the following objects:

1 Weaponitem

1 RadarObject

1 Spawner

1 ObjectLight

2 Triggers

Leave the Weaponitem and Spawner objects at position 0,0,0. The other objects do not appear in the game at runtime, so they should be moved away from the origin in some sort of organized manner.

This is the time bomb weapon pickup that players can walk over or activate to add a bomb to their inventory. Set up the options like this:

Name WeaponItem0

Template True

RespawnTime 10.000

WeaponType Timebomb

AmmoAmount 1

This object spawns in the time bomb at the location specified by the Startup_BombPickups StartupCommand. Set it up as follows:

Name Spawner0

Target #.weaponitem0

This light ensures that the bomb powerup is visible, even if it is placed in a somewhat dark area of a level.

Name ObjectLight0

FastLightObjects False

LightRadius 50.000

This object marks the location of the bomb pickup on the radar screen by pointing to the spawner object. It cannot point directly to the time bomb object since the time bomb doesn’t exist until the spawner creates it. Set it’s properties to:

Name RadarObject0

Type Objective

Target #.Spawner0

The Startup_BombPickups_Blue StartupCommand calls this trigger when the round begins. It instructs the spawner to create the time bomb, and turns on the radar object for the blue team.

Name SelectLocation_Blue

Command1 msg #.Spawner0 spawn

Command2 msg #.RadarObject0 on

Command3 msg #.RadarObject0 (team 0)

PlayerTriggerable False

The Startup_BombPickups_Red StartupCommand calls this trigger when the round begins. It instructs the spawner to create the time bomb, and turns on the radar object for the red team.

Name SelectLocation_Red

Command1 msg #.Spawner0 spawn

Command2 msg #.RadarObject0 on

Command3 msg #.RadarObject0 (team 1)

PlayerTriggerable False

When you are done creating and modifying the objects for the BombTarget prefab, save the level and move on to the next section.

This prefab contains a GameStartPoint object that is set up specifically for the Attacking team. Create a new world called “AttackingStartPoint.ltc” and add a single GameStartPoint object at grid position 0,0,0. Then, modify it’s properties as follows:

Command msg GlobalObjects00.Blue_Attacking_Msg trigger; msg GlobalObjects00.Red_Attacking_Msg trigger

SendCommandOnRespawn True

Team NoTeam

When done, save the level.

This prefab contains a GameStartPoint object that is set up specifically for the Defending team. Create a new world called “DefendingStartPoint.ltc” and add a single GameStartPoint object at grid position 0,0,0. Then, modify it’s properties as follows:

Command msg GlobalObjects00.Blue_Defending_Msg trigger; msg GlobalObjects00.Red_Defending_Msg trigger

SendCommandOnRespawn True

Team NoTeam

When done, save the level. You have now finished making all of the necessary prefabs for a demolition map. In the next section, you’ll learn how to place these prefabs in a level.

A good Demolition level will feature a reasonably defendable base of some sort where the defending team will spawn, and where all of the bomb targets are located. For the attacking team, a good sized but not necessarily fortified area to gather weapons and search for the time bomb is also needed. The level should be large enough to space out the bomb targets so that their icons do not seem too close together on radar, and to provide multiple attack routes to each of the targets.

The sample deathmatch map included with this release is a good example of a mid-sized deathmatch map that can be easily converted for demolition. The streets outside of the compound provide a staging area for the attackers, while the defenders all begin in some dilapidated apartment buildings and the courtyard that sits alongside of them. Since this is a mid-sized map, it will probably only support 4-8 players comfortably, but this is fine for the purposes of this tutorial.

Since you have already created prefabs that contain all of the necessary objects, level designers who want to make maps for demolition mode don’t have to do much more than drop them into the level and move some of the components where needed. Follow the steps below to convert dm_demolition for use with the demolition mod:

1. In DEdit, click on the “Worlds” Tab
2. Open the “RetailMultiplayer” folder
3. Open the world named “dm_demolition”.
4. Move the marker to an area outside of the normal level geometry.
5. Click on the “Prefabs” tab.
6. Open the Demolition folder.
7. Place a BombTarget Prefab on the barrels near the helicopter in the courtyard, the propane tank in the alley, the safe in the back room, the back of the generator closest to the armory, and the large computer in the computer room.
8. Place 5 BombPickup Prefabs around the streets outside of the compound.
9. Place a GlobalObjects Prefab in an area outside of the visible level geometry. It’s exact location is not important.
10. Replace GameStartPoint0 through GameStartPoint06 with AttackingStartPoint Prefabs. Make sure to rotate them accordingly.
11. Replace GameStartPoint07 through GameStartPoint14 with DefendingStartPoint Prefabs.
12. Make sure that the WorldProperties object is named “WorldProperties0” so that the demolition objects can send commands to end the level and award points to players and teams as needed.
13. Save the level back to the RetailMultiplayer folder as “de_demolition”.
14. Process the level normally.

And that’s it! You now have a fully functional demolition map that can be rezzed into a mappack or included with the mod distributable. You can use the map as-is, or you can modify the map further. Note that in it’s current form no actual damage is done to the targets when the bombs go off. Creating convincing destruction sequences are beyond the scope of this tutorial. If you want to make the bombs do damage without spending a lot of time, a quick solution might be to make the targets simply disappear and spawn debris when the bomb timer reaches 0. Or, if you are feeling adventurous, you may want to experiment with creating “before” and “after” WorldModels that can be hidden and unhidden as needed. How much work is done for this is entirely up to the level designer, and has no real impact on gameplay either way.

**Note:** For reference, the completed `de_demolition.tbw` and `de_demolition.dat` files have been included in the `Tools/Docs/Demolition_Final/Worlds/RetailMultiPlayer` folder.

Congratulations, you have now completed the first major step in mod creation. The next step is to modify the game code. See the **Building the Nolf 2 Source** document for details on how to accomplish this.

Once the source code modifications are complete, you’ll need to create a distributable .rez file that contains all of the files necessary to play the mod and create new levels. For demolition, create a .rez file called “Demolition.rez” and add the following files:

Required:

**Cres.dll** **Cshell.dll** **Object.lto**

**\Attributes\Commands.txt**

**\Worlds\RetailMultiPlayer\de_demolition.dat**

All of the files in the **\Prefabs\Demolition_Mod** folder.

Optional (if you want others to be able to modify the level itself):

**\Worlds\RetailMultiPlayer\de_demolition.tbw**

All of the files in the **\Prefabs\Demolition_Map** folder

For instructions on making .rez files, see the **Creating Content Packs and Modifications** document.

Note that a completed “Demolition.rez” file is included in this release. To install it, just right-click the Demolition_Mod archive in your main Nolf 2 installation folder, and then select “Extract to here”. This will automatically add The Demolition.rez file to the Custom/Mods/Demolition folder. To play it, run Nolf 2 and select Demolition from the custom menu in the launcher, and then host a LAN or Internet game.
