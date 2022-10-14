# Asset Basics
Assets are various things you can use in your game. 

## Overview of the most basic GameMaker assets
* Sprites are most of the images in your game. They can be animated, and have an associated collision hitbox.
* Sounds are sounds. These are used by GameMaker's audio engine, which renex engine doesn't use - instead, sound files are stored in the `data` folder, next to the engine `source` folder.
* Backgrounds are big images that can be used as, well, room backgrounds or tilesets.
* Objects are the things that make up your game - they exist somewhere in the current room, and they run their logic. For example, `Player`, `Cherry`, `Warp`, etc. are all objects. The individual things that then exist in your game are called instances of objects, so for example, a room may have many Blocks in it - these are different instances of one object. This is a small distinction, but it's worth noting.
* Rooms are where your game takes place - you are always in one, e.g. starting your game always puts you in the very first room in the Rooms folder. They contain object instances and tiles, and they can have backgrounds.

## Asset Tree
Assets are located in the asset tree:

![](img/03_asset_tree.png)

Most assets can be created by right-clicking the respective folder -> "Create ..." or by clicking the corresponding button in the top bar:

![](img/03_buttons.png)

Each asset has a name and can be dragged around in the asset tree. You can also group assets in subfolders by right clicking in the tree and selecting "Create group".

## Room Editor
GameMaker 8.2 comes with two room editors - the classic GameMaker 8 editor, and a new one made for 8.2, commonly referred to as gm82room. You can switch between the two editors in the far right button on the top button bar, in the File dropdown, or in GameMaker preferences. You probably won't find yourself needing to use the legacy editor, so we'll only focus on the new one.

gm82room opens in a separate window, as it is a separate program - there isn't a way to edit your project at the same time as you are editing a room. Simply double click any room in the asset tree to open it, here we'll open `rmTemplate` in the `Game` folder.

![](img/03_room_editor.png)

The first time you launch the room editor you'll get a quick guide.

![](img/03_room_guide.png)

### Creating your first Room

Creating a room is simple. Because there are common room settings and objects between most rooms, we don't actually create a brand new room. Instead, make a duplicate of `rmTemplate` by right-clicking the room in the asset tree.

![](img/03_room_duplicate.png)

After making the new room, you can rename it however you like and double-click it to open.

The editor has several "modes", selected by the big buttons in the top left corner - you can see the editor opens in the Instances mode. This is where you place and move instances of objects. On the left you have a palette of objects to choose from - these are all objects that already exist in the room. The very last button in the palette is used to select other objects in the project.

You can try dragging some objects around, or stretching some of the Blocks with the square handle at the bottom left of the selected instance.

Some of the objects already present in the template room are `PlayerStart`, which indicates where the Player spawns, the savepoint, a `MusicPlayer` instance that sets the background music for this room, or an `Autotiler` that places tiles in the room to match the Blocks when the room is created. To explain the difference between instances and tiles, we'll place the tiles ourselves, so for now delete the `Autotiler` instance.

