# Guide: Melee Weapon Prefab Configuration

## 1. Setting up Melee Combat Extended as a dependency for your mod

This step is required to be able to access the functionality of custom MCE scripts from within your mod
Make sure that you have downloaded MCE using Arma Reforger's mod browser

### When creating a new Enfusion Workbench project (mod)
![MCE as dependency](Guide%20Images/MCE%20as%20dependency.jpg)

### When you already have an existing project (mod)
With your project open click "Workbench" -> "Options" -> "Dependencies" -> add a new dependency and use the ID of MCE (or you can simply browse to the location where your downloaded MCE folder is saved)

## 2. Copying the MCE Base Weapon Prefab

MCE Base Weapon prefab can be found here:
Melee Combat Extended\Prefabs\Weapons\Core\MCE_Weapon_Base.et

This prefab already includes all the components required for the melee weapon to work:
![Blender Model Orientation](Guide%20Images/Melee%20Weapon%20Stats.jpg)

## 3. Changing the mesh
Select MeshObject component in the prefab's hierarchy

Change it to the mesh you have created for your new weapon

It is highly recommended to follow the guide for creating new melee weapon models if you want your weapon to work properly with MCE custom animations and scripts:
[Guide: Creating New Custom Melee Weapon Models](Guides/creating-new-weapons.md)

## 4. Changing the combat stats (Damage, Range, Attack Speed...)
All melee weapon combat stats are stored in the custom SCR_MCE_MeleeWeaponProperties component in the weapon prefab

- "Global" section is inherited from the base game MeleeWeaponProperties component, it contains Damage, Range and Accuracy stats for the MCE Heavy Attack
- "MCE Heavy Attack" and "MCE Light Attack" sections are self-explanatory

### Accuracy
Accuracy refers to the radius of the raycast which is used for melee attack hit detection
If you increase the radius too much it will be very difficult to precisely hit the desired body part
Therefore, 0.1 Accuracy value is arguably better than 0.3

### Attack Speed
Attack speed controls the animation speed of the wind-up phase of the attack animation
1 means default animation speed
1.5 means the wind-up of the attack is sped up by 50%

### Animation Type
Currently only Stab and Cut animations are implemented, more attack types might be added in the future

### Ragdoll Multiplier
This parameter controls how much the physics will impact the victim of the melee hit (including situations when the victim is already dead)
Higher values lead to funny results

### Use Bayonet Sound
For blunt weapons you might want to turn this off (like the crowbar and wooden mallet in MCE, for example)

## 5. Changing the name, description and tooltip
Select InventoryItemComponent in the weapon prefab
In Attributes/ItemDisplayName you will find:
- Name
- Description
- Item Hints (tooltips with damage and attack type that you see when hovering over MCE weapons)
Item name that you see when you are looking at it in the world (not in the inventory) can be changed in the WeaponComponent:
Unsorted -> UIInfo/Name

## 6. Weapon slot type
If you want your new melee weapon to be equipped in the "pistol" slot, put "secondary" instead of "primary" in WeaponComponent -> Unsorted -> WeaponSlotType