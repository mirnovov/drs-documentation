# Freeware - original 2004 release

## Freeware - original 2004 release

Getting doukutsu-rs to run with the original, freeware version of Cave Story is simple. doukutsu-rs is designed to work seamlessly with the original 2004 release of Doukutsu Monogatari.

First, you'll need to obtain the original game files. The recommended version is the 1.0.0.6 release, either in the original Japanese or with the Aeon Genesis (AGTP) English fan translation.

Here's where you can download the game:

* **Original Japanese 1.0.0.6:**
  * Directly from Studio Pixel (the game's creator): [https://studiopixel.jp/binaries/dou\_1006.zip](https://studiopixel.jp/binaries/dou_1006.zip)
  * Mirror on Cave Story Tribute Site: [https://www.cavestory.org/downloads/dou\_1006.zip](https://www.cavestory.org/downloads/dou_1006.zip)
* **Pre-patched with Aeon Genesis English Translation (AGTP):**
  * Cave Story Tribute Site: [https://www.cavestory.org/downloads/cavestoryen.zip](https://www.cavestory.org/downloads/cavestoryen.zip)

You can also find the Aeon Genesis English translation patch by itself, but it's distributed as a Windows executable (.exe), so applying it might be a little more involved if you aren't on Windows (you'll need something like Wine). So, the pre-patched version from Cave Story Tribute Site is generally more convenient. You may also find the pre-patched version on Cave Story Tribute Site.

Other versions, such as NXEngine-evo, CSE2, and earlier builds of the freeware release should also work, down to build 0.9.0.6.

The first time you run doukutsu-rs, it will automatically extract the necessary game assets from the original executable and place them into a new folder called `data` next to `doukutsu-rs` executable. Note that location of the `data` directory is platform-specific - please refer to the platform-specific guide for details. It's important to keep both `doukutsu-rs` and the original `Doukutsu.exe` in the same folder during this initial setup. After the `data` folder is created, `Doukutsu.exe` can be removed.

Other translations, and earlier game releases, should work out of the box, but may require extra steps. You can check [https://www.cavestory.org/downloads/](https://www.cavestory.org/downloads/) for more downloads.

### Mod Support

It's important to understand that most freeware Cave Story mods that alter the game's behavior won't work directly with doukutsu-rs. This is because many of these mods rely on one of two techniques:

1. **Binary Patches:** These mods directly modify the original `Doukutsu.exe` file, changing the game's code at a very low level. Because doukutsu-rs is a completely separate program, these changes won't be present.
2. **DLL Injection:** This technique involves adding extra code (in the form of a `.dll` file) that "injects" itself into the running game. Again, because doukutsu-rs is a different program, this injected code won't have any effect.

However, mods that _only_ change the game's _data files_ (graphics, sounds, maps, etc.) without modifying the core game code _will_ work perfectly fine with doukutsu-rs. A good example of this is the Cave Story Randomizer ([https://randovania.org/games/cave\_story/](https://randovania.org/games/cave_story/)).

Modified freeware data files, such as those bundled with "NXEngine-evo" and "CSE2", are also supported and will work without issues.