Switch to the Tiles tab in the top left corner, and click on the empty gray bar to select a tileset. Click the plus button in the left palette tab to add a new tile. Select a single tile to place (you can drag to select a bigger area, but you most likely don't need to), and press the finish button in the top left. Now you can select that tile from the palette at any point and place it in the room, moving and stretching it just like you can with instances. Place tiles under all of the Blocks in the room - the Blocks won't actually be visible in-game!

Lastly for now, you can switch to the backgrounds tab, and select a background by clicking the empty gray box below the 8 numbered buttons, just like you selected a tileset.

Now we need to tell the engine to use our new room as the start of the game. This might look scary since you'll have to open certain script and edit one line of code in it, but no worries. Open the engine_settings script at the very top of the Scripts folder.

![](img/03_engine_settings.png)

Now edit this specific line so that `global.first_room` gets set to the new room you just made.

![](img/03_engine_settings_room.png)

After that is done, you should be able to hit the green "Run test build" button (or just press `F5`) and after going through the menus you'll see your room in its full glory!

`[TODO: review the rest]`

Finally, let's see how to change the music of this room to something else. Assuming you know how to add music to your game (see latter chapters on that). Open your room, find the `MusicPlayer` object in the top-left corner of the room (looks like a piece of paper with a note drawn on it) and click on its bottom-left corner to open it's fields.

![](img/03_room_fields.png)

Click on `BGM` option and change to the file name of the song you want to play. That's it! Feel free to launch your game and see the new music being played. 

That's it for the basic tutorial. You can always go around and experiment a little, but it is also recommended to look at other chapters, just so you know is **not recommended** to do.

### Instances
Instances are, basically, instances of certain objects in the room.
It is important to destinguish between Objects and Instances. For example, every red cherry you see in a room is an instance of the object `Cherry`. Instances tab of Room Editor allows you to place instances of selected object from object palette (panel on the left). One of the features of Room Editor is ability for object to define fields, which allow easier configuration of each instance. You access fields by clicking object's bottom-left corner (where the icon is at) 

![](img/03_fields.png)

### Grid snap
Grid snap allows you to make objects and tiles get snapped to a grid when placing. 
In the top bar you can find two number input fields. Those control grid snap. One to the left controls grid cell width, one to the right controls grid cell height. As Quick Guide states, you can ignore the snap by pressing `Alt`.

### Tiles
Backgrounds can be used as tilesets. In Tiles tab of Room Editor you can add tiles to palette and place them. Choose background from where to take tiles, then click on "Add tiles..." button, then select the area that matches the single tile you want to add. Repeat until added all tiles needed. Now you can place them down. Alternatively, renex engine provides auto-tiler, but this won't be discussed in this tutorial, you can examine how it works in rTemplate room and examine the code and tile format behind it. 

### Backgrounds
You can have backgrounds in room, up to 8 of them (see in Backgrounds tab of room editor there are 8 buttons from 0 to 7). Each background possibly has a solid Colour and possibly has a Background asset to render above it. You can set it up in Background tab of Room Editor. There are options for drawing it tiled or stretched, also for offset and move speed. Background also can be drawn on foreground layer (above everything else). 

### Room Settings
There are multiple room settings available, but you really should touch only one of them: room size.
Here is a little breakdown of all of them.

* Caption (optional): Room caption is the window title. Engine sets the caption for you to include title and stats, don't edit this option yourself.
* Size: size of the room in pixels.
* Speed: Preferred FPS of the room. Fangames usually run at 50.
* "Persistent" option: If on, when you exit the room it is not completely unloaded, it's state is remembered and gets loaded back when you return. Breaks many things so keep this off.
* "Clear" option: If on, clears the screen before drawing to it. It should stay on. 
* Room code (optional): Custom code to execute when room loads.

## Sprites - animations, origin
Sprite is usually small image that objects use as their appearance. Sprites can have several subimages (frames) in them so you can make simple animations, they can have transparency in them, as well as they can be used for collision detection between objects based on non-transparent pixels (when used by objects as masks). Editing a sprite, you will find several properties as well as the sprite itself. Double-clicking on it will open up individual subimages. Animation is done through setting __instance's__ `image_speed` to the amount of animation to progress each frame (so if the value is 1/5 then each 5 frames it will transition to the next animation subimage). Each sprite also has an origin point. To put simply, when instance uses this sprite, sprite will be placed so the origin point matches with instance's coordinates.

### Creating Sprite
You can create new sprite by either right-clicking on "Sprites" folder in the asset tree -> "Create Sprite" or pressing "Create a sprite" button in top bar (looks like red pacman). Creating sprite or double-clicking existing one in asset tree will open Sprite Properties window:

![](img/03_sprite_window.png)

Let's walk through non-obvious options and what each one does:

1) Sprite name: the same name that will appear in the asset tree and by which you can refer to this sprite in code.
2) Load sprite from file: You can load sprites from files! You can use BMP, GIF, JPG and PNG sprites, as well as Game Maker Sprite format.
3) Save sprite into file: You can save sprites into Game Maker Sprite format with all the metadata stored in it. Saving individual subimages is also possible through Sprite Edit window.
4) Edit sprite button: This one will open Edit Sprite window.
5) Sprite origin: This setting sets the point relative to the top left corner of the sprite that will be used as sprite origin point. We've already mentioned what it does.
6) Precise collision checking: If this option is on, the collision with this sprite will be pixel-perfect. Otherwise it'll check only bounding box of the sprite.
7) Separate collision masks: If this option is on and sprite has more than 1 subimage, then collision mask will match the current subimage, instead of using one mask that consists of all subimages grouped on top of eachother. You can edit more of these by pressing "Modify masks" button, but i doubt you'll ever need it.

