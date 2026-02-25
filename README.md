# Dialog System - README

## Overview
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
