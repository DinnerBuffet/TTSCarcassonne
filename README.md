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

## Recommended packages

https://atom.io/packages/minimap

https://atom.io/packages/minimap-git-diff

https://atom.io/packages/linter

https://atom.io/packages/Sublime-Style-Column-Selection
