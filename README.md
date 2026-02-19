# The-Devouring-Hour
Short Horror Game Project centered around looping hour system with in between tasks.

## Changes Made (02/11/2026)
- Added 3 new BluePrints
  - BP_InventoryComponent - Handles tracking the current item, adding, removing, cycling next, cycling previous item
  - S_InventoryItem - Structure that breaks into the item name, item description, and item icon
  - WBP_InventoryClipboard - the visual clipboard (VERY PRIMATIVE!!!! Will be updated to look better soon)

- Edits to BP_FirstPersonCharacter
  - ToggleInventory Logic
  - CycleInventory Logic
  - Inventory test items (for demo purposes)

- Next update, looking to have "pick-upable" objects to add to inventory
- Some tweaks to clipboard UI widget so it doesn't look as ugly and take up the entire screen (more clipboard-like)

## Changes Made (02/18/2026)
- Added new BluePrint Actor 'BP_PickupableBase'
  - The base is a duplicate of 'BP_InteractableBase', is detected by the first person character in the same way
 - Created new function 'UpdateHeldItem' in BP_FirstPersonCharacter
   - This function handles setting the correct static mesh for the currently held item
- Updated CycleInventory logic in BP_FirstPersonCharacter EventGraph to include UpdateHeldItem when cycling
  - Cycling through the clipboard using Q and E will change the player's currently held item respective to what is displayed on the clipboard
  - ToggleInventory Logic also includes UpdateHeldItem so that held item is shown regardless of if menu is up or not
- Added input mapping to key H to toggle currently held item visible/hidden
