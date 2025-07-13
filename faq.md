---
description: Comprehensive answers to common questions
---

# FAQ

## General

### What is this project?

The answer to this question is on the home page [of our website](https://doukutsu.rs):

> **A reimplementation of Cave Story engine with many quality-of-life improvements.**

Please note that doukutsu-rs **is not a decompilation**, as it's written from scratch and does not contain the source code of the original game (unlike CSE2[^1], which is actually a fan decompilation of a freeware executable).

**doukutsu-rs** was originally started as a Rust learning project and meme, but after a while it evolved into a drop-in replacement for the major editions of the game (the original 2004 freeware edition, Cave Story+ for PC and Cave Story+ for Switch).

While doukutsu-rs **tries to be faithful** in behaviour to the original game, it **doesn't aim to be an exact copy** of it. For example, doukutsu-rs lacks bugs that exist in the vanilla version of the game, so there are some differences in behaviour (e.g. [issue #278](https://github.com/doukutsu-rs/doukutsu-rs/issues/278#issuecomment-2403594236)), but also includes features such as cutscene skip, lighting effects, subpixel scrolling and V-Sync support.

Also some features are not planned to be implemented such as Steam achievements, leaderboard, coop offscreen or floor particles in Sand Zone.

### Where are the saves/settings/logs?

You can open the folder with saves and settings via the menu: `Options` -> `Advanced` -> `Open user data directory`.

If you created a portable user data directory, the saves will be in the `user` folder next to the doukutsu-rs executable.

Otherwise, the location of the user data depends on the platform:

* on **Windows**: `%LOCALAPPDATA%\doukutsu-rs\data\` (that is `AppData\Local\doukutsu-rs\data\`);
* on **macOS**: `~/Library/Application Support/doukutsu-rs/saves`;
* on **Linux**:
  * if installed from **Flatpak**: `$XDG_DATA_HOME/doukutsu-rs/` (usually this is `$HOME/.var/app/io.github.doukutsu_rs.doukutsu-rs/data/doukutsu-rs/data`);
  * if you downloaded **the `.elf` executable file**: `$HOME/.local/share/doukutsu-rs/`;
* on **Android**: see [#how-to-open-game-user-data-directory-on-android](faq.md#how-to-open-game-user-data-directory-on-android "mention")

### How to open game/user data directory on Android?

If you have an app on your device called `Files` (app id `com.google.android.documentsui`), open it, swipe from the left edge to the right (or press the `≡` menu icon) and select `doukutsu-rs` from the list. Saves will be in the `saves` folder, game data in the `data` folder, logs in the `logs` folder.

If there is no such application, then you can install [shortcut](https://play.google.com/store/apps/details?id=com.marc.files) for it and repeat with it the same actions described in the previous paragraph.

If you don't want to install this shortcut, then install Material Files ([Google Play](https://play.google.com/store/apps/details?id=me.zhanghai.android.files)|[F-Droid](https://f-droid.org/en/packages/me.zhanghai.android.files/)|[Github Releases](https://github.com/zhanghai/MaterialFiles/releases)) by Hai Zhang. Once you open it, click on the menu icon `≡` -> `Add storage` -> `External storage` -> `≡` -> `doukutsu-rs` -> `USE THIS FOLDER` -> `ALLOW`. The `files` folder will appear in the menu, clicking on it will take you to the data dir doukutsu-rs.

## Features Support

### Are the mods supported?

Only mods that modify game data files (textures, maps, text scripts, music, sounds) and don't modify the original game executable are supported. Cave Story+ mods and challenges are also supported, but there are [graphics issues](https://github.com/doukutsu-rs/doukutsu-rs/issues/118) for some mods.

### Is multiplayer supported?

Local co-op is **available on PC**, but is **missing on Android**, as the engine doesn't support gamepad and keayboard control on Android.

However, [the port for Retroarch](https://github.com/DrGlaucous/doukutsu-rs-nm/releases/tag/RA-1.2.0) is stated by the developer to support local coop.

### Are saves from CS+ supported?

> I copied the CS+ save file, but only the first slot is loaded/saved.

doukutsu-rs uses a freeware compatible save format, so each slot is stored in a separate file. Cave Story+ saves are stored in a single file, so doukutsu-rs only reads the first slot from this file, and writes only the first slot to it.

However, work on adding support for CS+ and CS+ Switch saves has already [started](https://github.com/doukutsu-rs/doukutsu-rs/pull/317).

### Is a fixed window ratio (e.g. 4:3 as in the freeware) or resolution supported?

No, but [the DrGlaucous's fork](https://github.com/DrGlaucous/doukutsu-rs-nm) supports fixed window ratio. However, it doesn't have prebuilts, so you'll have to build it from the source code. See [initial-setup-and-compiling](modders-handbook/initial-setup-and-compiling/ "mention") (don't forget to add the `--release` argument to `cargo build`).

## Platform Support

### Is controller supported on Android?

Currently, the only control method available for native Android builds is touch screen controls. Keyboard or gamepad controls are not supported.

However, you can use [doukutsu-rs port for RetroArch](https://github.com/DrGlaucous/doukutsu-rs-nm/releases/tag/RA-1.2.0), which supports controller. This is currently the only reliable solution to this problem. Information on usage and installation can be found in the [port repository](https://github.com/DrGlaucous/doukutsu-rs-nm/tree/retroarch-dev#use).

### Which platforms is doukutsu-rs available on?

doukutsu-rs is officialy supported on PC ([Windows 10+](#user-content-fn-2)[^2], Linux, macOS 10.12+) and Android 7+. The builds for these platforms are stable: release builds as well as nightly builds are available for them.

In addition, doukutsu-rs also has several experimental ports, such as the Nintendo Switch port. There are no fresh builds of the engine for experimental ports, due to the lack of active support for them by doukutsu-rs maintainers.

### You should make a port to the XYZ platform.

doukutsu-rs is available on the most common platforms, so **there are no plans** to port to other platforms yet.

### Why are there no new builds for Switch?

Due to the lack of active support for this platform from the engine maintainers, the toolchain used to build the engine for this platform are obsolete and can no longer be used. Due to the lack of time and desire of the maintainers to address this issue, new builds aren't available.

***

To delve into the technical aspect of the issue, the patched _Rust toolchain_ version <kbd>1.67.0</kbd> and _libc_ were used to build this port. Several years have passed since the port was added, and in that time this version of toolchain is no longer suitable for building doukutsu-rs, as some dependencies have set the minimum required compiler version <kbd>>=1.80</kbd>. Rolling back to earlier versions of the dependencies where this restriction was not present does not help, as one of the dependencies still requires a compiler version <kbd>>=1.70</kbd>.

**Why not just update the patched toolchain to the latest version?** As said before, lack of interest and/or free time of the doukutsu-rs maintainers.

**Why not to backport this dependency?** This one dependency will require backporting several crates that depend on it. Besides, this is a temporary solution until we have to update some dependency that breaks the build again due to an outdated toolchain. Therefore, updating the toolchain seems to be a more rational option.

### The controls on Android are awkward, how do I customise them? How to make the buttons bigger or change their position?

No way. You cannot change the location of touch screen controls and their size. You can only disable their display in `Options` -> `Controls` -> `Display touch controls` -> `OFF`.

***

Although you can try changing the size and position of the buttons in the source code and rebuild the executable file, but this is very inconvenient and will take some time to find the right values.

If you're ready for it, in the file [src/input/touch\_controls.rs](https://github.com/doukutsu-rs/doukutsu-rs/blob/2f1159c14f671bb77e845d46b48de9fcfb5eb814/src/input/touch_controls.rs#L100-L146) on line 100-146 you can adjust the location of controls (the first argument of the `add_rect_tinted` function is an X-axis coordinate, and the second argument is a Y-axis coordinate), and in the file [src/input/touch\_player\_controller.rs](https://github.com/doukutsu-rs/doukutsu-rs/blob/2f1159c14f671bb77e845d46b48de9fcfb5eb814/src/input/touch_player_controller.rs#L81-L239) on line 81-239 you can adjust the zones for registering button presses (the zones in which the game will count pressing a particular button).

### When will native gamepad or any other thing support be added to the Android port?

Someday. ¯\\\_(ツ)\_/¯

## Game Info

### What are the differences between the difficulty levels?

* Easy - damage dealt by enemies is halved.
* Hard - no life capsules and missile launcher.

***

## Still have questions?

&#x20;Feel free to ask them on the project's [Discord server](https://discord.gg/fbRsNNB) or [Github issues](https://github.com/doukutsu-rs/doukutsu-rs/issues/new/choose).

[^1]: Cave Story Engine 2

[^2]: Although Windows 7 has been chosen by the community to be supported and doukutsu-rs can be built for it, there are no release builds targeting this platform.