If you press on "Edit Sprite" button, then it will open Sprite Edit window:

![](img/03_sprite_edit_window.png)

From here you can add, delete or edit each individual subimage of the sprite (double-click to edit), change their order, save one to PNG or read one from file, as well as preview sprite by using "Show preview" checkbox. More image manipulations are available in image editor or in menu options. They should be quite straght-forward to use.

## Backgrounds - tilesets
Backgrounds are images that are simply drawn to the screen. They are used in mainly two ways: Tilesets or Actually room backgrounds. Backgrounds cannot be animated and don't have collision. You can also use backgrounds for various props in your room. Using Background as room background was discussed previously, in order to use it as tileset you should also check the "Use as Tileset" checkbox in Background's properties and set up the size of each tile. Other options are useful only if your tiles are not tightly packed together and have space around them. In order to use background as a static prop, in Room Editor you open Tiles tab, add this background as tile, select whole area as tile region. Now you can place the prop.

### Creating Background
The process is similar to (and even easier than) creating sprites. Right-click on "Backgrounds" folder of Asset Tree or click on "Create Background" button in top bar (looks like an image icon). Creating background or double-clicking existing one will open Background Properties window. From here you can 
* Load background from BMP, GIF, JPG, PNG or Game Maker Background format with all metadata stored in it
* Save background to Game Maker Background format
* Edit background. This will open image editor, from where you also can save background as PNG.

To use background as tileset, tick the checkbox "Use as tile set" and fill in "tile width" and "tile height" options in opened panel.

## Sounds
**!IMPORTANT! This section is important!** 

Sounds in Game Maker 8.2 are slightly different than in other Game Maker versions. They operate on built-in Game Maker 8.2 Sound extension, which allows things like lazy-load sounds, sound encryption, effects, and many other things. But you cannot use the legacy Game Maker Sound system: 

![](img/03_sound_no.png)

### Adding Sounds
In renex engine you add sounds to your project by putting the sound into respective folder (must have either `.mp3`, `.ogg`, `.wav` for sounds, put them into `data/sounds`, and either `.ogg`, `.mp3`, `.mod`, `.s3m` for music, put them into `data/music`).

![](img/03_sound_folder.png)

![](img/03_sound_folder2.png)

**IMPORTANT**: When you finish with your game and Create Executable, you have to copy the `data` folder together with the exe. Otherwise there will be an error prompting you to do so :-)

To play the sound you use it's file name (WITHOUT file extension). For example, in code:

![](img/03_sound_play_example.png)

There are plenty of functions to make sounds sound differently, things like pitch, various effects and many more. They are quite advanced but in case you'll need them, there are some info on how to use them: Game Maker 8.2 Sound extension [readme](https://github.com/GM82Project/gm82snd/blob/master/readme.txt)

## Engine Settings
Renex engine is highly customizable, providing you with lots of settings to edit. You can locate them here: 

![](img/03_engine_settings.png)

Those are most important ones:

`game_title` - change the game title displayed in window title.

`first_room` - change the first room player spawns in.

Other options are thoroughly explained in the mentioned file in comments. Make sure to read it if something works not as you want. 
