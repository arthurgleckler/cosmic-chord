# COSMIC Chord

COSMIC Chord, `coschord`, helps you stay focused while you switch apps
under [COSMIC](https://system76.com/cosmic)[^1].
Given an app ID, it will make sure that the app is running and has a
window selected.  Once `coschord` is on a few keyboard shortcuts, when
your monkey brain thinks "show me web page," your fingers can make the
right thing happen instantly.  No fiddling with the mouse, and no
distractions.

[^1]: I switched to COSMIC after upgrading my System76 laptop to
    Pop!_OS 24.04 LTS.  COSMIC's tiling window manager is so good that
    I don't need the window-manipulation parts of my [Window
    Chord](https://speechcode.com/blog/window-chord) project any more.
    `coschord` was the only missing piece.

I set up COSMIC's custom keyboard shortcuts (`cosmic-settings
keyboard`) like this:

| app             | chord                                                        | command                             |
|-----------------|--------------------------------------------------------------|-------------------------------------|
| COSMIC Files    | <kbd>Ctrl</kbd>-<kbd>Alt</kbd>-<kbd>Shift</kbd>-<kbd>F</kbd> | `coschord com.system76.CosmicFiles` |
| COSMIC Terminal | <kbd>Ctrl</kbd>-<kbd>Alt</kbd>-<kbd>Shift</kbd>-<kbd>T</kbd> | `coschord com.system76.CosmicTerm`  |
| GNU Emacs       | <kbd>Ctrl</kbd>-<kbd>Alt</kbd>-<kbd>Shift</kbd>-<kbd>E</kbd> | `coschord emacs`                    |
| Google Chrome   | <kbd>Ctrl</kbd>-<kbd>Alt</kbd>-<kbd>Shift</kbd>-<kbd>W</kbd> | `coschord google-chrome`            |

```
Usage: coschord [<app_id>] [<launch_command>...]
```

If there are matching windows, `coschord` will select the first one it
finds.  If one is already selected, `coschord` will select the next
one.

If there are no matching windows, `coschord` will start the app using
*launch_command*, e.g.:

```sh
coschord emacs /usr/local/bin/emacs
```

If you only supply *app_id* (e.g. `coschord emacs`), `coschord` will
run the launch command for *app_id* found in
[`~/.config/coschord/commands.json`](~/.config/coschord/commands.json).

To see the app IDs of all running programs, run `coschord` with no
arguments.

Here's a sample `commands.json` configuration file:

```json
{
  "com.system76.CosmicFiles": ["cosmic-files"],
  "com.system76.CosmicTerm": ["cosmic-term"],
  "emacs": ["emacs"],
  "google-chrome": ["google-chrome"]
}
```

`coschord` is written in [Rust](https://rust-lang.org/).  To build and install it:

```
cd coschord
cargo build --release
cargo install --path .
```
