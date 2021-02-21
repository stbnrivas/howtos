Highlight Trailing Whitespace



+ bug block comments shortcut don't work in linux

As a workaround, go to Preferences->Key Bindings - User and add these keybindings (if you're using Linux):

{ "keys": ["ctrl+7"], "command": "toggle_comment", "args": { "block": false } },
{ "keys": ["ctrl+shift+7"], "command": "toggle_comment", "args": { "block": true } 