# Using DEdit to Create Worlds

![DEdit001](images/DEdit001.jpg)

Welcome to the DEdit overview and tutorial. DEdit is the tool created by the LithTech team that enabled the NOLF2 Level Designers and Artists to create the geometry and gameplay you experienced in No One Lives Forever 2 (NOLF2). DEdit allows you to build the ground, sky, walls, ceilings and shapes for your levels. You will then apply textures, props, prefabs, lights and sounds to give them a realistic appearance. No One Lives Forever 2 was created using literally thousands of these assets, which you may appropriate to create the base for your own level. You may also add your own assets where applicable. Finally, you’ll add the game objects that allow other players to interact with your world.

Creating levels is an extremely complex and time-consuming process, and the following is merely the starting point for those who want to learn the basics of building worlds for the LithTech Jupiter engine. If you’ve done game design before on a 3D or near-3D game, you’ve probably worked with tools like DEdit. A separate document will cover ModelEdit, the companion to DEdit, which allows you to create characters and models for your world.

These terms are relevant to a discussion of DEdit.

**Project** — A **project** in DEdit represents the sum of all the resources in the game: all the code, all the textures, all the sounds, all the worlds, and so on. Unlike other world geometry editors, DEdit first opens the project, rather than a world file.

**World** — When your players walk around in your game, it is a **world** that they’re standing in. Worlds divide your game up into sections where different parts of the game take place. In other games, these are sometimes referred to as maps, levels, scenes, or episodes. World editing is the primary focus of DEdit and each world is stored in a separate file on the hard drive.

**Objects** — Simply put, anything a player interacts with that moves, lights up, shoots, growls, or goes into the player’s inventory is an **object.** DEdit allows you to place any kind of object that your game’s code or the engine’s code can create.

**World Geometry** — Parts of the world that act as walls, floors and sky are generally made of **world geometry.** Such geometry is solid, immovable, and generally never changes.

**Brush** — The basic unit of world geometry. A brush is made up of planes that define its faces, lines that define its edges, and vertices that define its corners. You can manipulate either an entire brush at once or any of the vertices, lines, or planes in the brush.

**Polygon** — A closed plane figure bounded by straight sides. Most of the geometry created in DEdit and used for the LithTech Jupiter engine is one sided. As a result most of the creation process involves working with polygons instead of entire brushes.

**Primitive** A simple shape that you can add to the world as the foundation of a more complex shape. Typical primitives are things such as cubes, pyramids, and cylinders.

**Prefab** — A prefab is like a primitive, but more complex. If you build a street lamp complete with textures and a light source that gives off just the right shade of light, you can select the lamp and its associated source (or any group of objects and brushes inside DEdit) and save it as a **prefab.** Thereafter, you can copy and paste that streetlamp into your world without having to rebuild the whole object.

**Unit** — The basis of measurement in DEdit and the LithTech Jupiter engine. Units don’t equate directly to real-world values. Instead, the game designers can select a scale of game units to real-world measurements. As an example, in No One Lives Forever 2 the following values are used: railings are 56 units tall, a chest-high box would be 64 units, and a typical doorway would be 128 units high.

**Mode** — DEdit has several different modes that allow you to change certain elements of your world (i.e. just brushes or just objects) without accidentally affecting others. They’re designed to simplify interacting with your world while editing, so it’s important to choose the right mode for your task.

**Processing** — When you **process** your world, DEdit creates a second version of the world with some information removed (parts only you need to know about), and other information added (parts only the game engine needs). **Processing** is a necessary step you’ll take in getting your world up and running in the game, and is often the first place where you will discover problems with your level.

**Texture** — In DEdit, textures are used like wallpaper, paint, or plaster to cover the raw plywood of your walls, floors, ceilings, doors and so forth. Without a texture, your brush will appear flat-shaded in the game, almost always with unpleasant results. Just as you wouldn’t want a house with raw plywood walls, you always want to apply textures to the brushes in your level.

Before starting, you should learn a little more about the structure of the resources that DEdit and LithTech can use in a game. The LithTech Jupiter engine can access and use a wide variety of file types and other resources. The list below is arranged by resource type, and each resource type includes a list of the sorts of files LithTech can use in that type, as well as a description of those files.

**Project** — As mentioned before, the project is the total of your whole game and all its resources. A .DEP (DEdit Project) file at the top of your tree of game resource directories serves as a guide to DEdit. The .DEP file is a pointer to the rest of the resources for DEdit and includes some of the information about your game resources. The rest of your game’s files exist in subdirectories of the directory where your .DEP file resides.

**Directories** — The subdirectories that contain your other game resources are a type of resource in themselves. The structure of these directories defines the tree views you see in many of the tabs in DEdit’s Project window. If you find a game’s .DEP file and look at the subdirectories in the same folder with it, you’ll see names such as TEXTURES, WORLDS, SOUNDS, and MODELS. These folders contain whatever resource they’re named for, so if you want to add new textures to a game or copy a world from one game to another, you should look in the directories named Textures and Worlds , respectively.

**Worlds** — Worlds come in two forms: .LTA files and .DAT files*. If you think of worlds as programs, the .lta file is the source code: Editable and understandable by the user and DEdit, but not executable. The .DAT file is like an actual program: it can be run in the game, but since it’s been “compiled” ( processed , in this case), the user can no longer modify it. The .lta files are what you change and save changes to inside of DEdit, and the .DAT file is the output of Processor.exe, which prepares your world to run in the game and optimizes its performance.

*.LTA files can also be saved as .LTC and .TBW files. .LTC files simply .LTA files that have been compressed. .TBW files are a binary representation of the .LTA file. .TBW files load and process faster than .LTAs or .LTCs, so you’ll probably want to save your worlds as .TBW files in most cases.

**Textures** — LithTech uses its own form of texture, the .DTX file. Textures can be up to 32-bit images, although you can obviously choose to make lower-color textures. The .DTX files also contain flags for additional information used by the engine and the game. You can convert .PCX and .TGA files into .DTX files by importing them inside of DEdit.

**Sprites** — Sprites (.SPR files) consist of a series of .DTX files linked together as an animation with a set frame rate. They’re commonly used for animations and special effects such as smoke, bullet holes, and liquid droplets.

**Sounds** — LithTech supports standard .WAV files directly with no custom modifications.

**Models** — Models in LithTech are in a custom format, the .LTB file. This contains the mesh/geometry for the model and other information used by the game engine. You create these files in an external editor such as Maya or 3D Studio Max, then save them in the .LTB file format using a plug-in. Use ModelEdit , to modify files in the .ltc format once they’ve been created.

**Objects** — Also known as Entities , these are objects that programmers construct using code. Some of this code exists in the engine and doesn’t appear in the project directories. However, many objects are created in code written for the specific game. These objects are called game objects (to distinguish them from the engine objects inside the engine code) and are stored in a file called OBJECT.LTO in the same directory as the project’s .DEP file.

**Prefabs** — A prefab is a collection of objects, both brushes and code objects that are stored in their own .ltc files (just like a regular game world) in a separate set of directories. Anything you make in a level can be exported as a prefab to make it easier to re-use later. Examples are benches, camera systems, hallways, doorways, and statues. Prefabs can be useful if your group needs a way to distribute standard-looking objects to its members.

Before you can begin creating levels, you must first load the Nolf 2 project file. To do this, just follow these steps:

1. From the **File** menu, select **Open Project** .

2. Browse to the **Game** subfolder of your Nolf 2 installation folder (i.e. C:\Program Files\Fox\No One Lives Forever 2)

3. Select the **TO2.dep** file.

4. Click on **Open** .

If the Game subfolder or the To2.dep file do not exist, run the unrez.bat file located in the Tools\Bin folder to unpack the Nolf 2 resources.

Next, you should make sure that the project paths are set correctly so that you can run your levels directly from the editor. To view the current settings:

1. From the **Edit** menu, select **Options** . This will bring up the DEdit options menu.

2. Click on the **Run** Tab.

The default values are as follows:

Executable: **LithTech.exe**

Working Directory: **..**

Program arguments: **-rez engine.rez -rez Game +runworld "%WorldName%"**

The default values should be left alone in most cases. However, if you wish to have access to the console when running your levels through DEdit, change your Executable to LithTechDev.exe. Note that this executable has been provided for development use only and can only be used in single-player mode to avoid possible exploits in multiplayer games. Also note that selecting the executable with the browse button will copy it’s entire path to the field. This is normal, but not necessary as the working folder field also determines where the file can be found.

If you have installed any previous version of DEdit on your machine, it’s likely that the old values are still contained in the registry. In this case, you must change the paths before attempting to run your level through the editor. Also, after changing these values you should always exit DEdit and restart to ensure that the changes have taken effect.

Once you have DEdit working with the game you can adjust the preferences to suite your needs. These are also located in the DEdit options menu, which can be found by selecting **Edit/Options** from the top of the editor. The editor works fine as is, and changes are only recommended if you are having performance problems, or for advanced users who want to adjust their settings.

For better performance you can lower the **Number of Undos** stored, which can be found under the **miscellaneous** tab.

Lowering the **Default far Z** setting under the Viewport tab also has performance benefits. This is the distance the editor sees in the 3D window, the value is in units. This is best left alone if you aren’t working on a large and complex level.

Most of the other settings in the DEdit options menu are for preference.

There is also a list of key bindings with options to change them. This can be found by selecting **Edit/Edit Key Configuration** from the top of the editor.

![DEdit002](images/DEdit002.jpg)

The callouts in this screenshot illustrate the various sections of DEdit’s UI. Use the buttons in the **Toolbars** to make new worlds, switch modes, and run your world. You can learn an individual button’s function by hovering your mouse over it to get a Tool Tip.

In the **Project Window** , DEdit gives you access to all of the resources in the game. Most tabs represent a resource you can add to the game. There are two special ones ( **Properties** and **Nodes** ) that relate to objects inside your maps. We’ll discuss all of these in a later section and they’re documented in the *DEdit Toolbars* chapter as well.

There are four **viewports** that provide windows onto the world you’re building. Each one presents a different view of the world. The upper left window shows you a Perspective view shot from a movable camera point in the level. The other three views have a fixed-view camera that displays either Top, Front or Left view (going in clockwise order). You’ll spend a lot of time working with these views.

In the **Status Bar** , DEdit provides information about the level or about the view you’re currently in. We’ll get into the depths of the user interface in later chapters, although you’re welcome to stop and explore if you’d like. Use the Tool Tips and the Status Bar to learn more about what the controls do.

This will be a simple tutorial on building a basic room using the tools supplied with DEdit. Further detail and explanations of the elements can be found after the tutorial section.

Select the **Worlds** tab on the left side of the editor in the **Project Window** and highlight the **Worlds** folder. From the toolbar at the top of the editor press the **New World** button. Name the new world ***Test_1*** .

DEdit is divided by four viewports to work in. You can adjust the grid size in each view by holding the mouse cursor over it and pressing the **+** and **–** keys. The grid size is indicated on the bottom of the editor on the **status bar** . Keep the grid size at 64 units for now. Using the viewport on the top right of the editor. Move your mouse cursor to the top left corner of it and hit the **spacebar** once. This should have placed a point on the grid and left you with a line that is connected to the point and your cursor (Figure 1.). You can hit the **backspace** key at anytime in this process to remove the last point.

![DEdit003](images/DEdit003.jpg) Figure 1.

Now move the mouse cursor to the top right corner of the viewport and hit the **spacebar** again. You should now have a straight line that draws across the top of the viewport with a point still connected to the cursor. Do this again in the bottom right corner, bottom left corner, and then over the first point you made to make a square. This should conclude your square and a new brush dialog window should pop up asking for a thickness value to make it a cube, 256 units is fine for now. You should now have a cube of some sort that is visible in all viewports (Figure 2.).

