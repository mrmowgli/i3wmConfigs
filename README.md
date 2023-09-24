i3 is a tiling window manager similar to tmux. It's not for everyone, but it's very cool.
To get a good leg up on setup, we need to add dotfiles that represent our intent.

On Fedora, most things can be installed with:
```bash
sudo dnf groupinstall "i3 window manager"
sudo dnf groupinstall "i3 window manager (supplemental packages)"
```

A good starting place is: https://github.com/jdkaplan/dotfiles
Another good conftiguration starter: https://github.com/LukeSmithxyz/LARBS

A video on dmenu:
https://www.youtube.com/watch?v=R9m723tAurA

The main config can be found in: `.config/i3/config`, which is pretty clean but all key bindings don't seem to work.

SOme bindings are modifiers, so that the window may pop up split, and META+e will cycle to the new arrangement. Splitting windows doesn't mean it actually splits it, it means that the next window will go into a virtual space that can be moved in. Perhaps there is a better way?

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