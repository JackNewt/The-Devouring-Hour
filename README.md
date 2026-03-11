# The-Devouring-Hour
Short Horror Game Project centered around looping hour system with in between tasks.

# Olive Change Log
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

## Changes Made (02/24/2026)
A skeleton dialog system that supports both linear and branching conversations. Players can interact with interactable objects (will be NPCs) and make choices that lead to different dialog paths.

## Updates

### 1. S_DialogData (Structure)
Defines a single dialog entry.
- **SpeakerName**: Who is speaking
- **DialogText**: What they say
- **Responses**: Array of player response options
- **NextDialogIndices**: Array of dialog indices to jump to for each response

### 2. WBP_DialogBox (Widget Blueprint)
The UI that displays dialog on screen.
- Shows speaker name and dialog text
- Displays response buttons or continue button based on dialog type
- Manages dialog flow and progression

### 3. BP_DialogueTrigger (Actor Blueprint)
Interactable actor placed in the world that starts dialog.
- Implements BPI_Interactable interface
- Contains DialogSequence array with all dialog entries
- Spawns dialog widget when player presses E

## How It Works

### Linear Dialog
1. Player interacts with trigger
2. Dialog displays with Continue button
3. Clicking Continue advances to next dialog
4. Ends when reaching the last entry

### Branching Dialog
1. Player interacts with trigger
2. Dialog displays with 1-3 response buttons
3. Clicking a response jumps to specified dialog index
4. Can branch to different conversation paths
5. Ends when reaching a dialog with no next index

Olive Change Log
Changes Made (02/11/2026)

Added 3 new BluePrints

BP_InventoryComponent - Handles tracking the current item, adding, removing, cycling next, cycling previous item
S_InventoryItem - Structure that breaks into the item name, item description, and item icon
WBP_InventoryClipboard - the visual clipboard (VERY PRIMATIVE!!!! Will be updated to look better soon)


Edits to BP_FirstPersonCharacter

ToggleInventory Logic
CycleInventory Logic
Inventory test items (for demo purposes)


Next update, looking to have "pick-upable" objects to add to inventory
Some tweaks to clipboard UI widget so it doesn't look as ugly and take up the entire screen (more clipboard-like)

## Changes Made (02/18/2026)

Added new BluePrint Actor 'BP_PickupableBase'

The base is a duplicate of 'BP_InteractableBase', is detected by the first person character in the same way


Created new function 'UpdateHeldItem' in BP_FirstPersonCharacter

This function handles setting the correct static mesh for the currently held item


Updated CycleInventory logic in BP_FirstPersonCharacter EventGraph to include UpdateHeldItem when cycling

Cycling through the clipboard using Q and E will change the player's currently held item respective to what is displayed on the clipboard
ToggleInventory Logic also includes UpdateHeldItem so that held item is shown regardless of if menu is up or not


Added input mapping to key H to toggle currently held item visible/hidden

## Changes Made (02/24/2026)
A skeleton dialog system that supports both linear and branching conversations. Players can interact with interactable objects (will be NPCs) and make choices that lead to different dialog paths.
Updates
1. S_DialogData (Structure)
Defines a single dialog entry.

SpeakerName: Who is speaking
DialogText: What they say
Responses: Array of player response options
NextDialogIndices: Array of dialog indices to jump to for each response

2. WBP_DialogBox (Widget Blueprint)
The UI that displays dialog on screen.

Shows speaker name and dialog text
Displays response buttons or continue button based on dialog type
Manages dialog flow and progression

3. BP_DialogueTrigger (Actor Blueprint)
Interactable actor placed in the world that starts dialog.

Implements BPI_Interactable interface
Contains DialogSequence array with all dialog entries
Spawns dialog widget when player presses E

How It Works
Linear Dialog

Player interacts with trigger
Dialog displays with Continue button
Clicking Continue advances to next dialog
Ends when reaching the last entry

Branching Dialog

Player interacts with trigger
Dialog displays with 1-3 response buttons
Clicking a response jumps to specified dialog index
Can branch to different conversation paths
Ends when reaching a dialog with no next index


## Changes Made (03/10/2026)
Interactive computer screen system that allows players to interact with in-world UI displays. Players can view monitor screens with clickable interfaces and exit back to gameplay.
Updates
### 1. BP_Monitor (Actor Blueprint)
Interactable computer monitor placed in the world.
Components:

MonitorCamera: Camera component for viewing the screen up close
ScreenMesh: Static mesh (SM_Plane, 100×100cm) displaying the monitor screen
ScreenWidget: Widget component showing MonitorUI in world space (1024×1024 resolution)
UI_InteractPrompt: Widget showing interact prompt when player looks at monitor

Variables:

InUse (Boolean): Tracks if player is currently viewing the monitor
CachedPlayerController (Player Controller): Stores reference to player controller
CachedViewTarget (Actor): Stores original camera view target before switching
BlendTime (Float): Camera blend duration (default: 0.7 seconds)

OnInteract Event Logic:

Exiting Monitor (InUse = true):

Blend camera back to cached view target
Set input mode to Game Only
Hide mouse cursor
Set InUse to false


Entering Monitor (InUse = false):

Cache player controller and current view target
Activate MonitorCamera component
Blend camera to monitor (Self as view target)
Set input mode to UI Only with widget focus
Show mouse cursor
Set InUse to true

OnViewed Event Logic:

Shows interact prompt briefly when player looks at monitor
Prompt fades after 0.2 seconds

### 2. MonitorUI (Widget Blueprint)
The UI displayed on the computer screen.
Designer Layout:

Canvas Panel (root) - 1024×1024 resolution
Background (Image): Full-screen background image, exposed as variable
ExitButton (Button): Top-right "X" button to exit monitor view
TestButton (Button): Center test button for color demonstration

Event Graph Logic:

TestButton OnClicked:

Randomly changes Background color between red and blue
Uses Random Bool → Branch → Set Color and Opacity


ExitButton OnClicked:

Gets all BP_Monitor actors in scene
Calls OnInteract on first monitor to exit view
Uses Get Owning Player Pawn as instigator

### 3. ScreenWidget Component Configuration
Widget component settings for world-space UI display.
Settings:

Space: World (critical - not Screen space)
Widget Class: MonitorUI
Draw Size: 1024 × 1024 pixels
Transform:

Location: X=1, Y=0, Z=0 (slightly in front of mesh)
Rotation: Yaw=180° (faces outward)
Scale: X=0.1, Y=0.1, Z=1.0 (scales widget to match 100cm mesh)


Visible: Checked
Hidden in Game: Unchecked