![DEdit004](images/DEdit004.jpg) Figure 2.

Holding your cursor over the top right viewport, try holding the **O** or **I** key and move your cursor around. The **O** key will zoom your view in and out (your mouse wheel will also do this), while the **I** key moves your view along the plane. All three 2D viewports work like this. Move your cursor to the top left viewport, which is your 3D or perspective view. In this view hold down the **O** key and move your mouse around, this pivots the view from the point where your camera or view position is. If you hold down the **O** key and press the left or right mouse buttons it will zoom your view in and out. Holding down the **I** key in this view will allow the mouse to move along a plane, combined with pressing your right mouse button will move it vertically. The **U** key will deselect an object; you can simply click on the object with your mouse to select it again. With the brush selected you will notice it has handles on the corners, along the edges, and in the center in your 2D views. These are for sizing and positioning the brush. In the bottom right corner of the editor on the **status bar** there is a readout for the dimensions of the selected brush. By selecting the handles and stretching them in the different 2D views, make the brush measure 512x256x512. On the left portion of the editor in the **project window** there is a selection of tabs. Select the **textures** tab and pick a texture to place on the brush. Select the folder labeled Siberia and scroll down to the texture named SWSib030 and select it. The texture should now show up in a window just below the selection menu. With the texture and the brush selected, press the **Apply Texture** button on the top toolbar to add this texture to the brush. With the brush still selected hit the **F** key to flip the normals on the brush. This turns the brush inside out basically so that there is now an interior space.

With the brush still selected press the **Marker to Selection** button, and then the **Center View on Marker** button. This should position your view on the space you created. Right click in one of the viewports and select **Add/Object** , This will bring up a **Select Object Type** window. From the **Class Types** menu select **GameStartPoint** and then select ok, this adds the starting point from where you enter the level when in the game, this is an **object** .

There are three modes for selecting and working in DEdit: **Brush Edit** , **Geometry Edit** , and **Object Edit** . You will need to press the appropriate button on the top toolbar for which mode you need to be in if you deselect your object at this point. Notice that when adding new objects they appear in the middle of the marker (the big green crosshair looking thing). You can move the marker in the 2D views by holding the **X** key and moving your cursor, or if you have something selected and you can press the **Marker to Selection** button to center up on it. At this point if you select the **Nodes** tab in the **project window** , you will notice you have two items in your node tree now. You can select from this list no matter what mode you are in. The node tree is a means of organizing your level in a manor that will make it easier to work on, as it grows larger in size and complexity. With the **GameStartPoint** object selected, move your cursor to one of the bottom viewports and press your **down arrow** key once.

In your top view using the **right arrow** key move it two spaces to the right. This will move the selected object one grid space down, which should leave it 64 units (one grid space) above the floor. The arrow keys are an optional way to move items in the editor. With the marker still centered on the brush right click on one of the viewports again and select **Add/Object** again. This time select the **WorldProperties** object from the **ClassTypes** window. The level will now run, but needs a **light** object placed in it or it will too dark to see anything. With the marker still centered on the brush, right click any viewport and select **Add/Object** again. From the **ClassTypes** window select the **light** object to add a light. Using the **up arrow** key in one of the bottom viewports, move the light up one grid space. It should now be one grid space from the top. What you should now see is a new box above the old one that is surrounded by a large sphere. The sphere is the radius within the level that the light will fill. Go to the **Properties** tab in the **project window** and look at the properties of the light. In most cases and entity’s properties are the most important tool used to control its behavior. In the case of lights, this is where you can change their size, brightness and color. The light’s current size (set in the LightRadius property) is 300. That’s probably a little small, so change the value to 600. In the viewports you’ll see the size of the light radius increase as well. Now it’s large enough to make a good-sized pool of light around the player. Now is a good time to save your level by pressing the **Save Project** button on the top toolbar. It’s a good idea to save your progress often when working on levels. The level is now ready to process and run. Press the **Process World** button on the top toolbar, when the process window pops up select the **Process** button and press the **Close** button when it’s done. To run the world, press the **Run World** button on the top toolbar.

This tutorial will guide you through the process of adding a second room to your level. This exercise requires that your grid size be set to 64 units in all your viewports.

Select your original brush you created in the editor either in the node tree or by left mouse clicking over it in one of the views while in **Brush Edit Mode** (found on the top toolbar). Select the **Nodes** tab in the **project window** , right click the top folder ( ***Test_1*** ) and select **Add Container Node** . This will create a new folder in the node tree. Name the new folder ***Room_1*** . You can name/rename a folder or item at any time by selecting it in the node tree and pressing **F2** or right click the folder and select **Rename** . With your brush selected right click the new folder ( ***Room_1*** ) and select **Move Tagged Nodes Here** . This will move your brush into it’s own folder to make it easier to work with. Do the same with the **light** object you added to place it in the ***Room_1*** folder.

Center the marker on the geometry that makes up the room. In the perspective you will need to position your view to the interior space of the brush. You will need to be in **Brush Edit Mode** (top toolbar) to work with the brush and the polygons that make up the brush. With the brush selected press **Ctrl + J** to disconnect the polygons that make up the brush. This should leave you with six individual polygons. In the 3D viewport select the wall on the right side of the room. If your not sure which one it is, keep selecting them until you see the line on the right side of your top right (top view) viewport highlighted with handles on it. With your wall (polygon) selected move to your cursor to the bottom left (side view) viewport. Move your cursor to the top of the polygon and one grid space left of center. Press the **spacebar** and it should create a point on the grid one space left of center. Move your cursor (making a straight line) to the bottom of the polygon and press the **spacebar** again. You should now have a straight line that follows one space left of center down your polygon. Press the **S** key to split the polygon. This is called a two-point split. You should now have a split down the left side of the polygon. In the 3D view select the polygon to the right (the right half of the wall you just split) of the split. With the polygon selected move the cursor back down to the bottom left (side view) viewport and make a split one grid space right of center (two spaces right of the first split) the same way you did the first one. This should leave your wall in three pieces (polygons). In your 3D view select the middle polygon of the wall and move your cursor back to the bottom left (side view) viewport. Your polygon should be two grid spaces wide and the full height of the wall. Grab the **handle** on the bottom center of the polygon by holding the left mouse button down on it and raise it up three grid spaces. There should now be an opening in the wall (Figure 3. shows 3D and side view).

![DEdit005](images/DEdit005.jpg) ![DEdit006](images/DEdit006.jpg) Figure 3.

In your 3D view select all three of the polygons that make up the wall. You will need to hold down the **Ctrl** key while left mouse clicking each polygon. Holding down the **Ctrl** key while selecting allows you to select multiple items whether they are brushes, polygons, or objects. With all three polygons selected press **Shift + J** to connect or join them. You can now select anywhere on the wall and it will select the entire wall. With the entire wall selected move your cursor to the bottom left (side view) viewport and make a horizontal split across the entire wall that runs along the top of the opening you made (two grid spaces down from the top). You can do this the same way you made the vertical splits to create the opening. In your 3D view select all the polygons that make up the wall and join them again by pressing **Shift + J** . At this point the wall should be made up of five polygons that are joined (Figure 4.).

![DEdit007](images/DEdit007.jpg) Figure 4.

In the 3D view select the wall again, the whole wall should select with one click since the polygons were joined. You will need to be in **Geometry Edit** mode for the next operation. With that wall selected press the **Geometry Edit** button on the top toolbar. Move the cursor to the bottom left (side view) viewport. The door opening is there but the geometry is incorrect. In **Geometry Edit** mode you will see at the corner of each polygon there is a little dot that highlights when you run the cursor past it, this is a vertex. For geometry to clean, a vertex should always meet up with another vertex or be on a corner. If it sits an edge instead of another vertex, it creates what is called a **t-junction** and while the level processes, it will try to fix these on its own. It is better to build clean and avoid making the processor make the decisions on how to cut up the geometry for you. You will also get better lighting results if you build clean. With the wall selected and in **Geometry Edit** mode, in the bottom left (side view) viewport move the cursor over the vertex that is not in a corner on the left side of the wall (you should see it highlight). Hold down the **M** key and the left mouse button and drag the vertex up to meet with the one in the top left corner. Now using the same technique grab the top left vertex that meets the ceiling above the door and move it to meet up with the one in the far left upper corner (Figure 5.).

![DEdit008](images/DEdit008.jpg) ![DEdit009](images/DEdit009.jpg) Figure 5.

Do the same thing for the ones on the right side, dragging them to the top right corner. The geometry around the door is now clean. The floor isn’t, but we won’t worry about it for now. At this point you can select all the walls in the room and join them using **Shift + J** to keep things manageable. You will need to be in **Brush Edit** (top toolbar) mode to select and join them.

We will now add a hallway. In the **project window** select the Room_1 folder in the node tree from the **Nodes** tab to highlight the room and press the **Marker to Selection** button on the top toolbar. This should center the marker on your room. Using the top right (top view) viewport zoom the view out (using the **O** key or mouse wheel) enough so that you could fit two rooms in the view. Using the same technique you used to create the first brush (Room_1), create a brush on the right side of the existing room that meets up with its edge and is centered. Make the brush two grid spaces wide and four grid spaces long (128 x 256). When the editor prompts you for the thickness after you connect the points to make the brush, 256 will work for now. You should now have a new brush that is highlighted, but doesn’t sit flush with the door opening. With the brush still selected, move the cursor to the bottom left (side view) viewport and drag the **handles** so that the new brush is the same size as your door opening. The brush will already have a texture on it since you selected a texture for the first room. At this point move your view out in your 3D window so that you can see the entire room and the hall (Figure 6.).

![DEdit010](images/DEdit010.jpg) ![DEdit011](images/DEdit011.jpg) Figure 6.

With the hall still selected, press the **semicolon** ( **;** ) key. This should have hidden everything except for the new brush you created since it was selected. To unhide all just press the **apostrophe** ( **’** ) key, but keep the other stuff hidden for now. With the hallway still selected press the **Center View** button on the top toolbar to center up your view on the piece you’re working on. Now press the **Geometry Edit** button on the top toolbar to go into geometry edit mode. In the 3D view, position yourself at either end of the hallway and hold the cursor over the polygon. You should see the edges of it highlight red when doing this. When all the edges around the polygon are highlighted red, press the **Page Down** button to delete it (Figure 7.).

![DEdit012](images/DEdit012.jpg) ![DEdit013](images/DEdit013.jpg) Figure 7.

You can hit **Ctrl + Z** at anytime to undo your last action, you can also select undo at the top of the editor with **Edit/Undo** . Delete the polygon at the other end of the hallway the same way. You will now need to go back into **Brush Edit** mode (top toolbar). Once back in **Brush Edit** mode, with the brush still selected press the **F** key to flip the normals (turn it inside out). You should now have a hallway that is open on both ends. Press the **apostrophe** ( **‘** )key to unhide the rest of the level. In your node tree make another container like you did for the room and name it ***Hallway*** . With the hallway selected right click on that folder and select **Move Tagged Nodes** **Here** to place the brush in that folder.

Select the hallway and press the **Marker to Selection** button (top toolbar) to center the marker on it. In the node tree select the entire ***Room_1*** folder, this should select all the geometry and the light object that make up the room. With the entire room selected go to the top of the editor and select **Edit/Copy** and then **Edit/Paste Alternate** . This will create a duplicate of that room sitting in the same world space as the original, folder and all. With the entire new room still selected move the cursor to the top right (top view) viewport. While holding down the **Ctrl** key press the **right arrow** key four times to rotate the new room into position. When you rotate items, the editor uses the **marker** center as the rotation center point. With the marker centered on the hallway the new room should rotate around it and sit right into the correct position. If things aren’t set up so handy, you can always rotate off any given point and manually move it into position by dragging it with the mouse, or nudging it with the arrow keys. Now in the node tree rename the new folder to ***Room_2*** by highlighting it and pressing **F2** , or by right clicking it and selecting to rename it. You should now have two rooms connected by a hallway. Save your work, process it, and run it.

