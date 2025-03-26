# Building the No One Lives Forever 2 Game
## Overview
This document will describe the necessary steps to build the No One Lives Forever 2 (NOLF2) game projects. After building the projects you will need to refer to the section `How to Create a Mod`, which will tell you how to distribute your executables.

## Visual C++ Environment
Before building the game, you must setup your Visual C++ Environment. You will need Microsoft Visual C++ 6.0.

The game needs 3 environment variables to be defined for the executables to publish themselves correctly. The projects use these environment variables in their custom build step to copy or publish themselves to the install folder.  You will need to change this for your machine. You must set these before starting the IDE. You can set them in your system’s environment variables.  Alternatively, you can set them in a command window, and then launch msdev.exe from the command window.  The environment variables are in the following table.

| Environment Variable  | Description       | Example |
| -----                 |  -----            | -----   |
| GAME_MAIN_DIR         | Main directory    | C:\NOLF2\ |
| GAME_REZ_DIR          | Rez files         | C:\NOLF2\Game |
| GAME_TOOLS_DIR        | Tools Directory   | C:\NOLF2\Tools |

## Directory Structure
The next step is to setup the source directory structure. Unzip the source code into it’s folder, such as `c:\program files\fox\no one lives forever 2\tools\source`. The source is split up into three major categories: Engine, Game and Libs. These categories are described in the table below:

| category | Projects | Path | Description |
| ----- | ----- | -----| ----- |
| TO2 | Workspace | Game\TO2.dsw | Game workspace containing dependencies between game projects.
| | AutoRun | game\autorun.dsp | Autorun project | 





 
AutoRun2
 game\autorun2.dsp
 Autorun2 project for 2nd CD.
 
ButeMgr
 libs\butemgr.dsp
 Attribute file manager
 
ButeMgrMfcDll
 libs\butemgrmfcdll.dsp
 MFC DLL version of the Attribute file manager.
 
ClientFxDLL
 Game\ClientFXDll
 Client effects component.
 
ClientRes
 Game\ClientRes\TO2\

ClientRes.dsp
 Client side Resource DLL project.
 
ClientShellDLL
 Game\ClientShellDLL\TO2\

ClientShellDLL.dsp
 Client side game dll project.
 
ClientShellShared
 Game\ClientShellDLL\

ClientShellShared\ClientShellShared.dsp
 Client side game lib project.
 
Game
 game\game.dsp
 Project which is parent of all game projects.
 
Launcher
 Game\Launcher\TO2\Launcher.dsp
 Game launcher project.
 
LTGUIMgr
 Game\libs\LTGUIMgr\ltguimgr60.dsp
 GUI support lib.
 
Object
 Game\ObjectDLL\TO2\Object.dsp
 Server side game dll project.
 
ObjectShared
 Game\ObjectDLL\ObjectShared\ObjectShared.dsp
 Server side game lib project
 
ServerApp
 Game\ServerApp\ServerApp.dsp
 Stand-alone server application.
 
ServerRes
 Game\ServerRes\TO2\ServerRes.dsp
 Server side Resource DLL
 
Engine
 SDK
 Engine\SDK
 Include and link files for Engine.
 
Libs
 ButeMgr
 libs\ButeMgr\ButeMgr.dsp
 Attribute file manager.
 
ButeMgrMfcDll
 libs\ButeMgr\ButeMgrMfcDll.dsp
 MFC DLL version of attribute file manager.
 
CryptMgr
 libs\CryptMgr\cryptmgr.dsp
 Encryption manager.
 
CryptMgrMfcDll
 libs\CryptMgr\CryptMgrMfcDll.dsp
 MFC DLL version of encryption manager.
 
Lib_Lith
 libs\lith\Lib_Lith.dsp
 Utility library
 
Lib_StdLith
 libs\stdlith\Lib_StdLith.dsp
 Utility library
 
MFCStub
 libs\MFCStub\MFCStub60.dsp
 Non-MFC versions of some useful MFC classes.
 
RegMgr
 libs\RegMgr\regmgr60.dsp
 Registry manager
 
RegMgr32
 libs\RegMgr32\regmgr32.dsp
 Yet another Registry manager.

## Building
All the projects can be built through the game’s DSW located at `game\TO2.dsw`. The projects have their dependencies setup in this DSW. The DSW contains a helper NMAKE builder project that will build all the sub-projects with proper dependencies. This is located in `game\game.dsp`. The easiest way to build is using the game.dsp project. Select it as your active project and choose your build target of Debug, Release or Final. All the projects contain these targets. You can also use the batch files in the root source folder called `BuildDebug.bat`, `BuildRelease.bat` and `BuildFinal.bat`.

Debug and Release build targets enable helpful debugging tools while running the game.  Final is used to build the final version you will use for distribution and disables these debugging features.  

The temporary build files are built into a `Built` directory.  For the game projects, they are built into `game\built`.  For the libs, they are built in `libs\built`.

The executable files are published according to your environment variables that you set in the section “Visual C++ Environment”.

## Modifying Resource ID’s
As a special note on modifying resources in source code, it must be mentioned to be careful of changing existing resource ID’s. Some components cannot be built from this tools source release and may rely on the resource ID values to remain the same. Changing them could cause unpredictable results.  Instead, add new resource ID’s to the end of a range. Replacing string contents with something valid for your modifications should be ok, as long as you know how the string is used in code.

## Debugging Features
If you build debug or release configurations, some helpful debugging features will be enabled while running the game. When you distribute your mod, you should build using the Final build configuration. The debugging features are described in the table below.

 

Feature
 Key Mapping
 Description
 
Ghost Mode
 F1
 This will make you invisible to AI. You can still get thier attention through other means.
 
Spectator Mode
 F2
 This will allow you to fly through a level and clip through all objects and geometry.
 
AI Info
 F5
 AI info
 
View Volumes
 F11
 This key will cycle through several modes, allowing you to see various types of volumes and nodes in-game.
 
View Nodes
 Shift-F11
 View AI Nodes.