# Guide: How to Create and Configure Armor that Protects VS Melee Damage

## 1. Setting up Melee Combat Extended as a dependency for your mod

This step is required to be able to access the functionality of custom MCE scripts from within your mod
Make sure that you have downloaded MCE using Arma Reforger's mod browser

### When creating a new Enfusion Workbench project (mod)
![MCE as dependency](Guide%20Images/MCE%20as%20dependency.jpg)

### When you already have an existing project (mod)
With your project open click "Workbench" -> "Options" -> "Dependencies" -> add a new dependency and use the ID of MCE (or you can simply browse to the location where your downloaded MCE folder is saved)

## 2. Choose an armor mesh you would like to use

### Option 1 - Create an armor mesh (3D model) weight painted for the Arma Reforger character rig
I am not familiar with the process of creating armor models for Arma Reforger
But there should be many tutorials covering this subject (including the official Bohemia Interactive documentation)
Make sure that your armor mesh has collision, you can use this free Blender addon to create colliders: https://github.com/Weisl/simple_collider

### Option 2 - Use an existing armor model (either from base game or some other mod)
Make sure that this mesh has collision

### Proper collision example
When you open your armor model (.xob) in Enfusion Workbench, it must have at least 1 collider - otherwise it will NOT protect any body parts against melee damage:
![Armor Collision](Guide%20Images/Armor%20Collision.jpg)

## 3. Copying one of the MCE Armor Prefabs
Properly configured MCE armor prefabs can be found in this folder:
Melee Combat Extended\Prefabs\Characters\MCE Armor VS Melee Damage\

These prefabs already include all the components and settings required for the armor to protect against melee damage

MCE currently comes with sample armor items for 4 equipment slots:
- Jacket
- Armored Vest
- Pants
- Helmet

## 4. Changing the mesh and equipment slot
Armors are slightly different compared to weapons, they use 2 separate meshes

### Mesh of the lootable item
Select MeshObject component in the prefab's hierarchy and change the mesh in the Object parameter

### Mesh of the armor equipped on the character's body
Select BaseLoadoutClothComponent, change Worn Model and Item Model parameters
You might want to change the depth and offset parameters here, for examples look at armor items from the base game or other mods

### Equipment slot
BaseLoadoutClothComponent -> Unsorted -> AreaType

## 5. Configuring defensive stats
In base game armor does not work VS melee damage at all
MCE fixes the issue and relies on a custom HitZone script to achieve this

### Armor hitzone setup
SCR_ArmorDamageManagerComponent -> Unsorted -> Additional hit zones
For the armor to work against melee damage the list of "additional hit zones" must contain SCR_MCE_ArmorHitZone:
![MCE Armor Hit Zone](Guide%20Images/MCE%20Armor%20Stats%201.jpg)

Otherwise, if the armor piece has SCR_ArmorDamageManagerComponent with default SCR_ArmorHitZone it will only protect against kinetic damage (bullets)

### Choosing body parts (hit zone groups) to be protected
Scroll down to Additional hit zones/"Your hit zone name"/ProtectedHitZoneGroups parameter:
![Protected Hit Zone Groups](Guide%20Images/MCE%20Armor%20Stats%202.jpg)

Add all hit zone groups that you want your armor piece to protect
For example, a jacket might protect:
- Both arms
- Upper torso
- Lower torso

### Melee damage VS armor explanation
MCE supports multiple armor layers protecting the same body part (hit zone group)

Here is the damage calculation for the hit that targets the head, and melee attack raycast goes through the armored vest and the helmet:
![Melee Damage VS Armor Calculations](Guide%20Images/Melee%20Damage%20Armor%20Calculations.jpg)
As a result, only helmet protects the head, because it protects the hit zone group the body part belongs to
- The console log with melee damage calculation will be shown if you hit one of the 3 static NPCs in the MCE test map with a melee weapon while playing in Enfusion Workbench
- This is because a custom SCR_MCE_MeleeDamageMonitorComponent was added to these character prefabs, so they basically act as target dummies
- You can use them to test your own weapons and armor

### Defensive stats explanation
To adjust how much an armor piece reduces incoming melee damage you can manipulate 4 parameters in SCR_ArmorDamageManagerComponent:
- Base Damage Multiplier (0.6 value means 40% damage reduction)
- Melee multiplier (multiplicative with Base Damage Multiplier)
- Damage Reduction (flat damage reduction, applied after multipliers)
- Damage Threshold (if incoming damage is lower than this value, it is ignored, applied after Damage Reduction)
If a melee hit goes through 2 or more armor pieces that protect the targeted body part, their defensive values are applied one after another

### Explanation of protection vs kinetic damage (bullets)
This section has nothing to do with MCE and works the same in the base game, but I chose to include it, since it is not very obvious how the armor works in Arma Reforger (as of patch 1.4)
m_fPassedDamageScale parameter in the SCR_ArmorDamageManagerComponent reduces the incoming kinetic damage in addition to Base Damage Multiplier and Kinetic multiplier (they are stored in SCR_ArmorHitZone)
0.5 Passed Damage Scale means 50% reduced kinetic damage taken
But still do your own research and do not take my words for granted if you want to be 100% sure about how kinetic damage works

## 6. Changing the name, description and tooltip
Select InventoryItemComponent in the armor prefab
In Attributes/ItemDisplayName you will find:
- Name
- Description
- Item Hints (tooltips with defensive stats that you see when hovering over MCE armors)
Example of the armor tooltip:
![MCE Armor Tooltip](Guide%20Images/MCE%20Item%20Stat%20Tooltips.jpg)