Applying the proper textures to there surfaces is a key element in making a level feel like an actual place. This tutorial will guide you through some of the texturing basics in DEdit using the level you just created. It will also cover some basics in brush properties.

Select the ***Room_1*** folder from the node tree and press the **semicolon** ( **;** )key to hide the rest of the level. In the 3D viewport, move you camera view inside the room. You will need to be in **Brush Edit** mode (top toolbar) to start out. Inside the room, select the polygon that makes up the floor. Under the **properties** tab in the **project window** there should be some basic properties for this polygon. Select the dropdown for the lighting field and change it to lightmap. On larger polygons such as floors and ceilings changing the lighting to lightmaps will look better, but at a cost. Lightmapping is a performance hit to the engine and should be used sparingly. Select the polygons that make up the ceiling and walls, and do the same thing. Now select all of the walls that make up the room. At the bottom of the editor you will see the room size is 512x256x512. This means that your wall height is 256 units, and the SWSib030 texture that was applied to the room is 256x256 so it fits nicely. Right click in any of the viewports and select **Texture/Map Texture Coordinates.** This will bring up a new window that allows you to manipulate the texture size and position. The top portion of the window is for adjusting offsets. The wall texture should already fit correctly but feel free to adjust the offsets to see what they do. Just select cancel when you’re done so that the texture remains as it was. Press the **U** key to deselect any geometry and go into **Geometry Edit** mode (top toolbar). In the Siberia texture folder under the **Textures** tab in the **project window** , select the texture SFSib002. In your 3D viewport highlight the floor by moving the cursor over it, you will see the edges turn red. Press **Ctrl + T** while the polygon (floor) is highlighted to change the texture to the new texture. Do the same thing for the ceiling using the SFSib001 texture. You can view all the textures in a set by right clicking on the list and selecting **View Texture Palette** .

Tip: In **Geometry Edit** mode you can highlight a texture on a surface by holding the cursor over it and press the **K** key to have the editor align it for you. You may have to press it a few times since it lines the texture per edge and may not pick the edge you want to use first try. You can also press **Shift + C** to have it fit the texture to a surface. Note that this will stretch the texture to fit and it may need to be manually adjusted in the **Map Texture Coordinates** window to adjust it to look proper.

Prefabs are pre-assembled sets of geometry and sometimes include **objects** such as **Lights** or **worldmodels** . Prefabs are a quick way to bring a level to life if they are already made. They are a very efficient way to build for items that are going to be used more that once. Also, you can make changes to a prefab on it’s own, and it will update the changes across the level/levels globally for that prefab the next time the level is loaded in th4e editor.

Start with the existing ***Test_1*** level. Select ***Room_1*** from the node tree and hide everything else. Select the **light** object that you already added to the room from the node tree. Under the Properties tab in the **project window** , change the objects **BrightScale** field from 1.0, to 0.2. Since the prefab light prefabs you are about to add already have light objects in them, this will change this light objects value to make it dimmer. The **Light** objects are used primarily as fill or ambient light. Add a container node in the ***Room_1*** folder and name it ***Prefabs*** . If you go to the node tree and highlight the new ***Prefabs*** folder and press **F3** , it will make this folder the parent folder. The prefabs you add will now automatically be placed in that folder. In **Brush Edit** mode select the polygon that makes up the ceiling and press the **Marker to Selection** button. Now go to the **Prefabs** tab in the **project window** and select the Siberia folder. Scroll down to *Light_Flourescent_Basket_On_96x9x16* and double click on it from the list to add it to the level. You will need to be in **Object Edit** mode to select prefabs with the mouse in the editor. You can select anything from the node tree no matter what editing mode you are in. In your top view move the light two grid spaces with the **down arrow** key. Add another light prefab and move it two grid spaces with the **up arrow** key to give you two lights place appropriately on the ceiling. Now select the polygon that makes up the floor and select **Marker to Selection** to place the marker on it. Scroll and select a desk in the Siberia prefabs folder and double click on it to add it. In the top view viewport rotate the desk with **Ctrl + right arrow** key to make it facing the doorway. In the same viewport nudge it with the arrow keys to place it in the center of the room. Now add a chair from the Siberia prefabs folder and position it behind the desk. You should have a general idea how the prefabs are used and you can add whatever prefabs you choose to furnish the area at this point. Some prefabs have objects in them to allow the AI to interact with them in game. If you place these and don’t have AI volumes in yet you will get runtime errors in game, but the level will still run.

Tip: To learn more about how things are set up in the game you can right click on a prefab from the prefabs list and select to open it. With the prefab open, you can inspect values and how switches and such are set up. It is advised not to save any changes when you close the prefab or elements of the game may not work properly anymore.

We will now add a window to the room. You will need to select and explode (disconnect) the walls using **Ctrl + J** . With all the walls still highlighted hold down the **Ctrl** key and left mouse click on the wall to the rear of the desk (opposite of the doorway), this should deselect this polygon. Now press **Shift + J** to rejoin the remaining walls. Select your ***Prefabs*** folder you added to ***Room_1*** in the node tree and the with the cursor over a viewport, press the **Start Bracket** ( **[** ) key (the **End Bracket** ( **]** ) key will unhide a selected item) to hide them for now and the **U** to deselect them. Hiding and unhiding your work makes it easier to see what you are doing when working in the viewports. Select your back wall where you are going to add your window to highlight it and select **Marker to Selection** to center the marker on it. Under the **prefabs** tab in the **project window** , select the Siberia folder and scroll down to the *Window_02_104x56x8* prefab. Double mouse click the window prefab from the list to add it. You will need to move the window into position using you top and side view viewports. You will need to adjust your grid size in these viewports to get the selection on center and flush with the wall. In the top view there should be a 2 unit overhang on the interior side of the window. In the side view, position the window so that it is about centered with the door opening space. Using the techniques learned to add the doorway, cut up the wall behind the desk (using two point splits) to make a hole in the wall to place a window. You should be able to adjust your grid size, and simply make your splits by selecting the wall and following the outline of the window prefab (one edge at a time). Make your first split vertically down the left side of the window. Select the polygon on the right and make a split vertically down the right side of the window. The wall should now be made up of three polygons. Select all three by holding down the **Ctrl** key and mouse clicking on them in the 3D view. Now join them by pressing **Shift + J** . Make two more splits, one above and one bellow the window, again following the outline of the window. Select all the polygons that make up the wall and join them again using **Shift + J** . With the wall still selected go into **Geometry Edit** mode on the top toolbar. In the 3D view, hold the cursor over the polygon that covers the window to highlight it and press the **Page Down** key to delete it. At this point you may use the technique to clean up the t-junctions covered in the tutorial to make the doorway if you choose. You should now have a window in the wall that isn’t covered by a polygon.

This will be a simple tutorial on adding a skybox to your level. We will be using the ***Test_1*** level for this exercise. Set the grid size to 64 in your 2D views.

Holding the cursor over any viewport press the **apostrophe** ( **’** ) key to unhide all of your work. You will need to be in **Brush Edit** mode for the next step. In your node tree, select the top folder and add a new container to it. Name this container *Sky* and press **F3** with the new folder highlighted in the node tree to make it the active parent folder. In the top view viewport, using the **spacebar** make a box around the level that has a one unit space between it and the rooms all the way around. When you complete the box and it prompts you for a thickness, 256 units will work for now. Position and size your brush so that there is a one-unit space between it and the rooms in your side view viewport (Figure 8.). You will now need to flip the normals on the brush by pressing the **F** key while it is selected to change it into an interior space. Your rooms should now be sitting inside of the new brush. With the new brush selected go to the textures tab in the **project window** . Highlight the main texture folder and select the *Sky* texture, press the **Apply Texture** button on the top toolbar to give your brush the new texture. Now you will need to go to the **Properties** tab in the **project window** and change the brush **Type** from **Normal** to **SkyPortal** using the dropdown. This flags the selected item to use the information from a **Skybox** that we are about to add.

![DEdit014](images/DEdit014.jpg) Figure 8.

In the top view viewport zoom your view out a bit using the **O** key or the mouse wheel. Move your marker using the **X** key so that it is positioned outside of your level (the rooms). From the **Prefabs** tab in the **project window** , select the Siberia folder and scroll to select and add the *Sky_Night* prefab. After you add it, if it’s not outside the walls of your level, just move it so it is (Figure 8.). If you process and run the level now you should be able to see the night sky through the window, this particular sky doesn’t have any clouds in it. Feel free to try other skies out of different prefab folders to see what they look like.

This tutorial will guide you through the basics of creating an outdoor area and run you through some of the effects used in these areas.

Select the Worlds tab on the left side of the editor and highlight the Worlds folder. From the toolbar at the top of the level press the **New World** button. Name the world ***Test_2*** .

In your top view, right click and select Add/Box. For the Thickness field select 1024. This should have created a large box that will be used as an outdoor area. Zoom out in all of your 2D views so that the entire box is visible in each of them. In **Brush Edit** mode with the cursor over any viewport press the **F** key to flip the normals and create an interior space. Under the Textures tab in the **project window** select the Sky texture from the main folder and with the **Apply Texture** button on the top toolbar apply this texture to the new brush. In the **Properties** tab with the brush selected change the **Type** field to SkyPortal with the dropdown menu. Under the **Prefabs** tab in the **project window** , select the global folder and add the Sky02 prefab to the level. In your top right (top view) viewport move the prefab outside of the room by grabbing the handle in the middle and dragging the selection.

Right click any viewport and select **Add/Object** , choose and add the **WorldProperties** object from the Class Types window. Add a **GameStartPoint** object using the same technique and lower it a couple grid spaces so it isn’t in the same space as the last object added. Now add a **StaticSunlight** object the same way. Raise your **StaticSunlight** object near the top of the ceiling, and press the **Marker to Selection** button on the top toolbar to center the marker on it. Press the **Center View** button on the top toolbar with the **StaticSunlight** object selected to center the view on it. In the bottom left (side view) viewport zoom your view out a little so that you can see the whole **StaticSunlight** object. Rotate the object by holding down the **Ctrl** key and pressing the **left arrow** key so that the blue vector (the blue line on the object) is pointing down. This will make the sunlight shine straight down.

In the 3D view select the brush and explode it using **Ctrl + J** , holding the **Ctrl** key, left mouse click the floor to deselect it and rejoin the remaining polygons by using **Shift + J** . Select the polygon that makes up the floor and go to the properties tab and change it’s **Type** to normal and it’s **Lightning** field to Lightmap. Under the **Textures** tab select the TFJp009 texture from the Japan folder and apply it to the floor polygon using the **Apply Texture** button on the top toolbar. You should now have an outdoor level that is ready to run. You may process it and run it to take a look at this point if you wish. Note that the sky won’t mate up with the ground due to the bottom polygon of the skybox prefab not having a texture on it. Most of the skyboxes are made this way for performance benefits, since there is usually a fence, mountain or building to break the ground plane and you would never see the bottom of it anyway.

