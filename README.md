# RoR2ShareItemMod
RoR2 - Gives a copy of each picked up item to every player.

Only share non-lunar and non-void items. You can get items even after you die. Only host need this mod.

## Installation

Since v1.2.1.0, the developers refactor codes into RoR2.dll.

Replaces RoR2.dll in:
\steamapps\common\Risk of Rain 2\Risk of Rain 2_Data\Managed\RoR2.dll

**Backup current dll if you want to restore**

## DIY

Use dnSpy. My version is v6.0.4.

NOTE: Don't copy the dll to another folder before editing, which will cause compile fail. Backup and edit the file in `Managed` folder.

Edit RoR2.dll -> RoR2 -> ItemDef -> AttemptGrant()
Change:
```
inventory.GiveItem((pickupDef != null) ? pickupDef.itemIndex : ItemIndex.None, 1);
```
Into:
```
if (pickupDef.isLunar || pickupDef.itemTier == ItemTier.VoidTier1 || pickupDef.itemTier == ItemTier.VoidTier2 || pickupDef.itemTier == ItemTier.VoidTier3 || pickupDef.itemTier == ItemTier.VoidBoss)
{
  inventory.GiveItem((pickupDef != null) ? pickupDef.itemIndex : ItemIndex.None, 1);
}
else
{
  foreach (PlayerCharacterMasterController playerCharacterMasterController in PlayerCharacterMasterController.instances)
  {
    playerCharacterMasterController.master.inventory.GiveItem((pickupDef != null) ? pickupDef.itemIndex : ItemIndex.None, 1);
  }
}
```

Then save all.

## Thanks
Thanks to [the project](https://github.com/Solst1c3/SharedItemPickup) created by Solst1c3.
