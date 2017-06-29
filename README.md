# Sequencer 360 Audio

*[Unreal Engine plugin] Facebook 360 audio plugin (TBAudioEngine by Two Big Ears) and Sequencer integration*

## Introduction

This plugin allows connecting  360' audio layers/playlists to Level Sequence Actors, with fully automatic playback and synchronization. The plugin monitors the assigned reference sequence and automatically handles starting, pausing, stopping, seeking and playback rate changes. Playback rate changes due to global time dilation are also handled.

The plugin uses the Facebook 360 audio plugin (TBAudioEngine from here on), so you need that too. See https://facebook360.fb.com/spatial-workstation/ > Downloads > Rendering SDK.

## Usage

1. Install the TBAudioEngine plugin from the web page mentioned above
1. Download or clone this repository into your Plugins/ folder
1. In the editor, go to Edit menu > Plugins and make sure that both plugins are enabled; restart your editor if asked to
1. Locate the `Sequencer360Audio` class in the class browser (the panel on the left) and drop an instance to your level
1. In the Details panel of the newly created instance (see the tooltips for further details):
    1. `Audio Layers`: Define your TBE audio assets and their start times by filling this array
    1. `Reference Sequence`: Set this field to point to a Level Sequence Actor in your level. Playback will start when this level sequence starts playing and will stay synchronized with it.
    2. `Sequence Speed Change Handling`: Choose how to slow down or speed up the audio in case that the reference sequence playback rate is not 1.0.

## Notes

### Facebook 360 audio plugin

At least version 0.9.95 might fail to find its own DLL in packaged builds. You can fix this by adding the following line to Plugins/TBAudioEngine/Source/TBAudioEngine/TBAudioEngine.Build.cs:
```csharp
PublicDelayLoadDLLs.Add("TBAudioEngine.dll");
```
Alternatively, after packaging, you can also just move TBAudioEngine.dll from YourGame/Plugins/TBAudioEngine/Binaries/Win64 to YourGame/Binaries/Win64.

### UE versions

The plugin is created using UE 4.15. It is in itself fully compatible with 4.16, but it seems that at least version 0.9.95 of the Facebook 360 audio plugin does not package with 4.16!