To add an effect such as grass you need to place a **scatter volume** . In one of the viewports right mouse click and select **Add/Object** . From the **Class Types** menu open the **VolumeEffect** folder and add the **ScatterVolume** object from that folder. Although it may look like a brush in the editor, you will need to be in **Object Edit** mode to scale the object’s proportions. It is advised to move these manually with the mouse and the object’s handles, and not to try to rotate them. **/Grass** folder and select the grass2.dtx for the texture to use. Now move the volume down to rest on the ground plane and move it near a corner. The volume will put grass on any texture it touches unless you specify the only texture you want it on in the **PlacementTexture** field under the **Properties** tab. The level is ready to process and run to see the grass that’s been added. Don’t try to add grass for hiding or cover, it is a volume effect and these can be turned off in game.

Snow is added to a level by placing a snow volume. In one of the viewports right mouse click and select **Add/Object** . From the **Class Types** menu open the **VolumeEffect** and add the **SnowVolume** object. Although it may look like a brush in the editor, you will need to be in **Object Edit** mode to scale the object’s proportions. It is advised to move these manually with the mouse and the object’s handles, and not to try to rotate them. The volume now needs a texture to specify what it is. With the volume selected, go to the properties tab on the left side of the editor. In the **TextureName** field select the browse button to add a texture. Browse to the **TexFX/Snow** and select to use Snowflake1.dtx. Now stretch the volume so that it meets the ground and is about 512 units tall or so. The level is now ready to process and run to see the snow you just added. Snow can be blocked from entering interior spaces such as buildings by adding a polygon with the **Type** field set to ParticleBlocker sitting where you want the snow to stop. A quick way to do this is to just copy the roof and set the new roof with the brush **Type** set to ParticleBlocker.

The Nolf 2 AI systems are highly advanced and rather complex. Adding a complete set of AI that will behave in a realistic fashion under all conditions is beyond the scope of this document. However, the basics of adding AI are simple. This section will show you how to add a single patrolling AI that will attack when it sees the player.

First, load the Test_01 world, and then save it as Test_03 . Then, select Room_2 from the node tree and hide everything else. Next, add an AIRegion object and place it somewhere in the room. It’s exact location is not important. Now add an AIVolume object at the center of the room, and expand it’s size until it almost fills the horizontal dimensions of the room without actually intersecting with any walls. Note that the AI use these Volumes to determine where they are allowed to go, so AI volumes that intersect with walls can allow the AI to walk right through. When done, click on the properties tab, and type AIRegion0 in the Region field.

Now that the volume is placed, add 2 AINodePatrol objects to the level and place them at opposite ends of the room. Make sure that the nodes are positioned within both the horizontal and vertical boundaries of the Volume, or the AI will not be able to reach them. At this point, you must modify the Next property of each node so that they point to each other (i.e. AINodePatrol0 points to AINodePatrol1 and vice versa) .

Now that the AI environment has been established, it’s time to add an AI. From the World menu, select Add Object , then click on CAI from the object menu, and then select CAIHuman . Make sure that the AI is placed somewhere within the horizontal boundary of the AIVolume, or it will not be able to move when you run your world. When it’s in position, click on the Properties tab. For ModelTemplate, type in or select HarmGuardPurple. For GoalSet , type in or select Patrol . Finally, Next, click on the Attachments property, and select Sterling from the RightHand field. When done, click on OK to close the attachments window.

To learn more about working with AI, see the **NOLF2 AI** and **Nolf 2 AI Gameplay Setup** sections of the Nolf 2 help file.

The *Doomsday* mode of play will be briefly covered in this section for creating team based levels. Doomsday levels are very similar to standard CTF (Capture The Flag) levels as far as the layout goes. The level should consist of two bases that are identical or equally balanced in their design. Multiplayer levels require more **GameStartPoints** , and the *Team* field in the **objects** property must be set to specify which team will use that **GameStartPoint** . Team0 is for the blue team and Team1 is for red.

Below the team fields are two selections for *StartPoint* and *SpawnPoint* . Setting *StartPoint* to true will use this object as a **GameStartPoint** , a player will enter the level at this point when the level loads. Setting the *SpawnPoint* to true will use the object as a spawn point, the player will respawn (appear there) after being killed. With both fields set to true, the object will be used as both. Generally the **GameStartPoints** (8 or more) are set in close proximity to each other near the Doomsday device in each base with the *StartPoint* and *SpawnPoint* set to true. The **GameStartPoints** with only the *SpawnPoint* set to true are usually placed around that teams base in areas where it would be safe to respawn and less likely to be instantly confronted by the opposing team.

The Doomsday bases and pieces are simple to add, as they are available as prefabs in the Global directory of the Prefabs tab in the **Project Window** . The **Doomsday_Target** prefab goes in the blue base and the **Doomsday_Target2** goes in the red base. The pieces needed to assemble the Doomsday device are the core, transmitter, and the batteries, they are also prefabs and can found in the same folder as the bases. Each level only needs one of each piece placed in it. The core is generally placed in the center of the level making it equally accessible to both teams. The transmitter is placed in one base and the batteries in the other. Note when placing the items and start points, that they should be in the same position in either base to keep the two sides equal. The same rule applies for placing weapon and gear items in the level. Also, you may notice that the Doomsday bases and pieces will not appear in your levels when you run them through DEdit. This is intentional, since Doomsday levels are also available in Deathmatch modes.

In order for the game to recognize your multiplayer levels, they must be named for the game mode they were designed for, and their **.dat** files placed in the **Game\Worlds\RetailMultiplayer** folder of your .rez file. For Deathmatch/Team Deathmatch only levels, add the prefix “ **DM_** ” to the level game, e.g. “DM_Test01.ltc”. For Doomsday/Deathmatch/Team Deathmatch levels, use the “ **DD_** ” prefix. Cooperative levels do not necessarily require a prefix, but must be set up properly in the **game/attreibtues/coopmissions.txt** file before they will be recognized by the game.

For more information about setting up cooperative missions, and creating .rez files to distribute your levels, please refer to the NOLF2 Contentpacks and Modifications section of the NOLF2 Tools and Source Code Help file.

The N.O.L.F. universe tries to create a believable environment with objects and structures that are in a realistic scale. The tutorials aren’t necessarily to scale for simplicity of building and learning. Below is a list of scale standards used to create a realistic environment in the Jupiter engine. Wall thickness in general should be 16 units.

For some of these, the ideal height wasn't a multiple of 16, so I gave the closest multiple of 16 and a more ideal multiple of 8 or 4.

Doorknob Height 48 (56 ideal)

Door Height 128

Door Width 64 (not including frame)

Door Thickness 4

Table Height 48

Bar Height 64

Wall Switch Height 64 (72 ideal)

Chair seat Height 32

Chair Depth 24

