---
hidden: true
noIndex: true
---

# Lua API

doukutsu-rs includes a multiplayer-aware and event-based Lua API that lets you customize the behavior of Cave Story in many ways, allowing you to create stunning single and multi-player experiences. It's designed to be engine-agnostic as possible, for ease of implementation in other projects.

The API documentation is generated from TypeScript declarations and is available [here.](https://doukutsu-rs.github.io/api-docs/)

## Scripts

* `boot.lua` - runs in global context (so every loaded script inherits the global properties set in it). It is executed at game startup before the window is created and is a place where you can override certain settings such as window size and name, data paths and etc. Due to it's nature, it doesn't get reloaded when you use the `Reload Scripts` debugger option. **This is not sandboxed, so you need to be careful on what you expose in it to other scripts.** However it lets you load bytecode-based scripts and native extensions which is a very powerful feature (you can e.g., implement Discord rich presence that way) but also may crash the engine if used improperly.
* `scripts/*.lua` - sandboxed user scripts, note that their loading order isn't guaranteed and they run in separate contexts.

## Settings

There are various internal engine-specific settings that can be changed in doukutsu-rs, but many of them are considered out of scope of the common modding API. You can use `doukutsu.setSetting(name, value)` to modify those settings.

#### Setting types

| Type       | Description                                                                         |
| ---------- | ----------------------------------------------------------------------------------- |
| int        | a signed integer                                                                    |
| uint       | an unsigned integer                                                                 |
| float      | a floating point number                                                             |
| string     | a string literal                                                                    |
| bool       | a boolean                                                                           |
| "a" \| "b" | an enumeration type - only a specified set of values (delimited by `\|` is allowed) |

#### List of settings

| Name                                            | Description                                                                                                                                                                                                                                                                                                                                                                                                         | Type                   | Default Value                                      |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | -------------------------------------------------- |
| drs.tsc.encoding                                | Character encoding used while reading `.tsc` files                                                                                                                                                                                                                                                                                                                                                                  | "utf-8" \| "shift-jis" | `"shift-jis"`                                      |
| drs.tsc.encrypted                               | If set to true, doukutsu-rs will descramble the `.tsc` file before compiling to internal bytecode (in same way as vanilla engine does: grab the byte in halfway of the file (if the file size is not even, round the location towards zero) - if the byte equals `0x00`, use `0xf9` instead. Then subtract (with wrapping) that value from every byte in the file, except the byte that was used for descrambling.) | bool                   | `true`                                             |
| drs.window.title                                | Sets the window title. Works during any event.                                                                                                                                                                                                                                                                                                                                                                      | string                 | `"Cave Story ~ Doukutsu Monogatari (doukutsu-rs)"` |
| <p>drs.window.width</p><p>drs.window.height</p> | Sets the default window width/height. Has only an effect on first startup. Works only on platforms that support windowing, has no effect if the game runs exclusively in full screen mode (eg. on Android)                                                                                                                                                                                                          | uint                   | <p>640</p><p>480</p>                               |
