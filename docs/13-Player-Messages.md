# Player Messages

The “player” object handles a number of different trigger messages. This document will list the syntax and results of these various messages. In the syntax definitions below, parameters that appear in angle brackets, i.e. < > are required parameters. Parameters that appear in square brackets, i.e. [ ] are optional.

Most of the player messages to affect the game music take an optional timing parameter. This parameter may be any of the following:

Default - Will use the default value that is defined in the Control File or by DirectMusic

Immediately - Will happen immediately

Beat - Will happen on the next beat

Measure - Will happen on the next measure

Grid - Will happen on the next grid

Segment - Will happen on the next segment transition

This command changes the intensity of the music.

Music i <intensity> [timing]

Music intensity <intensity> [timing]

This command will play a secondary segment.

Music secondary <segment name> [timing]

Music ps <segment name> [timing]

This command will play a motif.

Music motif <motif style> <motif name> [timing]

Music pm <motif style> <motif name> [timing]

This command will adjust the volume of the music.

Music volume <volume adjustment in db> Music v <volume adjustment in db>

This command will stop a secondary segment.

Music stopsecondary <segment name> [timing]

Music ss <segment name> [timing]

This command will stop a motif.

Music stopmotif <motif name> [timing]

Music sm <motif name> [timing]

This command will start the music playing.

Music play

Music p

This command will stop playing the music.

Music stop [timing]

Music s [timing]

This command will lock the music in the current mood.

LockMood

LockMusic

This command will unlock the music from the currently locked mood.

LockMood

LockMusic

This command will lock the music in the current motif.

LockMotif

LockEvent

This command will unlock the music from the currently locked motif.

LockMotif

LockEvent

Rewards give the player experience points. The <reward name> parameter specifies the name of the reward given. The amount of experience received is set in missions.txt and is indexed by <reward name>

Reward <reward name>

The player’s objectives are divided into three classes. Objectives are goals which must be accomplished to complete the mission. Optional Objectives are goals that may be accomplished, but are not required. Mission Parameters are rules for how your objectives may be accomplished. The objective IDs referred to in these commands are the ids of strings in the CRes.dll string table.

These commands will add a new required item.

Objective add <objective id>

Option add <optional id>

Parameter add <parameter id>

These commands will remove an item.

Objective remove <objective id>

Option remove <optional id>

Parameter remove <parameter id>

These command will remove all items.

Objective removeall

Option removeall

Parameter removeall

This command will mark an objective or optional objective as completed. Parameters cannot be marked for completion.

Objective completed <objective id>

Option completed <optional id>

The key IDs referred to in these commands are the ids of entries in the KeyItems.txt attributes file.

This command will add a new key item.

Key add <key id>

This command will remove a key item.

Key remove <key id>

This command will remove all key items.

Key removeall

Transmissions are text messages that are sent to the player. The transmission ID referred to in this command is the id of a string in the CRes.dll string table. The ActivePlayerComm is an optional parameter set to 1 or 0. If set to 1, then the transmission will be displayed with the MP name of the ActivePlayer in this format: “< ActivePlayerName >: <Message>”. The TeamNumber is an optional parameter set to 1 or 0, referring to the team numbers. Only players on the TeamNumber team will receive the transmission.

Transmission <transmission id> [ ActivePlayerComm ][ TeamNumber ]

The credits message starts or stops the on screen credits.

This message will start the display of credits.

Credits on

This message will stop the display of credits.

Credits off

This message will start the display of the intro credits.

Credits intro

This message will give the player an intelligence item.

The <text id> parameter is the ID of a string in the CRes.dll string table.

The <popup id> parameter is the ID of an entry in the PopupItems.txt attributes file which will define how the item will be displayed in popups and in the menus.

The [ intel ] parameter should be 1 if the item should be considered as valuable intelligence data and 0 if it should be considered general information. This will be 0 by default.

The [show] parameter should be 1 if the popup up should be displayed and 0 if it should not. This will be 0 by default.

The [add] parameter should be 1 if the intel item is to be added to the list of intelligence items the player sees in the menu. This will be 1 by default.

MissionText <text id> <popup id> [ intel ] [show] [add]

These messages cause the screen to fade in or fade out over the given number of seconds.

FadeIn <time>

FadeOut <time>

This message will cause text to appear teletype style on the screen. The text id is the id of a string in the CRes.dll string table.

MissionText <text id>

This message will let the Mission Failure screen to appear and display the specified text. The text id is the id of a string in the CRes.dll string table.

MissionFailed <text id>

This message will remove all body objects that are currently in the level.

RemoveBodies

This message will remove all AI in the level that are considered “Bad” to the player.

RemoveAllBadAI

This message will reset all the weapons and give only the default weapon for the mission.

ResetInventory

PickupItems are any item that the player can pickup throughout the levels. They may also be acquired through searching or by being a default of the mission.

This message will give the player the specified weapon and will switch to that weapon.

AcquireWeapon <weapon name>

This message tells the player to change to the specified weapon if they currently have the weapon. The <weapon name> parameter refers to the name of a weapon definition in weapons.txt.

ChangeWeapon <weapon name>

This message will give the player the specified ammo.

AcquireAmmo <ammo name>

This message will give the player the specified weapon mod.

AcquireMod <mod name>

This message will give the player the specified gear.

AcquireGear <gear name>

This message will give the player the max amount of health.

FullHealth

This message will clear the sleeping damage rom the player

Wakeup

The player can have vehicle physics applied to them in a number of circumstances. Riding a PlayerVehicle , a snowmobile, is the most obvious but following a PlayerLure is also considered riding a vehicle.

This message will force the player to get off on vehicle they currently are on and use the normal player physics

Dismount

This message tells the player to begin following the specified PlayerLure . The < PlayerLure name> parameter must refer to the name of a PlayerLure object on the level.

FollowLure < PlayerLure name>

This message will tell the player to stop following any lure it is currently following.

CancelLure

Overlays are sprites that are displayed on screen such as the scope crosshairs, and certain cinematic specific overlays. To define what sprites are displayed per overlay look in the Overlay section of layout.txt.

This message turns the specified overlay on or off. The <Overlay Id> parameter is the id of the overlay to use. For a list of overlay Ids see ClientShellDLL\ClientShellShared\Overlays.h . The <On or Off > parameter specifies if the overlay should be rendered on the screen or not.

Overlay < OverlayId > <On or Off>

Objects that the player can carry, such as bodies and DoomsDayPieces , may be dropped through a message. The message name is misleading but all carried objects can be dropped through this message.

DropBody

This message provides a way to modify the players score for any event. The <+/- amount> parameter is simply the amount you want the players score to change by, positive or negative. When in team games, the players team score will also change by the new amount.

Score <+/- amount>
