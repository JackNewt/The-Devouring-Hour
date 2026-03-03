# The-Devouring-Hour
Short Horror Game Project centered around looping hour system with in between tasks.

## - 2026-03-03
### Added
- New custom event in BP_KeyPad that, given a value (pill name), will generate a random 3 digit code and then change that value's current code to be the new random one
    - Added debug event on keyboard input "3" to test this functionality while the key pad is in focus
- Added new event tick handler in BP_KeyPad

### Changed
- Altered SubmitInput to be called whenever CurrentInput for the key pad reaches 3 digits

### Removed
- Removed functionality for the enter key calling SubmitInput
- Removed BPI_FocusInteractable (old SubmitInput calling system)


## - 2026-02-24
### Added
- New BPI that adds dynamic functionality for using the enter key on different focus-interactable objects
- Added ValidCodes string -> string map that contains valid codes (keys) that correspond to pills (values)
    - Ex. 1234 -> Pill 1
- Added enter key event in BP_FirstPersonCharacter
- Added documentation

### Changed
- SubmitInput now prints whether or not the input code corresponds to a pill
- Put movement and cursor toggling in it's own function "ToggleMovementAndCursor"

### Removed
- Removed submit button box collision and on click event


## - 2026-02-23
### Added
- Temporary key pad model
- Key pad blueprint that
    - Toggles camera view from first person to focus on the key pad upon interacting with the blueprint
    - Tracks clicks on buttons 1-9 and submit button
    - Has a submit button that prints the string of numbers the user input
- New line trace channel "InteractionTrace" that handles interaction checks

### Changed
- Tweaked interaction in FirstPersonCharacter to line trace by new trace channel "InteractionTrace" rather than "Visibility"
- Updated BP_InteractableBase to handle collision with new InteractionTrace channel


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