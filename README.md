# 🍃 Modular Mint-Sway Dotfiles

A professional, modular configuration for Sway on Linux Mint. Designed to be "Machine-Agnostic" so you can sync the same repo across a Dell laptop and a Desktop PC.

## 🏗️ Architecture
This repo uses **GNU Stow** packages. You "mix and match" folders depending on which machine you are sitting at.

* `common`: Shared configs for Waybar and Wofi.
* `sway-core`: Main keybindings and logic.
* `dell-laptop`: Specific tweaks for Dell hardware (Touchpad/Scaling).

## 🚀 Installation

**1. Install Dependencies**
```bash
sudo apt update && sudo apt install -y sway waybar wofi stow git policykit-1-gnome gnome-keyring brightnessctl playerctl
```

**2. Clone & Link**
```bash
git clone [https://github.com/YOUR_USERNAME/dotfiles.git](https://github.com/YOUR_USERNAME/dotfiles.git) ~/dotfiles
cd ~/dotfiles

# Link common settings
stow common
stow sway-core

# Link machine-specific settings (Choose one)
stow dell-laptop 
```

## ⌨️ Handling Peripherals (Best Practices)
To ensure settings only apply to the correct hardware, this repo uses **Identifiers**. 

To find your device IDs on a new machine, run:
`swaymsg -t get_inputs` (for keyboards/mice)
`swaymsg -t get_outputs` (for monitors)

### Example Identifier Config (`config.d/laptop.conf`):
```sway
# Dell Touchpad Configuration
input "101:5:Dell_Touchpad" {
    tap enabled
    natural_scroll enabled
    dwt enabled  # disable-while-typing
}

# Laptop Screen Scaling
output "eDP-1" scale 1.2
```

## 🔧 Maintenance
* **Update a config:** Just edit the file in `~/.config/`. Since it's a symlink, the change happens inside `~/dotfiles` automatically.
* **Add a new machine:** Create a new folder (e.g., `work-pc`), mimic the `.config/sway/config.d/` structure, and run `stow work-pc`.
