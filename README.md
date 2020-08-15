# RoR2ShareItemMod
RoR2 - Gives a copy of each picked up item to every player.

## Installation
Replaces Assembly-CSharp.dll in:
\steamapps\common\Risk of Rain 2\Risk of Rain 2_Data\Managed\Assembly-CSharp.dll

**Backup current dll**

## DIY
Edit Assembly-CSharp.dll -> RoR2 -> GenericPickupController -> GrantItem() -> line 214
Change:
```
inventory.GiveItem((pickupDef != null) ? pickupDef.itemIndex : ItemIndex.None, 1);
```
Into:
```
if (this.pickupIndex.IsLunar())
{
  inventory.GiveItem((pickupDef != null) ? pickupDef.itemIndex : ItemIndex.None, 1);
}
else
{
  foreach (PlayerCharacterMasterController playerCharacterMasterController in PlayerCharacterMasterController.instances)
  {
    playerCharacterMasterController.master.inventory.GiveItem(this.pickupIndex.itemIndex, 1);
  }
}
```

## Thanks
Thanks to [the project](https://github.com/Solst1c3/SharedItemPickup) created by Solst1c3.
