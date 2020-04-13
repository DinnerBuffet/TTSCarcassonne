# Carcassonne
![Carcassonne](https://github.com/DinnerBuffet/TTSCarcassonne/blob/master/workshop%20splash.jpg)

Scripts, tile data, and files for the Tabletop Simulator mod:

http://steamcommunity.com/sharedfiles/filedetails/?id=779900330

The game Tabletop Simulator is required to play the mod:

http://store.steampowered.com/app/286160/Tabletop_Simulator/

You can see a rough outline of my road map at my Trello:

https://trello.com/b/3YNFvv9C/tts-carcassonne-road-map

## Instructions

Install Atom and the TTS plugin: http://berserk-games.com/knowledgebase/atom-editor-plugin/

In Atom, go to File->Settings->Packages->Click on settings for tabletopsimulator-lua

Check "#include other files"

Under "Base path for files you wish to #include", paste the path to your git folder

Now load Carcassonne from the workshop and make a new save file. Load that save file.

Now right-click your Project explorer on the left side and choose "Add project folder" and choose your git folder.

You should now be able to edit the code as separate files, rather than one big global file. Select Packages->Tabletop Simulator->Save and Play to update and load your save file with script changes.

## Recommended optional packages

https://atom.io/packages/minimap

https://atom.io/packages/minimap-git-diff

https://atom.io/packages/linter

https://atom.io/packages/Sublime-Style-Column-Selection

## Code guide

### global.ttslua

This is the main global script. It contains most global variables, plus includes for all other global scripts.

### helper_functions.ttslua

Contains functions that are not specific to Carcassonne, but are useful for all TTS mods.

### tts_events.ttslua

Contains all of the TTS entry points for the global scripts. All code begins execution here.

### setup_game.ttslua

Contains code related to setting up the game. Basically, everything that happens when you click the "Start Game" button.

### game_logic.ttslua

Contains most of the logic that drives the game's rules.

### state_machine.ttslua

Controls the flow of the game by giving each part of a turn a distinct "state". This also allows the game to be restored to this state when loaded from a save file.

### move_validation.ttslua

Contains code related to validating object movement made in the game.

### feature_map_management.ttslua

Contains code related to the "feature map", which is an aggregated storage of data for all of the tiles in play.

Currently, this does not contain *all* of the data, and the script may still need to retrieve some of this data straight from the tile. I hope to eventually store all of the data globally.

### tile_traversal.ttslua

Contains code which can recursively traverse adjacent tiles and retrieve aggregated data about features spanning multiple tiles.

This code is mostly legacy and is not well-maintained. Most real-time traversals were made obsolete when the feature map was created. Some of these use-cases will eventually be phased out while others (such as re-creating the featuremap when a tile is removed) will have to stay.

### hint_markers.ttslua

Contains code related to the hint markers that are shown when picking up a tile or meeple.

### ai.ttslua

Contains all of the code related to running an AI player.

Warning: This file contains a ton of duplicate code that needs to be cleaned up. If you modify any of the Easy code, you will also need to modify corresponding Hard code until it is refactored.

### localization.ttslua

Contains code and data related to localizing the mod in another language.

### control_panel_x.ttslua

Each page of the control panel references control_panel_common.ttslua, which has all common code.

### json.ttslua

Third-party JSON code used for de-serializing save files quicker than the built-in function.

### debug.ttslua

Contains debug code. There are no entry points to this code built into the mod. To execute these functions, you will need to create your own. I personally have an object that I save in my "Saved Objects" that creates buttons for executing them.
