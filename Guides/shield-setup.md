# Guide: How to Create and Configure Shields that Block Projectiles and Melee Attacks

## 1. Setting up Melee Combat Extended as a dependency for your mod

This step is required to be able to access the functionality of custom MCE scripts from within your mod  
Make sure that you have downloaded MCE using Arma Reforger's mod browser

### When creating a new Enfusion Workbench project (mod)
![MCE as dependency](../Guide%20Images/MCE%20as%20dependency.jpg)

### When you already have an existing project (mod)
With your project open click "Workbench" -> "Options" -> "Dependencies" -> add a new dependency and use the ID of MCE (or you can simply browse to the location where your downloaded MCE folder is saved)

## 2. Create a new shield model or find one that you can use
Make sure to properly position and scale your shield in Blender  
The handles for carrying the shield with the left arm should also be precisely where I placed them on the 2 models included in MCE (and also be similar in size)
![Shield Model in Blender](../Guide%20Images/Blender%20Shield%20Model.jpg)

### Enfusion Workbench .xob import settings
Rotation must be set to -90 degrees on X axis (assuming you rotated the shield model correctly in Blender)  
Your shield model must have at least 1 collider - otherwise it will NOT protect against melee damage or projectiles:
![Shield Model Import Settings](../Guide%20Images/Editor%20Shield%20Model%20Import.jpg)
The collider must also have the FireGeo layer preset

## 3. Copying one of the MCE Shield Prefabs
Properly configured MCE shield prefabs can be found in this folder:  
Melee Combat Extended\Prefabs\Items\Equipment\Shields\

These prefabs already include all the components and settings required for the shield to work correctly

## 4. Changing the mesh and shield prefab reference
Select MeshObject component of the shield prefab and change the model to the one you would like to use

### Reference to iself in Shield Component
Select SCR_MCE_ShieldComponent in the prefab's hierarchy and change the reference to the shield prefab itself
![Shield Prefab Setup](../Guide%20Images/Shield%20Prefab%20Component%20Setup.jpg)

## 5. Changing the name, description and tooltip
Select InventoryItemComponent in the armor prefab  
In Attributes/ItemDisplayName you will find:
- Name
- Description
- Item Hints - don't need to change this, all shields can have the same tooltip, they all block melee attacks and projectiles
