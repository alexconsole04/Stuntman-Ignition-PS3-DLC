<img width="2304" height="1296" alt="PS3-DLC-11-12-2026" src="https://github.com/user-attachments/assets/f37406a7-066d-4f89-b1cb-eaba88e6ada8" />

A PlayStation 3 port of Stuntman Ignition's DLC that was only released on Xbox 360. This unlocks the Vehicle Pack cars and ports all of the Director's Cut missions from the original Xbox 360 package file.

# AI DISCLAIMER
This port was made with the assistance of Claude Opus 5.5, it helped with file conversion due to lack of resources or information available regarding this game, but debugging and tests were all done by me. If you are not comfortable with AI assisted projects, please do not use this project. If this disclaimer disappoints you, I apologize.

# Information
Stuntman Ignition received DLC where 4 cars seen in the Constructor Arena are now playable and 6 new missions were added in a separate menu on the Career menu for each of the 6 movies, aiming to provide an extra challenge. Likely due to poor sales, only the Xbox 360 version received this DLC and the PlayStation 3 version was excluded. The port aims to bring all the original data, converted for the PS3 version.

# How it Works
* Despite the PS3 version not receiving the DLC, most of the code was still left on the EBOOT, implying it was supposed to receive the same DLC, but never ended up happening. The game looks for a binary file (DCManifest.txt) where it contains the folder directory to locate a BANK file known as "packageInfo.bnk" that holds all the information for the Director's Cut menu. The file is the same as the 360 version so when brought over to "`dev_hdd0/game/GAMESERIAl/USRDIR/DIRECTORCUT1/`, the game constructs the menu with all the separate entries for each mission.

# What's Included?
All the files from the Xbox 360 package is included within the PKGs provided here. Most of the files from the base game were brought over since they shared the same models and textures. A few assets had to be converted over including level data and textures.
A modified EBOOT for the game to not only patch DLC vehicle cars to remain unlocked, but to also fix a few bugs with the PS3 version. Some include:

***The following addresses are for BLUS30073 1.11***

- **Crash when starting a Director's Cut mission.** The DC missions start loading a few frames sooner than normal missions. This makes it so the pause menu's font (`g:\fonts\Smudger2.bnk`) isn't ready in time to construct the pause menu flash movie from "pause.bnk", which results in the game crashing when the intro fly-through sequence tried to use it. The EBOOT now waits for the font before building the menu. (`0x2D5D4C` → code at `0x7E4D0` waits for the font (up to 1 s), then builds the menu.)
- **Crash when switching to a Director's Cut mission from another mission (most often after Aftershock).** When the game unloads a film's world, it leaves that worlds's textures registered. Base missions hide this by loading the next world into the same memory. DC missions put their own data there instead, so the game read garbage and crashed, or showed a level with all its graphics broken. The EBOOT now clears those leftover texture entries before a world is unloaded or loaded. (hooks at `0x243CEC` (world unload) and `0x25189C` (world load) → stubs at `0x4174E4` → cleanup at `0xC64C8`, which removes leftover entries with `0x34C090`)

# Known Issues
If level data loads too fast, skipping the stunt rundown will result in the level loading without the remaining data streamed for a brief moment. On RPCS3, this requires `Emulate HDD Read Speeds` toggled to prevent this issue. Whether this can happen on PS3 with an SSD is currently unknown.
<img width="2560" height="1392" alt="Screenshot 2026-11-11 212138" src="https://github.com/user-attachments/assets/4d4240ee-d91e-439b-9584-4fcb7d555e2a" />


# Downloads
The downloads are on the Release of this repository. The version has been ported to 1.11 already and contains all the data. Please download the PKG that corresponds to your game's serial. If you are using this mod on RPCS3, please also download the imported_patch.yml file included as the PPU hash is not compatible with the patches provided on the wiki. The game requires the Unlock FPS patch to prevent a crash when completing missions due to the replay buffer (5400) overflowing from high performance. (THIS IS A GAME BUG)

# How to Install?
If you are playing this on a PS3, this requires CFW or HEN to use.

* Download the PKG for whatever version your game is (eg: BLUS30073)
* If on RPCS3, drag and drop the PKG onto the RPCS3 window or `File>Install Packages`
* If on PS3, import into the HDD or install from a USB device
* To import the patch for RPCS3, place the file inside the patches folder on your installation or add the patches to an already existing one.

This will overwrite your original EBOOT for the game, either make a back-up or delete the gamedata and re-install the update.
I will continue to look more into this game for research purposes, enjoy.
