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

Check "Experimental: Insert other files specified in source code"

Under "Experimental: Base path for files you wish to #include", paste the path to your git folder

Recommended: Check "Experimental: Ignore files from outwith the TTS folder"

Now load Carcassonne from the workshop and make a new save file. Load that save file.

You should now be able to edit the code as separate files, rather than one big global file.

## Recommended plugins

https://atom.io/packages/minimap

https://atom.io/packages/minimap-git-diff

https://atom.io/packages/linter