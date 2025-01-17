# <samp>DWM - Dynamic Window Manager<samp> <img alt="GitHub top language" src="https://img.shields.io/github/languages/top/saifshahriar/dwm-saif?color=%231a1b26&label=suckless%20&logo=c%2B%2B&logoColor=%237aa2f7&style=for-the-badge" align="right">

My build of dwm with minimal patches. Go to [patches](https://github.com/saifshahriar/dwm-saif-git#patches) section to know more.

<hr>

### Screenshots
<div align="center">
    <img src="https://raw.githubusercontent.com/saifshahriar/saifshahriar/master/repo/dwm/Screenshot_2022-10-07-20-32-21_1366x768.png" width="500px">
    <img src="https://raw.githubusercontent.com/saifshahriar/saifshahriar/master/repo/dwm/Screenshot_2022-10-07-20-35-53_1366x768.png" width="500px">
</div>

- Terminal Emulator: Alacritty
- Colorscheme: Tokyonight

<br>
dwm is an extremely fast, small, and dynamic window manager for X.

## Why another DWM fork?
DWM comes in pretty good shape. This fork of DWM tries to be minimal yet some features
that I thought is missing (for my personal taste obviously). The word *minimal* is different from person to person. To be
fair, I even tried to get rid of the bar. Lol! Also, one of the main purpose for
this project is learning the *beautifully unsafe C programming language* that
dwm is written in. :/

### Features:
- Simple edited `config.h` file.
- Ability to reload dwm without logging out. Default key for this is
`Mod4 + Shift + r`.
- Gaps and the ability to change the gaps on the fly. See `keybindings` section.
- *Smartgaps*: Show no gaps when there is only one window per tag.
- Ability to set colours from `~/.Xresources` or `~/.config/X11/xresources` file. See more at [Xresources Section](https://github.com/saifshahriar/dwm-saif#xresources-settings).
- Centers terminal windows (or any windows defined in the config) to the center
if it is the only window in that tag. Also change the `height`, `width` and the
`y-offset` of that window.
- Custom height for bar.
- Comes with four layouts. `tile`, `grid`, `floating`, `monocle`.
- Toggle maximize.
- No border when a window is minimized (can change the behaviour from the
config).

### More to come?
- [ ] ~~Maybe a ~~`lua` config file. Not too crazy like `awesomewm`. I am not sure. Heh.~~ `toml` parser.~~ I am sorry. Not doing this shit.
- [ ] Add patch `swallow`.
- [ ] Add patch `riodraw`.
- [ ] Combinations of `alttagsdecoration`, `underline tags`, and `rainbow` tags
	  and the ability to turn them on/off from the config.
- [ ] TODO: Ability to apply **Optional Patches** using preprocessors.

## Requirements
- In order to build dwm you need the Xlib header files.
~~- For colour emoji support, install `libxft-bgra`. Heres the [repo](https://github.com/uditkarode/libxft-bgra).~~
- `st`, unless you change the terminal emmulator
- `dmenu`, as the run launcher

**Optional:**
- `xmneu`, for right click menu support
- `xdotool`, for some of the xmenu scripting
- `JetBrainsMono Nerd Font` (default) or any nerd font for icons

## Installation
Clone the repo:
```bash
git clone https://github.com/saifshahriar/dwm-saif dwm --depth=1
cd dwm
```

Edit `config.mk` to match your local setup (dwm is installed into the
`/usr/local` namespace by default).

First time installing the window manager, type this command (as root) to setup
everything.
```bash
make setup
```

*Above command also copies the current contents of the folder to `/opt/dwm-saif`*

Enter the following command to build and install dwm after every change to the
files (if necessary as root):
```bash
make clean install
```

**If dwm crashes**
This is a problem with `libXft < 2.3.5`. This problem constantly occurs in Debian/Ubuntu derivatives. There is a patch file.
Run this command before `make install`
```bash
patch -p1 < noemoji.patch
```
	
## Running dwm
### Startx
Add the following line to your .xinitrc to start dwm using startx:

```bash
exec dwm
```
In order to connect dwm to a specific display, make sure that
the DISPLAY environment variable is set correctly, e.g.:

```bash
DISPLAY=foo.bar:1 exec dwm
```

(This will start dwm on display :1 of the host foo.bar.)

### Display Manager
If you are using a display manager (i.e. lightdm, sddm, gdm) and if you have
already ran the `make setup` command, you should see it in the login screen
list.

### Status Bar
In order to display status info in the bar, you can do something
like this in your .xinitrc:

```bash
while xsetroot -name "`date` `uptime | sed 's/.*,//'`"
do
    sleep 1
done &
exec dwm
```

__If you want a similar status bar like mine, you can get it from my [dotfiles](https://github.com/saifshahriar/dotfiles/blob/master/.config/dwm/dwmbar.sh) repo.__

<div align="right">
    <img src="https://user-images.githubusercontent.com/89329547/194582023-6a81df49-5e77-48bb-a6f7-6dde0bcdc646.png">
</div>

## Configuration
The configuration of dwm is done by creating a custom config.h
and (re)compiling the source code.

## Patches
Here are some of the patches that I have applied.

- actualfullscreen    - Actually toggle fullscreen for a window, instead of toggling the status bar and the monocle layout.
- adjacenttag         - Focus adjacent tag using left/right arrow keys.
- alttagsdecoration   - An alternative text for tags which contain at least one window
- alwayscenter        - Always center floating windows.
- center first window - Center specific window if only one window.
- cursorwarp          - Warp the cursor to the center of the target window when switching between them.
- extrabar            - Dual bar.
- focusonnetactive    - Focus when a window gets active even in some other tag.
- layoutscroll        - Cycle through all layouts defined in layouts array.
- movestack           - Move stacks in a tag using mod+shift+{j,k}
- noborder            - Noborder when only one window.
- pertag              - dwm pertag patch, which allow different type of window size in different tags and doesn't change if one changed in one tag.
- preserveonrestart   - Don't mashup all windows in a single tag on restarting dmw
- psudogaplessgrid    - Basically `gaplessgrid` layout. Psudo version is modified by me which adds gaps from `vanitygaps` patch.
- restartsig          - Restart dwm without exiting logging back on.
- status2d            - Allows colors and rectangle drawing in DWM status bar.
- underline tags      - Underline below a tag.
- vanitygaps          - Adds gapps around the windows.
- xrdb                - Read colors from xresources. For this patch to work, run the command `xrdb -load <path-to-xresources>`

**Optional Patches:** These are some optional patches that comes separately and are not applied by default. If you need them you can simply `git apply <patch-name>.patch` or you can use the standard `patch` command.
- bidi.patch          - Adds proper support for Right-To-Left languages. (such as Farsi, Arabic or Hebrew)
- noemoji.patch       - Disables coloured text and emojis in the title bar. There is a LibXft bug that causes DWM to crash whenever any emoji is being displayed in the title bar. Currently it has been fixed. So, treat this as a legacy code for older systems.
- touchpad.patch      - Touchpad support for laptops.


## Xresources Settings
This is an example for all the variables you can use to customize the colours of
dwm using `Xresources` file.

__Note that__, dwm will look for the config file first in the
`~/.config/X11/xresources` file. If not found, it will look for the
`~/.Xresources` file. You have to press `Mod4 + F5` to make the changes take
effect. This basically runs the `xrdb -merge <xresources>` command
```scss
! TokyoNight colors for Xresources
*background: #1a1b26
*foreground: #c0caf5
*selbackground: #1a1b26
*selforeground: #7aa2f7
*accent: #7aa2f7
*border: #7aa2f7

*color0: #15161e
*color1: #f7768e
*color2: #9ece6a
*color3: #e0af68
*color4: #7aa2f7
*color5: #bb9af7
*color6: #7dcfff
*color7: #a9b1d6

*color8: #414868
*color9: #f7768e
*color10: #9ece6a
*color11: #e0af68
*color12: #7aa2f7
*color13: #bb9af7
*color14: #7dcfff
*color15: #c0caf5

! Xmenu specific
xmenu.font: JetBrainsMono Nerd Font:size=9, NotoColorEmoji:size=11
xmenu.separator: #c0caf5
xmenu.borderWidth: 2
```

## Major Keybindings
`Super`(Mod4) key is the `Modkey`
| **Keys**                         | **Action**                                          |
|----------------------------------|-----------------------------------------------------|
| `Mod + Return`                   | Open a terminal (`st`)                              |
| `Mod + d`                        | Launch `dmenu_run`                                  |
| `Mod + c`                        | Close the focused window                            |
| `Mod + {k, j}`                   | Move focus to the {next, previous} window           |
| `Mod + Shift + {k, j}`           | Move the focused window within the stack            |
| `Mod + {h, l}`                   | {Increase, Decrease} the master pane size           |
| `Alt + Tab`                      | Cycle focus between windows                         |
| `Mod + Tab`                      | Toggle between layouts                              |
| `Mod + f`                        | Toggle fullscreen mode                              |
| `Mod + Space`                    | Toggle floating mode                                |
| `Mod + Shift + Space`            | Toggle monocle (maximize) layout                    |
| `Mod + {1-9}`                    | Switch to tag {1-9}                                 |
| `Mod + Shift + {1-9}`            | Move the focused window to tag {1-9}                |
| `Mod + {Left, Right}`            | Switch to the {next, previous} tag                  |
| `Mod + Shift + {Left, Right}`    | Move the focused window to the {next, previous} tag |
| `Mod + {equal, minus}`           | {Increase, Decrease} gaps                           |
| `Mod + Shift + g`                | Toggle gaps                                         |
| `Mod + Shift + q`                | Quit DWM                                            |
| `Mod + Shift + r`                | Restart DWM                                         |

_See more keybinds in [`config.h`](https://github.com/saifshahriar/dwm-saif/blob/master/config.h)_
