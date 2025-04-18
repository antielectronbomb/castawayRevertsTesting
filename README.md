## Introduction
Repository for plugins used on [castaway.tf](https://castaway.tf/)

The only entirely custom plugins here are ones credited only to random (chat-adverts, etc.). Everything else is a plugin made by someone else. The credits for said plugins can be found unmodified at the top of each plugin's .sp file.

This is not a comprehensive list of all plugins used on the server, however it does include all the most relevant ones to the player experience such as the map voting, team scrambling, and weapon revert plugins. 

## Compiling

To compile the plugins, download a recent Sourcemod stable version and merge the scripting directory into the scripting directory of this repo, then use `./compile.sh <plugin_name>` to compile each plugin. 

The reverts plugin has the following dependencies:
- 32 bit server/sourcemod - 64 bit sourcemod is not yet fully working for all plugins
- [TF2Items](https://github.com/nosoop/SMExt-TF2Items)
- [TF2Attributes](https://github.com/FlaminSarge/tf2attributes)
- [TF2Utils](https://github.com/nosoop/SM-TFUtils)
- [Source Scramble](https://github.com/nosoop/SMExt-SourceScramble) - Only required if using the memory patches (see Usage for more info)

No other plugins have any external dependencies, and the include files for the above dependencies are within this repo.

## Usage

The reverts plugin, after installing all the required dependencies, should work out of the box. 

### Memory Patches

There are a few revert patches within the revert plugin by default that utilize sourcescramble. These reverts are currently **linux server only** due to how the signatures are set up. If you have a windows server, they will not work whatsoever, and it is advised to not compile the plugin with them enabled.

To disable them, uncomment the following line near the top of the reverts.sp file before you compile:
```
//#undef VERDIUS_PATCHES
```

### Toggling Reverts

If you want to disable a specific weapon revert, you can create a config file called `reverts.cfg` in your `tf/cfg/sourcemod` folder. To disable a specific revert, you set the following:

```
sm_reverts__item_<name> 1/0
```
The below would disable the equalizer and sandman reverts
```
sm_reverts__item_equalizer 0
sm_reverts__item_sandman 0
```

To get the name to use, open up the reverts.sp file and find the `ItemDefine` block near the top inside of OnPluginStart, and use the second value in the params.

By default, all reverts are on. 

## Additional Credits
Some or all of these plugins have been modified in some way, sometimes in major ways. I do not claim credit for these plugins and all credit goes to their original creators.

* reverts.sp - This plugin is a heavily modified version of bakugo's [weapon revert plugin](https://github.com/bakugo/sourcemod-plugins), featuring lots of new reverts and different core plugin functionality. In order to add onto it I have occasionally taken some code from NotnHeavy's gun mettle revert plugin. It has since been deleted from github, however a copy of the code can be found unmodified in the scripting/legacy directory, and the gamedata in gamedata/legacy.
* votescramble - This is a heavily modded version of the votescramble from the [uncletopia plugin repo](https://github.com/leighmacdonald/uncletopia). Their version simply calls the game's autoscrambler, while my version reimplements the scramble logic from the ground up.
* nativevotes-* - This is sapphonie's [nativevotes-updates](https://github.com/sapphonie/sourcemod-nativevotes-updated), with some small modifications and bug fixes. Most notably, the nativevotes-mapchooser has a persistent mapcycle that remains between restarts.