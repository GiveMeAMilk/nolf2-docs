# Building the No One Lives Forever 2 Game

This document describes the steps required to build the No One Lives Forever 2 (NOLF2) game projects. After building the projects, refer to the section about creating a mod to package and distribute your executables.

## Visual C++ Environment

Before building the game, you must set up your Visual C++ environment. You will need Microsoft Visual C++ 6.0.

The game needs three environment variables to be defined for the executables to publish themselves correctly. The projects use these variables in their custom build step to copy or publish themselves to the install folder. You will need to adjust them for your machine.

Set these variables before starting the IDE. You can define them in your system environment variables, or you can set them in a command window and then launch `msdev.exe` from that same window.

| **Environment Variable** | **Description** | **Example** |
| --- | --- | --- |
| `GAME_MAIN_DIR` | Main directory | `C:\NOLF2\` |
| `GAME_REZ_DIR` | Rez files | `C:\NOLF2\Game` |
| `GAME_TOOLS_DIR` | Tools directory | `C:\NOLF2\Tools` |

## Source Layout

The next step is to set up the source directory structure. Unzip the source code into its folder, such as `c:\program files\fox\no one lives forever 2\tools\source`.

The source is split into three major categories: Engine, Game, and Libs. These categories are described in the table below.

| **Category** | **Projects** | **Path** | **Description** |
| --- | --- | --- | --- |
| `TO2` | `<Workspace>` | `Game\TO2.dsw` | Game workspace containing dependencies between game projects. |
| `AutoRun` | `game\autorun.dsp` | Autorun project |  |
| `AutoRun2` | `game\autorun2.dsp` | Autorun2 project for 2nd CD. |  |
| `ButeMgr` | `libs\butemgr.dsp` | Attribute file manager |  |
| `ButeMgrMfcDll` | `libs\butemgrmfcdll.dsp` | MFC DLL version of the attribute file manager. |  |
| `ClientFxDLL` | `Game\ClientFXDll` | Client effects component. |  |
| `ClientRes` | `Game\ClientRes\TO2\ClientRes.dsp` | Client-side resource DLL project. |  |
| `ClientShellDLL` | `Game\ClientShellDLL\TO2\ClientShellDLL.dsp` | Client-side game DLL project. |  |
| `ClientShellShared` | `Game\ClientShellDLL\ClientShellShared\ClientShellShared.dsp` | Client-side game library project. |  |
| `Game` | `game\game.dsp` | Project which is parent of all game projects. |  |
| `Launcher` | `Game\Launcher\TO2\Launcher.dsp` | Game launcher project. |  |
| `LTGUIMgr` | `Game\libs\LTGUIMgr\ltguimgr60.dsp` | GUI support library. |  |
| `Object` | `Game\ObjectDLL\TO2\Object.dsp` | Server-side game DLL project. |  |
| `ObjectShared` | `Game\ObjectDLL\ObjectShared\ObjectShared.dsp` | Server-side game library project. |  |
| `ServerApp` | `Game\ServerApp\ServerApp.dsp` | Stand-alone server application. |  |
| `ServerRes` | `Game\ServerRes\TO2\ServerRes.dsp` | Server-side resource DLL. |  |
| `Engine` | `SDK` | `Engine\SDK` | Include and link files for the engine. |
| `Libs` | `ButeMgr` | `libs\ButeMgr\ButeMgr.dsp` | Attribute file manager. |
| `ButeMgrMfcDll` | `libs\ButeMgr\ButeMgrMfcDll.dsp` | MFC DLL version of the attribute file manager. |  |
| `CryptMgr` | `libs\CryptMgr\cryptmgr.dsp` | Encryption manager. |  |
| `CryptMgrMfcDll` | `libs\CryptMgr\CryptMgrMfcDll.dsp` | MFC DLL version of the encryption manager. |  |
| `Lib_Lith` | `libs\lith\Lib_Lith.dsp` | Utility library. |  |
| `Lib_StdLith` | `libs\stdlith\Lib_StdLith.dsp` | Utility library. |  |
| `MFCStub` | `libs\MFCStub\MFCStub60.dsp` | Non-MFC versions of useful MFC classes. |  |
| `RegMgr` | `libs\RegMgr\regmgr60.dsp` | Registry manager. |  |
| `RegMgr32` | `libs\RegMgr32\regmgr32.dsp` | Another registry manager. |  |

## Building the Projects

All the projects can be built through the game’s DSW located at `game\TO2.dsw`. The projects have their dependencies set up in this DSW. The DSW contains a helper NMAKE builder project that will build all the sub-projects with proper dependencies. This is located in `game\game.dsp`.

The easiest way to build is to use the `game.dsp` project. Select it as your active project and choose your build target of Debug, Release, or Final. All the projects contain these targets. You can also use the batch files in the root source folder:

- `BuildDebug.bat`
- `BuildRelease.bat`
- `BuildFinal.bat`

Debug and Release build targets enable helpful debugging tools while running the game. Final is used to build the final version you will use for distribution and disables these debugging features.

The temporary build files are written into a `Built` directory. For the game projects, they are built into `game\built`. For the libraries, they are built into `libs\built`.

The executable files are published according to the environment variables defined in the Visual C++ environment section above.

## Modifying Resource ID’s

When modifying resources in source code, be careful not to change existing resource IDs. Some components cannot be built from this tools source release and may rely on those values remaining unchanged. Changing them could cause unpredictable results.

Instead, add new resource IDs to the end of a range. Replacing string contents with something valid for your modifications is generally safe, as long as you understand how the string is used in code.

## Debug Features

If you build debug or release configurations, some helpful debugging features will be enabled while running the game. When you distribute your mod, you should build using the Final build configuration. The debugging features are described in the table below.

| **Feature** | **Key Mapping** | **Description** |
| --- | --- | --- |
| Ghost Mode | F1 | This will make you invisible to AI. You can still get their attention through other means. |
| Spectator Mode | F2 | This will allow you to fly through a level and clip through all objects and geometry. |
| AI Info | F5 | AI info |
| View Volumes | F11 | This key will cycle through several modes, allowing you to see various types of volumes and nodes in-game. |
| View Nodes | Shift-F11 | View AI Nodes. |
