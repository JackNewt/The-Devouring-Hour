# The-Devouring-Hour
Short Horror Game Project centered around looping hour system with in between tasks.


## - 2026-02-16
### Added
- Inventory system with scrollwheel compatability
- Data Asset template for making inventory items
- Added two new functions to Interactable interface
    - IsPickup (returns boolean)
    - GetItemData (returns Data Asset)
- Two temporary items (blue key and red box)
- Clear inventory function that wipes entire inventory
- Clear inventory item function that removes currently selected item

### Changed
- BP_InteractableBase now takes two instance editable variables
- Tweaked interaction in FirstPersonCharacter to check if BP_InteractableBase is also a pickup item
