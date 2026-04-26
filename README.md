# xkb - Readme
My XKB dots for mimicing German (US) layout, known from GNOME and KDE, on Hyprland, i3WM, Sway & river.


---
## Table of Contents
- [FAQ](#faq)
  - [What it does?](#what-it-does)
  - [What is X keyboard Extension?](#what-is-x-keyboard-extension)
  - [Why?](#why)
- [Mapping](#mapping)
  - [Umlauts (Vocal mutations)](#umlauts-vocal-mutations)
  - [Sharp S (Eszett) and EURO sign](#sharp-s-eszett-and-euro-sign)
- [Setup](#setup)
  - [Niri (including ncotalia shell)](#niri)
  - [Hyprland](#hyprland)
  - [Compose key (Optional)](#compose-key-optional)
- [Removal](#removal)
- [Changelog](#changelog)

--- 

## FAQ
### What it does?
Currently, it just adds a custom config for XKB (X keyboard Extension). it works for most Wayland compositors like Sway, river, Hyprland, and it should also work on X11 tiling window managers like i3WM.

### What is Xkeyboard Extension?
Originally, it was a Xorg protocol for keyboard input, but its use got extended from i3WM to Sway and then to Hyprland.

### Why?
Because WMs like Hyprland and Co doesn't support German (US) as layout which is my preferred layout under GNOME and KDE. The main advantage is that it lays out the input from the keyboard in ANSI-US, perfect for terminal and coding work, but terrible for writing in German. US (intl) and US(altGr, intl) solve it half way, but by starting a compose mode as soon as you use the apostrophe or quote marks. It's slow, doesn't work everywhere, e.g. in CLI, and is annoying as soon as you need the apostrophe or quotation mark, because both are now the the key, pause and then space.
My config solve it by mapping the letters and the Euro sign as shortcuts that can be access by right alt.

---

## Mapping
#### Umlauts (Vocal mutations)
ä = `rAlt`+`a`\
ö = `rAlt`+`o`\
ü = `rAlt`+`u`\
Ä = `rAlt`+`Shift`+`a`\
Ö = `rAlt`+`Shift`+`o`\
Ü = `rAlt`+`Shift`+`u`\

#### Sharp S (Eszett) and EURO sign
ß (lower) = `rAlt`+`s`\
ẞ (upper) = `rAlt`+`Shift`+`s`\
€ = `rAlt`+`e` or `rAlt`+`Shift`+`E`\


---

## Setup
If `~/.config/xkb/symbols/` doesn't exist, create `~/.config/xkb/`:

```
mkdir --parents ~/.config/xkb/symbols/
```
Clone the file into it:
```sh
git clone https://github.com/ghostcat1001001/xkb-dots.git &&
  cp xkb-dots/us_german ~/.config/xkb/symbols
```

---

### Niri
#### (Also works with Noctalia shall)
Add the following input to your dots.
In my case, it's `~/.config/niri/cfg/input.kdl`. In most cases, you find the settings for Niri at `~/.config/niri/`.  
Search for the following part:

```conf
input {
    keyboard {
        xkb {
            layout "us"
        }
    }
}
```
Don't worry, if there's more content into it. We just change `layout "us"` to `layout "us_german"` and comment any variant (e.g. `variant "alt-intl"` to `// variant "alt-intl"`).

If you are unsure about the path, try first `grep -r "layout " ~/.config/niri" 2>/dev/null`, and if that fail, read the documentation of your dotfiles.

**Log out and log in again!** Niri scans only for xkb layouts at log-in.

---

### Hyprland
#### (how it was used to work. I stopped working on the Hyprland setup. You can attemot it but I recommend to follow the documentation of Hyprland as the devs loves to changes how things work)
Add the following input to your dots.
In my case, it's `~/.config/hypr/config/input.conf`, as I use a modular approach that lets hyprland call multiple modular config files.\
The default by vanilla Hyprland is `~/.config/hypr/hyprland.conf`.\
You probably find the input variable and a layout declaration inside.
**If so**, just edit or replace them with this:

```conf
input {
  kb_layout = us_german
}
```

**Then, reload with hyprctl reload** from your terminal, if you don't have a keybinding for reloading.\
On CachyOS, Hyprland should automatically take the change, otherwise force it via `Super`+`o`.

--- 

### Compose key (Optional)
 If you want a compose key to be set, you wanna add `kb_options = compose:menu` **inside** the input **under** `kb_layout = us_german`, like:

```conf
input {
  kb_layout = us_german
  kb_options = compose:menu
}
```

This will allow you, to access the compose mode via Menu, and then you can add `a` and `'` to `á`, or make `--`. to `–` (used in Germany to separate thoughts in texts or give from-to declarations[*](https://de.wikipedia.org/wiki/Halbgeviertstrich)),
or `---` to `—` (separates thoughts in texts in English[*](https://en.wikipedia.org/wiki/Dash)).

You find the compose list [on this GitHub page](https://tuttle.github.io/python-useful/compose-key-cheat-sheet.html).\

You can also set another key as compose key. Just follow the [Ubuntu Help article](https://help.ubuntu.com/community/ComposeKey).

---

## Removal
`rm ~/.config/xkb/symbols/us_german` for just removing the **file** **(RECOMMENDED IF YOU DON'T KNOW WHAT YOU DO!)**,

or `rm -rf ~/.config/xkb/symbols/` for the whole **Symbols folder** (only recommended if you don't wanna keep other symbols configs,

## Changelog
1. 2026 April 26: Official support for Hyprland setup depricated. Support for setup on Niri added, as I moved on. Reason: frequently changes to Hyprland makes it hard to maainain dotfiles. Niri is way more stable and I appreciate scrolling WMs more.

or `rm -rf ~/.config/xkb/` for removing all *XKB configs (only recommended if you either don't have custom XKB configs or want to get rid off every XKB configs.