Chair Back Height 64 (up to the shoulders

80 (just above top of head)

Minimum Crouch Height 64

Stair Height 16

Stair Depth 24

Handrail Diameter 4

Handrail Height 56

A property you may want to modify is the light’s color. To change the colors, click on the color sample button next to the property name. Start by clicking the white button (LightColor). The dialog that comes up is a standard color picker dialog, and it allows you to pick from a standard palette or create your own custom colors. Choose one of the very light blue colors for something similar to a fluorescent light. You can use the slider on the far right to lighten or darken the color to your taste. When you’re done, close the dialog and you’ll see your new color in place on the LightColor button. Lastly, you can set the brightness of the light using the BrightScale property. At its default setting of 1.0, the light appears at a normal brightness. If you change the value of BrightScale to 0.5, the light’s brightness is halved. However, the radius stays the same. Thus, you can create a very large light that doesn’t overwhelm the area closest to its center. Likewise, if you want an intensely bright light, you can increase the BrightScale value to 2.0, which will make the light much brighter. For now, leave BrightScale as it is.

There is another useful type of light with very different behavior from the regular one: The DirLight. While a normal light throws light in a sphere all the way around it, a DirLight acts like a spotlight: It throws light in a cone, the diameter of which you can control.

A DirLight is a directional or spotlight. You can aim a Dirlight using the object’s Rotation property. Click the button next to the property’s name and you’ll see a dialog appear. Within this dialog, you can control every aspect of the object’s facing. Each of the three aspects has a range between 0 and 359. Yaw controls the horizontal facing of the object, and is aligned identically to the Top viewport like a compass needle. You can use the preview display at the top of the dialog to see how the results will appear. A setting of 0 points the object straight “north,” towards the top edge of the Top viewport. A setting of 90 would aim “east,” a setting of 135 would point “southeast” towards the lower right corner of the viewport and so on. For now, set the yaw to 180 to spin the Dirlight around so it’s facing the opposite direction.

Pitch controls the vertical angle of the object. The Pitch preview display shows the result of your changes. Since the Dirlight is pointed at the proper angle already, there’s no need to change this.

The Roll control controls the spin of the object. This is useful mainly for props or cameras, where you want the object to bank or its viewpoint to sway. You would change a motorcycle’s Roll, for example, if you wanted it to lean as it turned a sharp corner. Again, there’s no need to change this value in the case of a Dirlight.

You should also increase the LightRadius of the light to 600 to extend the reach of the light a little further.

You can add an overall ambient light value to your entire level. In the editor press **Ctrl + W** to bring up your **World Info** window. Enter AmbientLight R G B in the field with the R G B being light values for Red, Blue, and Green. An example for this would be AmbientLight 12 12 12. This would give the level a dim overall lighting with white light since the RGB values are all equal. It isn’t recommended to light the entire level like this without using the light objects. The world ambient lighting does not cast shadows and will give the level a flat overall look when used on it’s own.

With a brush or polygon selected, you can change the way it is effected by lights in two ways. In the **Lighting** field generally **Lightmap** or **Gouraud** will be used for the basic lighting style. Gouraud lighting takes the light sample from the vertices to light the brush. This is the preferred method to light the majority of your world. On larger brushes or where a vertex meets an edge the results may not look very good. Keep in mind where your vertices are when placing lights in your level, and try to place the light source near them. Lightmapping creates better looking results on larger planes, but at a cost to perfomance. When a polygons is set to **Lightmap** you can optionally change the lightmap grid size. This can be found in the **LightControl** field. By selecting it, it will open a new dialog with a field in it named **LMGridSize** . The default value for the field is 20 and the shadows become more defined as the variable is decreased. Note that halving the value makes a quadruple hit to the performance. It is recommended only to decrease the value in isolated instances. Generally a value between 6 and 10 will give you a pretty defined shadow where you feel it may be necessary.

To create glass, simply bind a brush with a glass texture to a WorldModel object and adjust a few fields under the Properties tab in the **Project Window.** Set the **DebrisType** to Window, the **SurfaceOverrride** to Glass, and the **BlendMode** to Translucent. The **Alpha** field dictates the opacity of your glass, with 1.0 being opaque, decreasing the value makes the glass more transparent. Generally the Alpha on glass is set to about 0.5.

An occluder is a plane with the brush Type set to Occluder. Occluders are most effective when they are axis aligned (not set at an angle), it is not recommended to place them otherwise. Occluders are placed to block the engine from drawing geometry that is not visible to the player, thus reducing the number of triangles draw by the engine. The geometry of a level is divided into renderblocks, with each renderblock contains 2,000 triangles. Any geometry that is associated with a worldmodel will draw it’s own renderblock regardless of the number of triangles within it. If a renderblock cannot be seen by the engine from the players perspective the geometry contained will not be drawn by the engine. When possible it is best to run them a good distance through the geometry if they lead to an area where the player couldn’t see in game anyways. This will assure they cover as many renderblocks as possible. Occluders do eat up resources at runtime, so the should be used sparingly and efficiently. Small occluders are not very effective since the majority of renderblocks are rather large and would not be hidden behind them. There are two types of occluders, dynamic and static.

**Static Occluders** - Static occluders are always on and occluding the geometry behind them. They are best suited placed in walls, ceilings, and other larger pieces of geometry which the player could not see through anyway. If a static occluder has bad placement it is most likely you will see geometry popping in and out when running the game.

**Dynamic Occluders** - Dynamic occluders are set-up to work in conjunction with a volume. When a player is in the volume the occluder is active, it becomes inactive when the player leaves the volume. The dynamic occluder is valuable to hide large sections of geometry when the player is in an area where the geometry is not visible anyway. To make a dynamic occluder volume you can just create a brush that you want to act as the volume. Center the marker on the brush and right click any viewport and select Add/Object, from the Class Types menu select and add the DynamicOccluderVolume object. Select the brush you created for the volume, and in the node tree place the brush under the . With the DynamicOccluderVolume object selected go to the Properties tab in the project window. Notice there are fields for occluder names. Enter the name of the occluder/occluders you want to be active when the player is in the volume in these fields. It is best to give the dynamic occluders special names to make them easier to keep track of when using them. You can rename them in the node tree, and example would be Dynamic_01.

Below is a list and basic description of game objects used in the creation of No One Lives Forever 2. If you have a question about the meaning of any of the available properties of an object, you may access the online help built into DEdit by placing your cursor over the property in question until the cursor is replaced by a question mark. Left click to display a definition of that property.

Volumes placed to send information to the AI when a player is within the boundaries.

Nodes placed to relay information or instructions to the AI.

Objects used to group the AI volumes into regions of a level. This divides the level into unique areas for the AI’s search behavior.

Volumes placed for areas the AI can travel in. Some have special attributes to inform the AI of actions to take while in the volume.

You can assign an ambient value to brushes that are placed under this object in the objects properties. Note that individual brush ambient values are ignored when under this object.

AmmoBoxes are placed in the world as a powerup. Each Ammobox can contain up to ten different kinds of ammunition.

This is the object used to place AI in a level.

Cameras show scenes in the world outside the player.

This is a controller object used for cut scenes and in game dialog.

Objects placed to execute, track and time a series of events and/or commands.

This object controls properties of up to 8 objects.

An object to place decal textures under, allowing textures with an alpha channel to be placed overlapping standard textures.

An object placed to give the player multiple choices they can make.

DemoSkyWorldModels allow objects to render in the skybox in a single step. A DemoSkyWorldModel is an object that fuses a WorldModel and a SkyPointer. By doing this, binding a brush to the one object allows it to be rendered in the skybox without the need for any additional objects.

An object placed to message dialogue for the AI to use.

DirLights act like a spotlight, shining only within an arc that you specify instead of in a sphere like a regular light. You can aim them to any angle you choose.

This is an incremental colored bar meter displayed on the screen. It is useful for “boss” fights.

This object displays a timer on the screen in game.

The object used to create a volume by placing a brush under it. When the player is in the volume, the occluders indicated in the volume will be active

This object will store up to 10 different "events", with each event containing an integer value and two commands. The idea is that the game code can increment/decrement the EventCounter's value (by sending ”Increment” or “Inc” and ”Decrement” or “Dec” messages). When the counter’s value is equal to one (or more) of the EventXValue (i.e., Event1Value, Event2Value, etc.), either the EventXIncToValCmd or EventXDecToValCmd will be processes. In other words, how the counter gets to the EventXValue determines which command is sent. For example, if Event1Value = 2, and the EventCounter’s staring value is 0, if the EventCounter gets 2 “Inc” messages, the Event1IncToValCmd will be processed. If at this point the “Inc” message is sent again (so the counter is now at 3), and then the “Dec” message is sent to the counter, the Event1DecToValCmd will be processed. This object also understands the “Lock” and “Unlock” commands (Inc/Dec don’t have any effect on the counter if it is locked).

This is an object used to place explosion effects in the world.

This is an object used to create fire effects.

This is the point that the player enters the game world.

This is an object used to place gear power up items in the world.

This is an object used when you wish to send the same message to several different objects at once. It acts as a simple relay.

This is an object used to define a point in the path of a keyframed object.

This is an object used to define a point in the path of a keyframed object.

This is a basic point light, or omni light object used to light the world.

This is an object used to place gear power up items in the world.

This is a light that only affects models.

ObjectRemover contains several "groups" of objects. For each group, you may list up to 10 objects. Specify how many groups of objects you wish to keep in the "GroupsToKeep" property.

On the first update, the ObjectRemover will randomly select the groups of objects it will keep (based on how many were specified to keep), and remove all the objects in all the other groups, and then remove itself.

Any time you want to spawn a large number of similar simple objects in one location or area, you probably want a ParticleSystem object. Particle systems create a cloud of objects, usually sprites or simple models. They can make the sprites move, determine the area where they appear and how long they remain after being created.

A polygrid is a grid of triangles that can have an animating surface. They’re used to simulate flags, curtains, water, force fields and many other effects.

The Prop object is used to place .ltb models into the game world. Props are typically things that would be too complex or impractical to be created from world geometry. Examples would be plants, telephones, detailed furnishings, etc.

This object is a subclass of the Prop object. It is used to add bits of information that the player can discover during the course of gameplay. These are typically in the form of letters, rolls of film, briefcases, etc. Since it is a subclass of the Prop object, it shares many of its properties.

This object is a subclass of the Prop object. This object is used to place PlayerVehicles in the world that the player can interact with. Since it is a subclass of the Prop object, it shares many of its properties.

This object is a subclass of the Prop object. This is a different way of managing prop placement in levels. We found that a lot of the props that we placed were set up the same as each other. Yet we still had to set all of the flags. The PropType object places props by way of a simple dropdown menu. The dropdown menu refers to a bute file where the all of the prop flags have been predefined. Since it is a subclass of the Prop object, it shares many of its properties.

Used to place a radar point on the compass.

This object is a subclass of the Prop object. In default mode works like a security camera (i.e., scans back and forth and it's yaw and fov can be adjusted). However, you can alternatively give it a Target object to follow (e.g., you can set up a keyframer and have the searchlight follow the keyframed object). Also there is a SpecialFXStuff property group that allows you to change the special fx (i.e., beam radius/alpha, dynamic light color/radius, and lensflare fx). Since it is a subclass of the Prop object, it shares many of its properties.

This object is a subclass of the Prop object. This object is used to place security cameras in the world. Since it is a subclass of the Prop object, it shares many of its properties.

The RandomSpawner is used to spawn objects randomly through multiple Spawner objects.

Items placed under this object can be triggered to hide and unhide from within a DynamicOccluderVolume.

These are objects that spin on any given axis. The most common example of a RotatingWorldModel would be a spinning fan.

ScaleSprites are free-standing textures that don’t need a surface to appear on. ScaleSprites get compounded into a lot of other game objects, but they can be used on their own to make a lot of things happen too. ScaleSprites are used for all kinds of things — halos around lights, floating symbols, decals on walls and objects in the sky.

The ScreenShake object shakes the camera when triggered.

SkyPointer objects allow the objects that they target to render in the skybox of the level. Only WorldModel-derived objects and Sprites can appear in the skybox.

This object allows you to place sounds in the world.

This is a generic object used to “Spawn” objects into the game world.

This object is used in conversational dialogues in a cinematic trigger. If a character needs to have a conversation with a non-AI object such as an intercom, this is the object that will fill the position of that AI in the conversation.

Placed in a level to give commands to objects within the level when the level is loaded.

The StaticSunLight object supplies levels that have a skybox with light from a sunlike source. The light radiates into the level through all skyportal brushes as if from an infinitely far point. This sunlight’s direction is determined by the rotation of the StaticSunLight object. Its position doesn’t matter, since the emitted light acts as if it comes from an infinite distance. The StaticSunlight’s position is ignored.

The Steam object is a form of the ParticleSystem object that has been set up to more easily create particle effects resembling jets of steam. The effect created by this object travels down the forward facing vector of the object.

This object is used to define the position and rotation of a point in space that the player or an AI can be moved to instantly.

The Transitional Area Mapping level-loading scheme, referred to as the “Trans. A.M”, is used to add the ability to travel from one level to the next, and back if you choose. To create a transition between levels you must first place a TransitionArea object in each level. The two TransintionAreas MUST have the same name and MUST have the same dimensions. If the TransitionArea in the first level is named TransAM01 the TransitionArea in the second level must also be named TransAM01. You can have multiple TransitionAreas in each level but for every TransitionArea in one level you must have a TransitionArea in the level you wish to transition to with the same name and same dimensions. Binding a TransitionArea object to a brush creates a TransitionArea. The volume contained by the TransitionArea holds the objects that will be transitioned between levels. If an ammo box is in the TransitionArea as you leave the first level it will be in the same position and rotation within the TransitionArea of the second level. The player’s position and rotation within the TransitionArea is also kept. To specify which level a TransitionArea is supposed to transition you to, enter the level number in the ‘TransitionToLevel’ property. This number corresponds to a LevelNumber in missions.txt. You can only create transitions between levels within the same mission, so if the ‘TransitionToLevel’ property is 1 then the level that this TransitionArea will load will be the level specified in the missions ‘Level1’ property. To trigger a transition from a TransitionArea simply send the TransitionArea a ‘TRANSITION’ message. You can send this message from a switch or even a trigger from within the TransitionArea. The player must be inside the TransitionArea in order for the transition to occur.

To better create the effect that the player never really left a level, the geometry and other objects surrounding the TransitionAreas in each level should match exactly. When creating a TransitionArea, keep it small and simple. Use areas such as a small room, hallway, stairwell or elevator as places to contain the TransitionArea. Try not to over populate the TransitionArea with a lot of objects. Certain objects will not transition even if they are inside the TransitionArea. All WorldModels and Triggers will not transition but they can be inside a TransitionArea during a transition.

Triggers are placed in a level to send messages or commands to other objects when a player or AI enters or passes through them.

This object is a subclass of the Trigger object. This object is used to trigger the end of a level.

Volume brushes are used for a number of effects — Water, damaging environments, ladders, and to relay physics instructions such as gravity changes to name a few. A VolumeBrush object is designed to bind to a brush and use the brush to determine its area of effect. If the effect is continuous, such as snow, it only occurs within the space defined by the brush. If the effect happens to players and AI’s, it only happens to them when they’re within the volume. The effects of the volume are triggered when the player enters the space and usually un-triggered when they leave.

Used to place ScatterVolumes (for grass) and SnowVolumes.

This is an object used to place Weapon power up items in the world.

The naming convention should be mentioned first. There are three basic types, WorldModels, Doors, and Switches. Each of these three basic types has different movement types as prefixes describing how they behave. “Rotating” means the objects will rotate around a point a specified number of degrees around each axis (much like the NOLF HingedDoor). “Sliding” objects will move a specified number of units in a specified direction (much like the NOLF Door), think of the behavior of a desk drawer. “Spinning” objects will spin around a point in a specified number of seconds on each axis (much like the NOLF RotatingWorldModel), think of a ceiling fans behavior. Each movement type has identical properties and behaves exactly the same so when you are learning how to use a RotatingWorldModel you are also learning the RotatingSwitch and RotatingDoor. However, even though a RotatingWorldModel can be used exactly as a RotatingDoor you should NOT put a RotatingWorldModel where a Door should go, and vice versa. Use a Door only for Doors, use Switches only for Switches, and WorldModels for everything else. Game objects, specifically AI and Players, need to know if they are interacting with a Door, Switch or something else.

Most basic functionality is shared for every new WorldModel object. All of the new objects have common features and properties that you can edit. They are all created the same way, they all move and rotate based on their local coordinate system and they can all receive certain messages. “Active” WorldModels, that is any Rotating, Sliding or Spinning objects, can also send commands to other objects and play sounds depending on what state they are in.

###### Creation

To create an instance of a WorldModel just bind a WorldModel object to a brush or a set of brushes. There are several property values you can edit to achieve the object you want. BlendModes is a property drop down list containing several blend operations for your WorldModel object. WorldModels can have Additive blending, they can be Chromakeyed, or they can be Translucent. None is the default BlendMode for newly created WorldModel objects. You can also edit several other properties such as visibility and solidity. If you have a fairly complex brush that the player will be walking on or moving around you may want to set the BoxPhysics flag to FALSE. You can override the surface flags set by the texture mapped to the brush(s) by simply selecting the desired surface in the SurfaceOverride property dropdown list.

Once a WorldModel is positioned and behaves as you would like you can rotate it by selecting both the object and all brushes it is bound to then select Rotate Object in the right click menu in DEdit. You can rotate the WorldModel on all axis, and in any direction. The WorldModel will now move or rotate with the same behavior around its own local coordinate system.

###### Damage

All WorldModels can handle damage. Each one has a subset property labeled DamageProperties. There are several different values and flags that can all be edited to define how the WorldModel behaves when damaged. Here is a list of the properties that are included in the DamageProperties subset and what each on means:

- HitPoints: Number of hit points the WorldModel has when created.
- MaxHitPoints: Max number of hit points the WorldModel can ever have.
- Armor: Amount of armor that the WorldModel has when it is created.
- MaxArmor: Max amount of armor the WorldModel can ever have.
- DamageTriggerCounter: How many times the object must be damaged before the damage message will be sent.
- DamageTriggerTarget : Name of the object that will receive the DamageTriggerMessage.
- DamageTriggerMessage: Command string that is sent when the WorldModel receives damage from any source.
- DamageTriggerNumSends: Specifies how many times the damage message will be sent.
- DamageMessage: Command string that is sent to the object that caused the damage.
- DeathTriggerTarget: Name of the object that will receive the DeathTriggerMessage.
- DeathTriggerMessage : Command string that is sent when the WorldModel has been destroyed.
- PlayerDeathTriggerTarget: Name of the object that receives the PlayerDeathTriggerMessage.
- PlayerDeathTriggerMessage: Command string that is sent when the player destroys the WorldModel.
- KillerMessage: Command string is sent to the object that destroys this WorldModel.
- CanHeal: Toggles whether the WorldModel can be healed.
- CanRepair: Toggles whether the WorldModel can be repaired.
- CanDamage: Toggles whether the WorldModel can be damaged.
- Mass: Sets the mass of the WorldModel within the game.
- NeverDestroy: Toggles whether the WorldModel can be destroyed.

###### Attachments

All WorldModels can have attachments (you can attach models, props, and other WorldModel objects) much like Doorknobs in the NOLF Doors. When attached to a WordlModel, objects will move and rotate with the WorldModel. To have an object attach to a WorldModel when the game loads, add the object you want to attach and position it in DEdit. Enter the name of the Object you want to attach in the Attachments property field, you can have as many objects attached to a WorldModel as you want. List all the objects you want attached separated by a semicolon (ex. Prop1; Prop2; SlidingWorldModel0). During runtime of the game you can attach and detach objects through messages.

###### States

All “Active” WorldModel objects (Rotating, Sliding, and Spinning) have different states they go through. These states are: PowerOn, On, PowerOff, Off. Doors have similar states with different names: Opening, Open, Closing, Closed. By default, this can be changed in the Options property subset, all objects start in the ‘Off’ or ‘Closed’ state. When positioning and rotating the object in DEdit you are setting its ‘Off’ position. By entering in values for the Movement or Rotation properties you are setting how and where the object will move to when fully ‘On’ or ‘Open’. Sliding WorldModel objects will be moving in the direction you specified while in the ‘PowerOn’ state and when they have moved to the distance you specified they are considered ‘On’. While moving back to their original position and rotation they are in the ‘PowerOff’ state and when they have reached their original position and are at rest they are considered ‘Off’. Rotating and Sliding objects will stay still in their ‘On’ positions and rotations, but SpinningWorldModels will continue to spin at the specified rotations per second while ‘On’.

All WorldModels can receive “ATTACH” and “DETACH” messages sent from other objects. To send an ATTACH just send a message to a WorldModel like you would other objects and enter the name of the object you want to ATTACH:

(Ex. msg WorldModelName (ATTACH Prop0)). Only one object can be attached at a time using this method. When another ATTACH message is sent to the same WorldModel the first attachment is detached and the new object is attached. To detach the object you attached with an ATTACH message, send the object a DETACH message. DETACH takes no additional parameters.

(Ex. msg WorldModelName DETACH)

All “Active” WorldModel objects (Rotating, Sliding, and Spinning) can also receive messages to turn ‘On’ and ‘Off’. Messages that “Active” WorldModels can receive are:

- ON: If not already in the On or PowerOn states, puts the WorldModel in the PowerOn state.
- TRIGGERON: same as ON
- OFF: If not already in the Off or PowerOff states, puts the WorldModel in the PowerOff state.
- TRIGGEROFF: same as OFF
- TRIGGER: Toggles the state. Basically the same as when a player presses use against this object. If the WorldModel is in the ‘On’ or ‘PowerOn’ state it will immediately switch to ‘PowerOff’. If it’s in the ‘Off’ or ‘PowerOff’ state, then it will switch to ‘PowerOn’.
- LOCK: Locks the object. Once locked the object cannot be activated.
- UNLOCK: Unlocks the object so it can now be activated by the player and messages.

These messages take no other parameters so an example to toggle a SpinningWorldModels current state would be: msg SpinningWorldModelName TRIGGER

###### Options

All “Active” WorldModel objects (Rotating, Sliding, and Spinning) have several options that can be changed in the Options property subset group. These control how interactive the objects are and set some behavior. PlayerActivate and AIActivate, these let the object know who, if anybody, can turn them ‘On’ or Close them. If these are FLASE then only other objects can interact with it by sending it messages, if PlayerActivate is TRUE then a player can trigger the object by pressing “use”. StartOn, when TRUE, puts the object in the PowerOn or Opening state as soon as the game loads. TriggerOff toggles weather or not the object can be turned off. RemainOn, if TRUE, will keep the object in its’ ‘On’ state until told to turn off, either by the player or another object. Locked, when TRUE, will start the object off as being locked. While Locked the object cannot turn on or off until it is unlocked through a message. Waveform is a dropdown list of movement types that the object will use to rotate or move.

###### Commands

All “Active” WorldModel objects (Rotating, Sliding, and Spinning) can send commands based on what state they are in. There are 5 commands listed in the Commands property subset group: OnCommand, OffCommand, PowerOnCommand, PowerOffComand, LockedComand. Doors have similar commands with different names: OpenCommand, ClosedCommand, OpeningCommand, ClosingCommand. Each command line can have multiple commands, separated by semicolons, entered and each one will be executed every time the WorldModel object first enters the corresponding state. To have a command executed as soon as on object is activated, either by the player pressing “use” or by receiving an ‘On’ message, simply enter the command in the PowerOnCommand or OpeningCommand line. If you would like a command executed at the end of an objects movement or rotation enter it in the OnCommand line. The LockedCommand will be executed if the object is locked and a player or message tries to activate it.

###### Sounds

All “Active” WorldModel objects (Rotating, Sliding, and Spinning) can play sounds based on what state they are in. There are 5 sounds listed in the Sounds property subset group: PowerOnSound, OnSound, PowerOffSound, OffSound, LockedSound. Doors have similar sounds with different names: OpeningSound, OpenSound, ClosingSound and ClosedSound. Other properties that can be edited in this subset group are the relative sound position, the radius the sound fades off to and weather or not the sounds will loop. The LockedSound will never loop. Each sound is a single .wav file that is easily picked through a browser. The sounds will start playing every time the WorldModel object first enters the corresponding state. To have a sound start playing every time the object starts to turn off or close enter it in the PowerOffSound or ClosingSound. The LockedSound will play if the object is locked and the player or a message tries to activate it.

###### Animated Lightmaps

All “Active” WorldModel objects (Rotating, Sliding, and Spinning) can have animated lightmaps associated with their movement or rotation. To create animated lightmaps you must first add a KeyframerLight object. Set the properties of the KeyframerLight as desired, position it close to the WorldModel object you would like to lightmap, if it’s a directional light then make sure the light is pointed in the right direction. Setting ShadowMap to FALSE typically looks much better. Once the KeyframerLight is set just type the name of the KeyframerLight object in the ShadowLights property. You can enter up to 8 lights in the ShadowLights property separated by semicolons. Now just enter the number of frames you would like have in the animation, up to 128. Sometimes less frames actually look better but experiment and use what works best **. Remember that the more animations and the more frames in the animations is a real memory hog. Too many animated lightmaps is also a real frame rate killer!**

This is the basic “non-active” WorldModel object. It does not move or rotate, does not play any sounds and cannot execute any commands. Like all of the new objects this can handle Attachments, can have BlendModes, has Damage properties, and a surface type can be selected.

Any place where you need a stationary WorldModel, this is the object you should use. An example would be a desk that you want to damage or to be able to handle attachments. This object is also very well suited for keyframing. If you want a keyframed WorldModel object you should use this object.

This object is created normally. Simply bind this object to a brush or groups of brushes and then edit the properties as fit.

This object can handle damage. Edit the DamageProperties subset to define behavior.

This object can handle attachments. Enter all the objects you want attached to the WorldModel, separated by a semicolon, in the Attachments property.

None – This object does not move or rotate so there is no need for states.

WorldModels can receive these messages.

- ATTACH: Attaches the object specified in the message
- DETACH: Detach the object attached with the ATTACH message.

None – The player and AI cannot activate this object. It has no movement or rotation properties.

None – This object cannot execute any commands.

None – This object cannot play any sounds.

##### RotatingWorldModel

This WorldModel can rotate around a point a specified number of degrees around each axis. The player can interact with this object or it can be controlled only through other objects. Sounds can be played and commands can be executed when certain states are reached. Like all of the new objects this can handle Attachments, can have BlendModes, has Damage properties, and a surface type can be selected. This WorldModel can also have an animated light map associated with it.

Any place you want a WorldModel that should swing like it is hinged to a wall. Kitchen cabinets or window shutters are a good example of what these can be used for but of course there are many uses.

This object is created normally. Simply bind this object to a brush or group of brushes. To set its rotation properties just edit the vector labeled RotationAngles and either position the bound object where you would like to rotate around or link to a Point object positioned where you want the object to rotate around. Enter the number of degrees, positive or negative, around each axis you would like this object to rotate. Using the kitchen cabinet as an example you would create your brush in the closed position, bind a RotatingWorldModel to the brush, move the bound object to either the left or right edge of the brush, and then edit the vector (0.0 140.0 0.0). This cabinet door will now open out 140 degrees.

This object can handle damage. Edit the DamageProperties subset to define behavior.

This object can handle attachments. Enter all the objects you want attached to the RotatingWorldModel, separated by a semicolon, in the Attachments property.

States

- On: When the RotatingWorldModel as fully rotated to the degree amounts

specified in the RotationAngles property, it is considered ‘On’.

- PowerOn: While rotating towards the ‘On’ position it is considered to be in the ‘PowerOn’ state.
- Off: By default RotatingWorldModels start in the ‘Off’ position, and are considered ‘Off’ while in this position.
- PowerOff: While rotating from the ‘On’ position towards the ‘Off’ position theRotatingWorldModel is in the ‘PowerOff’ state.

A RotatingWorldModel can receive these messages.

- ATTACH: Attaches the object specified in the message
- DETACH: Detach the object attached with the ATTACH message.
- ON: If not already in the On or PowerOn states, puts the WorldModel in the PowerOn state.
- OFF: If not already in the Off or PowerOff states, puts the WorldModel inthe PowerOff state.
- TRIGGER: Toggles the state. Basically the same as when a player presses use against this object. If the WorldModel is in the ‘On’ or ‘PowerOn’
- state it will immediately switch to ‘PowerOff’. If it’s in the ‘Off’ or ‘PowerOff’ state, then it will switch to ‘PowerOn’.
- LOCK: Locks the object. Once locked the object cannot be activated.
- UNLOCK: Unlocks the object so it can now be activated by the player and other messages.

A RotatingWorldModel can have these options edited.

- PlayerActivate: Toggles if the Player can interact with the RotatingWorldModel or not.
- StartOn: When TRUE the RotatingWorldModel is in the ‘On’ position at load time
- TriggerOff: Toggles weather or not the player can directly turn a
- RotatingWorldModel ‘Off’.
- RemainOn: If this is TRUE the RotatingWorldModel will stay in the ‘On’ position until directly told to turn off, either by a player or a message.
- ForceMove: When TRUE the RotatingWorldModel will rotate through the player and other objects.
- Locked : Toggles weather this object starts locked or not.
- RotateAway: If TRUE the RotatingWorldModel will swing away from the player.
- Waveform: Defines how the object Rotates.

A RotatingWorldModel can send these commands when in the corresponding state.

- OnCommand
- OffCommand
- PowerOnCommand
- PowerOffComand
- LockedComand

A RotatingWorldModel can play these sounds when in the corresponding state.

- PowerOnSound
- OnSound
- PowerOffSound
- OffSound
- LockedSound

This WorldModel can slide, or move, a specified number of units in a specified direction. The player can interact with this object or it can be controlled only through other objects. Sounds can be played and commands can be executed when certain states are reached. Like all of the new objects this can handle Attachments, can have BlendModes, has Damage properties, and a surface type can be selected. This WorldModel can also have an animated light map associated with it.

Any place you want a WorldModel that should move in a specific direction. Desk drawers are a good example of what these can be used for but of course there are many uses.

This object is created normally. Simply bind this object to a brush or group of brushes. To set its movement properties just edit the vector labeled MoveDir and set the distance you would like this SlidingWorldModel to move to in the property labeled MoveDist. A MoveDir vector of (0.0 1.0 0.0 ) will move the SlidingWorldModel along its own local Y axis, typically straight up. This vector can be edited to point in any direction you want (0.5 0.5 0.0) will move the SlidingWorldModel diagonally along its X and Y axis. The MoveDist property is the distance the SlidingWorldModel will travel in DEdit units. Using the desk drawer as an example you would create your brush in the closed position, bind a SlidingWorldModel to the brush and then edit the MoveDir vector (0.0 0.0 1.0). Now specify how far you want the object to move by making MoveDist 64.0. The desk drawer will now slide 64 units out in its local Z axis.

This object can handle damage. Edit the DamageProperties subset to define behavior.

This object can handle attachments. Enter all the objects you want attached to the SlidingWorldModel, separated by a semicolon, in the Attachments property.

- On: When the SlidingWorldModel is fully moved to the distance
- specified in the MoveDist property, it is considered ‘On’.
- PowerOn: While moving towards the ‘On’ position it is considered to be in the ‘PowerOn’ state.
- Off: By default SlidingWorldModels start in the ‘Off’ position, and are considered ‘Off’ while in this position.
- PowerOff: While moving from the ‘On’ position towards the ‘Off’ position theSlidingWorldModel is in the ‘PowerOff’ state.

A SlidingWorldModel can receive these messages.

- ATTACH: Attaches the object specified in the message
- DETACH: Detach the object attached with the ATTACH message.
- ON: If not already in the On or PowerOn states, puts the WorldModel in the PowerOn state.
- OFF: If not already in the Off or PowerOff states, puts the WorldModel in the PowerOff state.
- TRIGGER: Toggles the state. Basically the same as when a player presses use against this object. If the WorldModel is in the ‘On’ or ‘PowerOn’ state it will immediately switch to ‘PowerOff’. If it’s in the ‘Off’ or ‘PowerOff’ state, then it will switch to ‘PowerOn’.
- LOCK: Locks the object. Once locked the object cannot be activated.
- UNLOCK: Unlocks the object so it can now be activated by the player and other messages.

A SlidingWorldModel can have these options edited.

- PlayerActivate: Toggles if the Player can interact with the SlidingWorldModel or not.
- StartOn: When TRUE the SlidingWorldModel is in the ‘On’ position at load time
- TriggerOff: Toggles weather or not the player can directly turn a
- SlidingWorldModel ‘Off’.
- RemainOn: If this is TRUE the SlidingWorldModel will stay in the ‘On’ position until directly told to turn off, either by a player or a message.
- ForceMove: When TRUE the SlidingWorldModel will move through the player andother objects.
- Locked : Toggles weather this object starts locked or not.
- Waveform: Defines how the object moves.

A SlidingWorldModel can send these commands when in the corresponding state.

- OnCommand
- OffCommand
- PowerOnCommand
- PowerOffComand
- LockedComand

A SlidingWorldModel can play these sounds when in the corresponding state.

- PowerOnSound
- OnSound
- PowerOffSound
- OffSound
- LockedSound

This WorldModel can spin around a point a in the specified amount of time to make one rotation around each axis. The player can interact with this object or it can be controlled only through other objects. Sounds can be played and commands can be executed when certain states are reached. Like all of the new objects this can handle Attachments, can have BlendModes, has Damage properties, and a surface type can be selected. This WorldModel can also have an animated light map associated with it.

Any place you want a WorldModel that should spin around a central point. Ceiling fans or a Rolodex are good examples of what these can be used for but of course there are many uses.

This object is created normally. Simply bind this object to a brush or group of brushes. To set its rotation properties just edit the vector labeled RotationAngles and either position the bound object where you would like to spin around or link to a Point object positioned where you want the object to spin around. Enter the amount of time, in seconds to make one rotation around each axis, you would like this object to spin. Using the ceiling fan as an example you would create your brush in the closed position, bind a SpinningWorldModel to the brush, move the bound object to the center of the object (by default it is), and then edit the RotationAngles vector (0.0 4.0 0.0). This fan will now spin around its Y axis once every 4 seconds.

This object can handle damage. Edit the DamageProperties subset to define behavior.

This object can handle attachments. Enter all the objects you want attached to the RotatingWorldModel, separated by a semicolon, in the Attachments property.

- On: When the SpinningWorldModel is spinning at the desired rate
- specified in the RotationAngles property, it is considered ‘On’.
- PowerOn: While spinning around the point picking up speed towards the specified rate it is considered to be in the ‘PowerOn’ state.
- Off: By default RotatingWorldModels start in the ‘Off’ position, and are considered ‘Off’ when they are no longer spinning.
- PowerOff: While spinning from the specified rate slowly towards a resting position the SpinningWorldModel is in the ‘PowerOff’ state.

A SpinningWorldModel can receive these messages.

- ATTACH: Attaches the object specified in the message
- DETACH: Detach the object attached with the ATTACH message.
- ON: If not already in the On or PowerOn states, puts the WorldModel in the PowerOn state.
- OFF: If not already in the Off or PowerOff states, puts the WorldModel in the PowerOff state.
- TRIGGER: Toggles the state. Basically the same as when a player presses use against this object. If the WorldModel is in the ‘On’ or ‘PowerOn’ state it will immediately switch to ‘PowerOff’. If it’s in the ‘Off’ or ‘PowerOff’ state, then it will switch to ‘PowerOn’.
- LOCK : Locks the object. Once locked the object cannot be activated.
- UNLOCK: Unlocks the object so it can now be activated by the player and other messages.

A SpinningWorldModel can have these options edited.

- PlayerActivate: Toggles if the Player can interact with the SpinningWorldModel or not.
- StartOn: When TRUE the SpinningWorldModel will start spinning at load time
- TriggerOff: Toggles weather or not the player can directly turn a
- SpinningWorldModel ‘Off’.
- RemainOn: If this is TRUE the SpinningWorldModel will keep on spinning until directly told to turn off, either by a player or a message.
- ForceMove: When TRUE the SpinningWorldModel will rotate through the player and other objects.
- Locked : Toggles weather this object starts locked or not.
- Waveform: Defines how the object Spins.

A SpinningWorldModel can send these commands when in the corresponding state.

- OnCommand
- OffCommand
- PowerOnCommand
- PowerOffComand
- LockedComand

A SpinningWorldModel can play these sounds when in the corresponding state.

- PowerOnSound
- OnSound
- PowerOffSound
- OffSound
- LockedSound

This Door can rotate around a point a specified number of degrees around each axis. The player can interact with this object or it can be controlled only through other objects. Sounds can be played and commands can be executed when certain states are reached. Like all of the new objects this can handle Attachments, can have BlendModes, has Damage properties, and a surface type can be selected. This Door can also have an animated light map associated with it. Doors also have the ability to open another door they are linked to and they can open and close portals when they open and close.

Any place you want a Door that should swing like it is hinged to a wall. An office Door or a car Door are good examples of what these can be used for but of course there are many uses.

This object is created normally. Simply bind this object to a brush or group of brushes. To set its rotation properties just edit the vector labeled RotationAngles and either position the bound object where you would like to rotate around or link to a Point object positioned where you want the object to rotate around. Enter the number of degrees, positive or negative, around each axis you would like this object to rotate. Using the office door as an example you would create your brush in the closed position, bind a RotatingDoor to the brush, move the bound object to either the left or right edge of the brush, and then edit the vector (0.0 90.0 0.0). This office door will now open 90 degrees.

If you want this door to open another door whenever it is activated to open simply use the DoorLink property’s ObjectBrowser to find the door name you would like. Typically Door1 will link to Door 2 and Door2 will link to Door1, this way doors right next to each other will open more naturally. If you want this door to control the opening and closing of a portal just type in the name of the portal brush you want in the PortalName property.

This object can handle damage. Edit the DamageProperties subset to define behavior.

This object can handle attachments. Enter all the objects you want attached to the RotatingDoor, separated by a semicolon, in the Attachments property. A very good use for this would be a doorknob and a peephole.

- Open: When the RotatingDoor is fully rotated to the degree amounts
- specified in the RotationAngles property, it is considered ‘Open’.
- Opening: While rotating towards the ‘Open’ position it is considered to be in the ‘Opening’ state.
- Closed: By default a RotatingDoor starts in the ‘Closed’ position, and are considered‘Closed’ whenever in this position.
- Closing: While rotating from the ‘Open’ position towards the ‘Closed’ position the RotatingDoor is in the ‘Closing’ state.

A RotatingDoor can receive these messages.

- ATTACH: Attaches the object specified in the message
- DETACH: Detach the object attached with the ATTACH message.
- ON: If not already in the Open or Opening states, puts the Door in the Opening state.
- OFF: If not already in the Closed or Closing states, puts the Door in the Closing state.
- TRIGGER: Toggles the state. Basically the same as when a player presses use against this object. If the Door is in the ‘Open’ or ‘Opening’
- state it will immediately switch to ‘Closing’. If it’s in the ‘Closed’ or ‘Closing’ state, then it will switch to ‘Opening’.
- LOCK: Locks the object. Once locked the object cannot be activated.
- UNLOCK: Unlocks the object so it can now be activated by the player and other messages.

A RotatingDoor can have these options edited.

- PlayerActivate: Toggles if the Player can interact with the RotatingDoor or not.
- AIActivate: Toggles if AI can interact with the door or not.
- StartOpen: When TRUE the RotatingDoor is in the ‘Open’ position at load time.
- TriggerClose: Toggles weather or not the player can directly Close a RotatingDoor.
- RemainOpen: If this is TRUE the RotatingDoor will stay in the ‘Open’ position until directly told to close, either by a player or a message.
- ForceMove: When TRUE the RotatingDoor will rotate through the player andother objects.
- Locked : Toggles weather this object starts locked or not.
- RotateAway: If TRUE the RotatingDoor will swing away from the player.
- Waveform: Defines how the object Rotates.

A RotatingDoor can send these commands when in the corresponding state.

- OpenCommand
- ClosedCommand
- OpeningCommand
- ClosingComand
- LockedComand

A RotatingDoor can play these sounds when in the corresponding state.

- OpeningSound
- OpenSound
- ClosingSound
- ClosedSound
- LockedSound

This Door can slide, or move, a specified number of units in a specified direction. The player can interact with this object or it can be controlled only through other objects. Sounds can be played and commands can be executed when certain states are reached. Like all of the new objects this can handle Attachments, can have BlendModes, has Damage properties, and a surface type can be selected. This Door can also have an animated light map associated with it. Doors also have the ability to open another door they are linked to and they can open and close portals when they open and close.

Any place you want a Door that should move in a specific direction. Sliding glass doors or those sliding Asian doors are a very good example of what these can be used for but of course there are many uses.

This object is created normally. Simply bind this object to a brush or group of brushes. To set its movement properties just edit the vector labeled MoveDir and set the distance you would like this SlidingDoor to move to in the property labeled MoveDist. A MoveDir vector of (0.0 1.0 0.0 ) will move the SlidingDoor along its own local Y axis, typically straight up. This vector can be edited to point in any direction you want (0.5 0.5 0.0) will move the SlidingDoor diagonally along its X and Y axis. The MoveDist property is the distance the SlidingDoor will travel in DEdit units. Using the sliding glass door as an example you would create your brush in the closed position, bind a SlidingDoor to the brush and then edit the MoveDir vector (1.0 0.0 0.0). Now specify how far you want the object to move by making MoveDist 128.0. The sliding door will now slide 128 units out in its local X axis. If you want this door to open another door whenever it is activated to open simply use the DoorLink property’s ObjectBrowser to find the door name you would like. Typically Door1 will link to Door 2 and Door2 will link to Door1, this way doors right next to each other will open more naturally. If you want this door to control the opening and closing of a portal just type in the name of the portal brush you want in the PortalName property.

This object can handle damage. Edit the DamageProperties subset to define behavior.

This object can handle attachments. Enter all the objects you want attached to the SlidingDoor, separated by a semicolon, in the Attachments property. A very good use for this would be a doorknob and a peephole.

- Open: When the SlidingDoor is fully moved to the distancespecified in the MoveDist property, it is considered ‘On’.
- Opening: While moving towards the ‘Open’ position it is considered to be in the ‘Opening’ state.
- Closed: By default a SlidingDoor starts in the ‘Closed’ position, and are considered ‘Closed’ whenever in this position.
- Closing: While moving from the ‘Open’ position towards the ‘Closed’ position the SlidingDoor is in the ‘Closing’ state.

A SlidingDoor can receive these messages.

- ATTACH: Attaches the object specified in the message
- DETACH: Detach the object attached with the ATTACH message.
- ON: If not already in the Open or Opening states, puts the Door in the Opening state.
- OFF: If not already in the Closed or Closing states, puts the Door inthe Closing state.
- TRIGGER: Toggles the state. Basically the same as when a player presses use against this object. If the Door is in the ‘Open’ or ‘Opening’
- state it will immediately switch to ‘Closing’. If it’s in the ‘Closed’ or ‘Closing’ state, then it will switch to ‘Opening’.
- LOCK: Locks the object. Once locked the object cannot be activated.
- UNLOCK: Unlocks the object so it can now be activated by the player and other messages.

A SlidingDoor can have these options edited.

- PlayerActivate: Toggles if the Player can interact with the SlidingDoor or not.
- AIActivate: Toggles if AI can interact with the door or not.
- StartOpen: When TRUE the SlidingDoor is in the ‘Open’ position at load time.
- TriggerClose: Toggles weather or not the player can directly Close a SlidingDoor.
- RemainOpen: If this is TRUE the SlidingDoor will stay in the ‘Open’ position until directly told to close, either by a player or a message.
- ForceMove: When TRUE the SlidingDoor will rotate through the player andother objects.
- Locked: Toggles weather this object starts locked or not.
- Waveform: Defines how the object Moves.

A SlidingDoor can send these commands when in the corresponding state.

- OpenCommand
- ClosedCommand
- OpeningCommand
- ClosingComand
- LockedComand

A SlidingDoor can play these sounds when in the corresponding state.

- OpeningSound
- OpenSound
- ClosingSound
- ClosedSound
- LockedSound

This Switch can rotate around a point a specified number of degrees around each axis. The player can interact with this object or it can be controlled only through other objects. Sounds can be played and commands can be executed when certain states are reached. Like all of the new objects this can handle Attachments, can have BlendModes, has Damage properties, and a surface type can be selected. This Switch can also have an animated light map associated with it.

Any place you want a Switch that should swing like it is hinged to the floor. Levers are a good example of what these can be used for but of course there are many uses.

This object is created normally. Simply bind this object to a brush or group of brushes. To set its rotation properties just edit the vector labeled RotationAngles and either position the bound object where you would like to rotate around or link to a Point object positioned where you want the object to rotate around. Enter the number of degrees, positive or negative, around each axis you would like this object to rotate. Using the lever as an example you would create your brush in the closed position, bind a RotatingSwitch to the brush, move the bound object to the bottom edge of the brush, and then edit the vector (0.0 0.0 -45.0). This lever will now rotate -45 degrees around it’s Z axis.

This object can handle damage. Edit the DamageProperties subset to define behavior.

This object can handle attachments. Enter all the objects you want attached to the RotatingSwitch, separated by a semicolon, in the Attachments property. A good example of this would be a handle for the lever.

- On: When the RotatingSwitch as fully rotated to the degree amountsspecified in the RotationAngles property, it is considered ‘On’.
- PowerOn: While rotating towards the ‘On’ position it is considered to be in the ‘PowerOn’ state.
- Off: By default RotatingSwitches start in the ‘Off’ position, and are considered ‘Off’ while in this position.
- PowerOff: While rotating from the ‘On’ position towards the ‘Off’ position the RotatingSwitch is in the ‘PowerOff’ state.

A RotatingSwitch can receive these messages.

- ATTACH: Attaches the object specified in the message
- DETACH: Detach the object attached with the ATTACH message.
- ON: If not already in the On or PowerOn states, puts the Switch in the PowerOn state.
- OFF: If not already in the Off or PowerOff states, puts the Switch inthe PowerOff state.
- TRIGGER: Toggles the state. Basically the same as when a player presses use against this object. If the Switch is in the ‘On’ or ‘PowerOn’ state it will immediately switch to ‘PowerOff’. If it’s in the ‘Off’ or ‘PowerOff’ state, then it will switch to ‘PowerOn’.
- LOCK: Locks the object. Once locked the object cannot be activated.
- UNLOCK: Unlocks the object so it can now be activated by the player and other messages.

A RotatingSwitch can have these options edited.

- PlayerActivate: Toggles if the Player can interact with the RotatingSwitch or not.
- StartOn: When TRUE the RotatingSwitch is in the ‘On’ position at load time.
- TriggerOff: Toggles weather or not the player can directly turn a RotatingSwitch ‘Off’.
- RemainOn: If this is TRUE the RotatingSwitch will stay in the ‘On’ position until directly told to turn off, either by a player or a message.
- ForceMove: When TRUE the RotatingSwitch will rotate through the player and other objects.
- Locked : Toggles weather this object starts locked or not.
- RotateAway: If TRUE the RotatingSwitch will swing away from the player.
- Waveform: Defines how the object Rotates.

A RotatingSwitch can send these commands when in the corresponding state.

- OnCommand
- OffCommand
- PowerOnCommand
- PowerOffComand
- LockedComand

A RotatingSwitch can play these sounds when in the corresponding state.

- PowerOnSound
- OnSound
- PowerOffSound
- OffSound
- LockedSound

This Switch can slide, or move, a specified number of units in a specified direction. The player can interact with this object or it can be controlled only through other objects. Sounds can be played and commands can be executed when certain states are reached. Like all of the new objects this can handle Attachments, can have BlendModes, has Damage properties, and a surface type can be selected. This WorldModel can also have an animated light map associated with it.

Any place you want a Switch that should move in a specific direction. Push buttons are a good example of what these can be used for but of course there are many uses.

This object is created normally. Simply bind this object to a brush or group of brushes. To set its movement properties just edit the vector labeled MoveDir and set the distance you would like this SlidingSwitch to move to in the property labeled MoveDist. A MoveDir vector of (0.0 0.0 1.0 ) will move the SlidingSwitch along its own local Z axis, typically forward. This vector can be edited to point in any direction you want (0.5 0.5 0.0) will move the SlidingSwitch diagonally along its X and Y axis. The MoveDist property is the distance the SlidingSwitch will travel in DEdit units. Using the push button as an example you would create your brush in the closed position, bind a SlidingSwitch to the brush and then edit the MoveDir vector (0.0 0.0 1.0). Now specify how far you want the object to move by making MoveDist 8.0. The push button will now slide 8 units out in its local Z axis.

This object can handle damage. Edit the DamageProperties subset to define behavior.

This object can handle attachments. Enter all the objects you want attached to the SlidingSwitch, separated by a semicolon, in the Attachments property.

- On: When the SlidingSwitch is fully moved to the distancespecified in the MoveDist property, it is considered ‘On’.
- PowerOn: While moving towards the ‘On’ position it is considered to be in the ‘PowerOn’ state.
- Off: By default SlidingSwitches start in the ‘Off’ position, and are considered ‘Off’ while in this position.
- PowerOff: While moving from the ‘On’ position towards the ‘Off’ position the SlidingSwitch is in the ‘PowerOff’ state.

A SlidingSwitch can receive these messages.

- ATTACH: Attaches the object specified in the message
- DETACH: Detach the object attached with the ATTACH message.
- ON: If not already in the On or PowerOn states, puts the Switch in the PowerOn state.
- OFF: If not already in the Off or PowerOff states, puts the Switch inthe PowerOff state.
- TRIGGER: Toggles the state. Basically the same as when a player presses use against this object. If the Switch is in the ‘On’ or ‘PowerOn’ state it will immediately switch to ‘PowerOff’. If it’s in the ‘Off’ or ‘PowerOff’ state, then it will switch to ‘PowerOn’.
- LOCK: Locks the object. Once locked the object cannot be activated.
- UNLOCK: Unlocks the object so it can now be activated by the player and other messages.

A SlidingSwitch can have these options edited.

- PlayerActivate: Toggles if the Player can interact with the SlidingSwitch or not.
- StartOn: When TRUE the SlidingSwitch is in the ‘On’ position at load time
- TriggerOff: Toggles weather or not the player can directly turn a SlidingSwitch ‘Off’.
- RemainOn: If this is TRUE the SlidingSwitch will stay in the ‘On’ position until directly told to turn off, either by a player or a message.
- ForceMove: When TRUE the SlidingSwitch will move through the player andother objects.
- Locked : Toggles weather this object starts locked or not.
- Waveform: Defines how the object moves.

A SlidingSwitch can send these commands when in the corresponding state.

- OnCommand
- OffCommand
- PowerOnCommand
- PowerOffComand
- LockedComand

A SlidingSwitch can play these sounds when in the corresponding state.

- PowerOnSound
- OnSound
- PowerOffSound
- OffSound
- LockedSound

This object is placed in every level to define many of the global properties of the level.
