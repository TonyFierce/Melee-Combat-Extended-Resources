# Melee Combat Extended Resources

Melee Combat Extended is a user-made mod for Arma Reforger that extends melee combat logic of the base game.
https://reforger.armaplatform.com/workshop/6595113A3678CF5D-MeleeCombatExtended

### PREREQUISITES
Before you open any Blender files included in the repo:
1. Install Arma Reforger Tools
2. Make sure that your Blender version is compatible with Enfusion Workbench (I used 4.2 LTS)
3. Setup the Enfusion Blender Tools addon
https://community.bistudio.com/wiki/Arma_Reforger:Enfusion_Blender_Tools


## Guide: Adding New Custom Melee Weapons

### 1. Blender 3D Model Setup

#### Proper Model Orientation

The edge of your melee weapon model should face negative X axis:
![Blender Model Orientation](Guide%20Images/Blender%20Model%20Orientation.jpg)

![Blender Model Orientation Perspective](Guide%20Images/Blender%20Model%20Orientation%20Perspective.jpg)

#### Colliders creation
Colliders can be created using the Simple Collider addon for Blender
https://github.com/Weisl/simple_collider

You can follow this video tutorial:
https://www.youtube.com/watch?v=-h9_eOCZh7U&t=326s

Delete all materials created by Simple Collider addon before exporting to Enfusion Workbench

Your results should look similar to mine:
![Blender Colliders](Guide%20Images/Blender%20Colliders.jpg)


### 2. Exporting to Enfusion Workbench

#### Transform Settings

When you initally import the .fbx file from Blender into Enfusion Workbench, the weapon won't be positioned and rotated properly in the character's hand

To correct this, you must change the model transform in file import settings and click "reimport":
![Editor Model Import Transform](Guide%20Images/Editor%20Model%20Import%20Transform.jpg)

#### Colliders in editor
If you have correctly created the colliders in Blender, they should be visible in Enfusion Workbench:
![Editor Model Colliders](Guide%20Images/Editor%20Model%20Colliders.jpg)

Sometimes you must simplify the geometry of the collider to make Enfusion Workbench accept it during export (use decimate modifier in Blender)


### 3. Textures

#### Packing textures in a format supported by Enfusion Engine

You can follow this video tutorial:
https://www.youtube.com/watch?v=H0BfD3Ri8L0&list=LL&index=19

The channel packing tool is included in this repo
