# Mullvad VPN module for Waybar

![Green lock](./images/screenshot1.png "Mullvad Waybar Module")

Just needed a simple way to see if I'm connected to Mullvad VPN and what server I'm using, so I made this simple custom waybar module.

## Prerequisites

- [mullvad-vpn](https://archlinux.org/packages/?name=mullvad-vpn) or [mullvad-vpn-bin](https://aur.archlinux.org/packages/mullvad-vpn-bin) installed and setup on your system.

## Getting Started

**1. Clone the repo**

```sh
git clone git@github.com:Jonathandah/mullvad-waybar-module.git
```

**2. If you haven't already installed mullvad-vpn, you can install it with yay:**

```sh
# or mullvad-vpn if you prefer the non-bin version
yay -S mullvad-vpn-bin
```

**3. Copy the mullvad script**

```sh
#  ~/.config/waybar/scripts/mullvad.sh is just a suggestion, you can put it wherever you like
mkdir -p ~/.config/waybar/scripts && cp mullvad-waybar-module/mullvad.sh ~/.config/waybar/scripts/mullvad.sh
```

**4. Add the module to your waybar config**

Paste the module into your `~/.config/waybar/config.jsonc`

```jsonc
"custom/mullvad": {
  "format": "{icon}",
  "exec": "~/.config/waybar/scripts/mullvad.sh",
  "interval": 60,
  "return-type": "json",
  "on-click": "~/.config/waybar/scripts/mullvad.sh toggle",
  "on-click-middle": "mullvad-vpn",
  "on-click-right": "~/.config/waybar/scripts/mullvad.sh reconnect",
  "format-icons": {
    "connected": "\uf023",
    "connecting": "\uf023",
    "disconnected": "\uf2fc",
  },
  "tooltip": true,
},
```

> [!NOTE]
> Adjust the `exec` and `on-click` paths if you placed the script somewhere else.

Then add `"custom/mullvad"` to your `modules-left`, `modules-center`, or `modules-right` array to use it.

```jsonc
  "modules-left": [],
  "modules-center": [],
  "modules-right": ["custom/mullvad"]
```

**5. Append the styles to your waybar style.css**

```sh
#  ~/.config/waybar/style.css is just a suggestion, you can put it wherever you like
cat mullvad-waybar-module/style.css >> ~/.config/waybar/style.css
```

```css
@define-color error #F96184;
@define-color foreground #D3D9FF;
@define-color success #01D38F;

#custom-mullvad {
  min-width: 14px;
  margin: 0 7.5px;
}

#custom-mullvad.connecting {
  color: @foreground;
}
#custom-mullvad.connected {
  color: @success;
}
#custom-mullvad.disconnected {
  font-size: 16px;
  margin: 0 7.5px 0 4.5px;
  color: @error;
}
```

**6. Restart waybar**

```sh
killall waybar && waybar &
```

done!

## Thanks

Thanks to Mullvad for providing a great product!

<https://mullvad.net/en>

and many appreciation to the waybar project as well ofc!

<https://github.com/Alexays/Waybar>

## Contributing

Contributions are welcome! Please submit pull requests or open issues for any suggestions, bug reports, or improvements.
