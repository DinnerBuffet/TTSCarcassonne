# Carcassonne
![Carcassonne](https://github.com/DinnerBuffet/TTSCarcassonne/blob/master/workshop%20splash.jpg)

NOTE: I am no longer actively updating this mod. Others are welcome to branch the code and continue updating it. mmann78 has started a promising branch with lots of new changes. I recommend following that branch for future updates: https://github.com/mmann78/TTSCarcassonne

The game Tabletop Simulator is required to play the mod:

http://store.steampowered.com/app/286160/Tabletop_Simulator/

~~Workshop item for the Tabletop Simulator mod:~~

~~http://steamcommunity.com/sharedfiles/filedetails/?id=779900330~~

The workshop item has been taken down. You will now have the download the save file yourself. The current version is available here:

https://drive.google.com/uc?export=download&id=1wGsemzGAnhkjniPFhM9rOHjYS9nDWhwb

On Windows, move the file to your Windows user's Documents\My Games\Tabletop Simulator\Saves folder

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

Contains all global TTS entry points for the mod. All code begins execution here, with the exception of some events that run on objects (ie. control panels + a couple other objects).

Note that buttons created by this code can provide for additional entry points (which are stored in other files).

### setup_game.ttslua

Contains code related to setting up the game. Basically, everything that happens when you click the "Start Game" button.

### game_logic.ttslua

Contains most of the logic that drives the game's rules.

### state_machine.ttslua

Controls the flow of the game by giving each part of a turn a distinct "state". This allows most functions in the game logic to simply call nextState() without needing to know what the next state is. This also allows the game to be restored to this state when loaded from a save file.

### move_validation.ttslua

Contains code related to validating object movement made in the game.

### feature_map_management.ttslua

Contains code related to the feature mapping. Feature mapping relies on a few different sets of global tables, such as tileGrid, featureList, and linkedFeatures. Feature mapping makes the script run faster by storing a condensed aggregated set of data for all of the tiles in play.

*tileGrid* - a 2-dimensional table showing information about the tile + featureMap that exists in a particular x-y coordinate. The middle tile is represented as 17-17 (It's not 0-0 because I had issues serializing a table with negative indexes)

*featureMap* - Contains a map of positions within this grid location to featureNums. The locations are defined here: https://github.com/DinnerBuffet/TTSCarcassonne/blob/master/tile_positions.jpg

*featureList* - An aggregated summary of distinct features indexed by featureNum.

*linkedFeatures* - distinct features which maintain some kind of connection to other distinct features are defined here.

Currently, this does not contain *all* of the data necessary for the game's logic, and the script may still need to retrieve some of this data straight from the tile and/or traverse to nearby tiles to retrieve data. I hope to eventually store all of the data globally.

### tile_traversal.ttslua

Contains code which can recursively traverse adjacent tiles and retrieve aggregated data about features spanning multiple tiles.

This code is mostly legacy and is not well-maintained. Most real-time traversals were made obsolete when the feature map was created. Some of these use-cases will eventually be phased out while others (such as re-creating the featureMap when a tile is removed) will require this code long-term.

### hint_markers.ttslua

Contains code related to the hint markers that are shown when picking up a tile or meeple.

### ai.ttslua

Contains all of the code related to running an AI player.

Warning: This file contains a ton of duplicate code that needs to be cleaned up. If you modify any of the Easy code, you will also need to modify corresponding Hard code until it is refactored.

### localization.ttslua

Contains code and data related to localizing the mod in another language.

### json.ttslua

Third-party JSON code used for de-serializing save files quicker than the built-in function.

### debug.ttslua

Contains debug code. There are no entry points to this code built into the mod. To execute these functions, you will need to create your own. I personally have an object that I save in my "Saved Objects" that creates buttons for executing them.

### control_panel_x.ttslua

Each page of the control panel references control_panel_common.ttslua, which has all common code. The entry points to the code are OnLoad and (in some cases) onPlayerChangedColor.

Note that this code may create buttons which provide additional entry points.

### xml

Contains XML UIs, mainly for the control panel.

### tile_data

raw metadata used to represent the characteristics of the tile. For details see: https://github.com/DinnerBuffet/TTSCarcassonne/blob/master/tile_data/README.md
