# from xmodmap to xkb 

xmodmap has been deprecated from fedora 27 doesn't support in gnome 3


## xev

Xev  creates a window and then asks the X server to send it events whenever anything happens to
the window (such as it being moved, resized, typed in, clicked in, etc.).  You can also  attach
it  to  an existing window.  It is useful for seeing what causes events to occur and to display
the information that they contain; it is essentially a  debugging  and  development  tool,  and
should not be needed in normal usage.


xdev and press key to show the code

```bash
# to show only keyboard event, ignoring mouse
xev -event keyboard
# to show all
xev
```



KeyRelease event, serial 37, synthetic NO, window 0x3200001,
    root 0x2ac, subw 0x0, time 824899, (834,218), root:(879,327),
    state 0x10, keycode 49 (keysym 0xba, masculine), same_screen YES,
    XLookupString gives 2 bytes: (c2 ba) "º"
    XFilterEvent returns: False

__keycode 49 -> keysym 0xba, masculine__


KeyPress event, serial 37, synthetic NO, window 0x3200001,
    root 0x2ac, subw 0x0, time 826971, (834,218), root:(879,327),
    state 0x10, keycode 94 (keysym 0x3c, less), same_screen YES,
    XLookupString gives 1 bytes: (3c) "<"
    XmbLookupString gives 1 bytes: (3c) "<"
    XFilterEvent returns: False

__keycode 94 -> keysym 0x3c, less__




```bash
cd /usr/share/X11/xkb
tree -L 1

├── compat
├── geometry
├── keycodes
├── rules
├── symbols
└── types
```

__geometry folder__ geometry directory there are files giving instruction to the keyboard-manager application about the physical appearance of the keyboard.

__keycodes__ In the keycodes and symbols directories there are files to modify to design a custom layout.

In the keycodes/evdev file you can map a binding between the key-code and the key-symbol. The key-symbol will be interpreted by XKB accordingly to the mapping table written in the file symbols/us.

__rules__ The files contained in the rules directory inform XKB about the available layouts and their children (layout-variants).


setxkbmap -print -verbose 10

```bash
[stbn@hk51-gzk ~]$ setxkbmap -print -verbose 10
Setting verbose level to 10
locale is C
Trying to load rules file ./rules/evdev...
Trying to load rules file /usr/share/X11/xkb/rules/evdev...
Success.
Applied rules from evdev:
rules:      evdev
model:      pc105
layout:     us
Trying to build keymap using the following components:
keycodes:   evdev+aliases(qwerty)
types:      complete
compat:     complete
symbols:    pc+us+inet(evdev)
geometry:   pc(pc105)
xkb_keymap {
	xkb_keycodes  { include "evdev+aliases(qwerty)"	};
	xkb_types     { include "complete"	};
	xkb_compat    { include "complete"	};
	xkb_symbols   { include "pc+us+inet(evdev)"	};
	xkb_geometry  { include "pc(pc105)"	};
};
```


setxkbmap -layout us,us -variant ,dvorak -option "lv3:rwin_switch"





# remaping

__keycode 49 -> keysym 0xba, masculine__
__keycode 94 -> keysym 0x3c, less__

```bash
setkeycodes --help
# usage: setkeycode scancode keycode ...
# (where scancode is either xx or e0xx, given in hexadecimal,
#  and keycode is given in decimal)
# setkeycodes 0xe048 54
setkeycodes 0xba 97
setkeycodes 0x3c 49
```

but unfortunately it doesn't work searching into forums I discovered that the problem it's about hardware apple aluminium keyboard in kernel. and I found a solution at: 

https://bugs.launchpad.net/ubuntu/+source/linux/+bug/214786

thanks so much gianni https://launchpad.net/~gianni.

# THE SOLUTION

The command for a volatile fix

```bash
echo 0 | sudo tee /sys/module/hid_apple/parameters/iso_layout
```

and for a permanent solution

```bash
echo options hid_apple iso_layout=0 | sudo tee -a /etc/modprobe.d/hid_apple.conf
```


