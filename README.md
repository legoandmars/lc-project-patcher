﻿# Lethal Company Project Patcher

> This tool is still in development and is quite experimental, but should be usable.

This tool fills in a unity project with functional assets so it can be used for Lethal Company modding.

This tool does **not** distribute game files. It uses what is already on your computer from the installed game.

## What does it do?

- Installs required packages, and enforces specific versions for them
- Updates various project settings:
  - Tags
  - Layers
  - Physics settings
  - Time settings
  - Navmesh settings
- Strips generated netcode inside of game scripts so they can compile in Unity
- Fixes missing script references
- Fixes missing shaders on materials
- Fixes broken scriptable objects
- Copies needed DLLs from the game directly
- Exports game assets with an embeded version of Asset Ripper
- Sets up a BepInEx environment to test patches and plugins in-editor
- Can load up normal plugins in-editor
- Supports disabling domain reloading in-editor for faster compile times
- And much more!

![image](./Images~/preview_2.png)

## Requirements

- About 900 MB for the asset ripper export
  - There is a toggle to delete the export after the patcher is done
- About 900 MB for the copied files from that export into the project
- [Git](https://git-scm.com/download/win)
- [Unity 2022.3.9f1](https://unity.com/releases/editor/archive)

## Installation
#### Using Unity Package Manager

1. Make sure you have git installed: https://git-scm.com/download/win
    - After installing, restart Unity
2. Open the Package Manager from `Window/Package Manager`
3. Click the '+' button in the top-left of the window
4. Click 'Add package from git URL'
5. Provide the URL of the this git repository: https://github.com/nomnomab/lc-project-patcher.git
6. Click the 'add' button

## Usage

1. Create a new Unity project
    - Use version [2022.3.9f1](https://unity.com/releases/editor/archive)
    - Use the 3D (HDRP) template
2. Open the tool from `Tools/Nomnom/LC - Project Patcher`
    - This will create some default folders for you when it opens
> At this point if you have the DunGen asset, or any other asset, import it now and move it into `Unity\AssetStore`

3. Assign the Game's data directory path at the top
    - Example being `C:\Program Files (x86)\Steam\steamapps\common\Lethal Company\Lethal Company_Data`
4. Click the `Run Patcher` button
    - This process *will* take a while, so be patient
    - The editor may restart a few times, this is normal
    - When it asks about the New Input System and switching backends, click `Yes`
7. Now you should have a nice template to work from!

## BepInEx Usage

You can make plugins directly in the editor like normal.

> I have not tested *patchers*, so use them with caution!

If you want to add some normal plugins, you'll have to navigate outside of `Assets` for this, and next to it is a folder called `Lethal Company`.

This is a dummy folder that houses the normal BepInEx root and a fake game data structure so it can initialize before I route it to the actual game files.

## FAQ

### Why can I not delete a plugin from the plugins folder?

If a plugin is loaded while playing the game in-editor, then it will stay loaded forever. This is just how Unity handles their dll hooks.

If you need to remove a plugin, then close unity first, then delete it.

The same steps go for anything else that BepInEx has a hook on, such as its log files.

### Why is my audio doubling?

For some reason the diagetic audio mixer's master group has effects on by default. The main reason why there is an echo
is due to the `Echo` effect on it. 

If the auto-patcher didn't work, you can remove this effect by:

1. Opening the `Diagetic` audio mixer
2. Clicking on the `Master` group
3. Going into the inspector and navigate to where `Echo` is
4. Click the gear in the top-right of the effect and click `Bypass`
5. Profit

### How can I make Unity not take three years to compile scripts when pressing play?

> Make sure you understand what you have to do manually if domain reloading is disabled
> 
> https://docs.unity3d.com/Manual/DomainReloading.html

This is straightforward, as long as your own plugin code supports it.

1. Open the `Edit\Project Settings` menu
2. Go to the `Editor` tab
3. Check `Enter Play Mode Options`
4. Check `Reload Scene`

Now it will take like a second to press play instead of a minute 😀

### Why doesn't my plugin get found from inside a folder with an assembly definition?

I only check the main Assembly-CSharp dll for plugins at the moment.

## Useful packages

- Parrel Sync - https://github.com/VeriorPies/ParrelSync.git?path=/ParrelSync
  - This lets you run multiple instances of the project at once to test LAN without building the game.

- Editor Attributes - https://github.com/v0lt13/EditorAttributes.git
  - This is a nice package that adds some useful attributes for the inspector

## Credits

- Asset Ripper - https://github.com/AssetRipper/AssetRipper
  - Modified source - https://github.com/nomnomab/AssetRipper
- Asset Bundles Browser - https://github.com/Unity-Technologies/AssetBundles-Browser
- UniTask - https://github.com/Cysharp/UniTask
- UYAML Parser - https://gist.github.com/Lachee/5f80fb5cb2be99dad9fc1ae5915d8263
- MonoMod - https://github.com/MonoMod/MonoMod