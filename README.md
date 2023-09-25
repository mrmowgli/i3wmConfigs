i3 is a tiling window manager similar to tmux. It's not for everyone, but it's very cool.

To get a good leg up on setup, we need to add some configurations that offer a good starting point.

On Fedora, most things needed for i3wm can be installed with:
```bash
sudo dnf groupinstall "i3 window manager"
sudo dnf groupinstall "i3 window manager (supplemental packages)"
```

Some additional convenience tools you may want to install are:
mpv - Compact tiled video 
ranger - File Manager (Including a configuration change in this repo)
neomutt - Mail client
newsboat - RSS Feeds
maim - Screen capture
caca-utils - image to text
highlight - color terminal previews of code in ranger
atool - archive info, packing and extraction tools
w3m - a web browser for the terminal, doesn't process JS
w3m-img - Allow images to display in the terminal 
poppler-utils - Convert PDF's into text, useful in ranger
mediainfo - tools to allow ranger to correctly preview various mime types.

```bash
sudo dnf install mpv ranger neomutt newsboat maim caca-utils highlight atool w3m w3m-img poppler-utils mediainfo
```

Effectively we have the main configuration file, which should be installed to `.config/i3/config`.

In addition I've included some optional changes to the ranger .config, which if used should be moved in after you have used
ranger at least one time.

A good source of inspiration with S3 is Luke Smith, or lukesmithxyz on Youtube. Unfortunately he has mostly moved
on from just doing an i3wm configuration, but he has several really useful videos for configuring and learning i3 wm.

Luke's configuration makes a good conftiguration starter: https://github.com/LukeSmithxyz/LARBS
however you will want to go back in time, most likely to commit b8cd0ab4953d053fef09c48ba04f2fbb2df57aa4 or earlier.
in order to see the correct configs for i3.

Specifically you should view his video on dmenu:
https://www.youtube.com/watch?v=R9m723tAurA

The main config can be found in: `.config/i3/config`, which is pretty clean but all key bindings don't seem to work.

Some bindings are modifiers, so that the window may pop up split, and META+e will cycle to the new arrangement. Splitting windows doesn't mean it actually splits it, it means that the next window will go into a virtual space that can be moved in. Perhaps there is a better way?

Also certain things like screenshots are not directly supported. To do screenshots we need to use an app like `maim`.

Install:
- `maim`
- `xclip`
- `xdotool`

```config
# For screenshots install :
# apt-get install maim xclip copyq

##  Screenshots in files
bindsym Print exec --no-startup-id maim --format=png "/home/$USER/Pictures/screenshot-$(date -u +'%Y%m%d-%H%M%SZ')-all.png"
bindsym $mod+Print exec --no-startup-id maim --format=png --window $(xdotool getactivewindow) "/home/$USER/Pictures/screenshot-$(date -u +'%Y%m%d-%H%M%SZ')-current.png"
bindsym Shift+Print exec --no-startup-id maim --format=png --select "/home/$USER/Pictures/screenshot-$(date -u +'%Y%m%d-%H%M%SZ')-selected.png"

## Screenshots in clipboards
bindsym Ctrl+Print exec --no-startup-id maim --format=png | xclip -selection clipboard -t image/png
bindsym Ctrl+$mod+Print exec --no-startup-id maim --format=png --window $(xdotool getactivewindow) | xclip -selection clipboard -t image/png
bindsym Ctrl+Shift+Print exec --no-startup-id maim --format=png --select | xclip -selection clipboard -t image/png
```

exec xargs -a .background feh --no-fehbg --bg-fill

For multi screen displays, you will need `arandr`, a way to actually visually set screen resolution and placement.
