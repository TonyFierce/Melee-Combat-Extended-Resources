# Guide: How to Configure Bayonets to be Usable as Standalone Weapons

## 1. Setting up Melee Combat Extended as a dependency for your mod

This step is required to be able to access the functionality of custom MCE scripts from within your mod  
Make sure that you have downloaded MCE using Arma Reforger's mod browser

### When creating a new Enfusion Workbench project (mod)
![MCE as dependency](../Guide%20Images/MCE%20as%20dependency.jpg)

### When you already have an existing project (mod)
With your project open click "Workbench" -> "Options" -> "Dependencies" -> add a new dependency and use the ID of MCE (or you can simply browse to the location where your downloaded MCE folder is saved)

## 2. Copying one of the MCE bayonet prefabs

All 3 bayonets from the base game are usable as standalone melee weapons in MCE  
They can be found here:  
Melee Combat Extended\Prefabs\Weapons\Attachments\Bayonets

Prefabs in this folder already include all the components required for them to work both as bayonets and as standalone melee weapons:
![Bayonet Prefab](../Guide%20Images/Bayonet%20Prefab.jpg)
You can duplicate one of them into your mod and customize the settings depending on your needs

## 3. Following the guide about non-bayonet MCE weapon prefabs

This guide will not repeat the information found in the guide about setting up standalone MCE melee weapons  
It is HIGHLY recommeded to read that guide first:
[Guide: How to Configure Melee Weapon Prefabs](Guides/weapon-prefab-configuration.md)

## 4. Bayonet specific information

Most of the settings specific to bayonets are contained in the InventoryItemComponent

### Position of the weapon in the character's hands

Open InventoryItemComponent -> Attributes -> Item Animation Attributes  
Find "Animation IK Pose" parameter - it controls which IK pose is used for holding the weapon  
If you properly positioned your 3d model in Blender (or whichever software you used) and imported it into Workbench with the transform settings recommended in my guide, you should set the parameter to:  
Melee Combat Extended\Assets\Weapons\MeleeOneHanded\anims\anm\p_melee_1h_ik.anm

### Bayonet attachment settings and combat stats

Open InventoryItemComponent -> Attributes -> Custom Attributes  
Configure the attributes to make the bayonet work with whatever firearm you want it to  
This process would be exactly the same in the base game, MCE does not change anything here