# VibrantWayland: Saturation and Contrast Controller for Wayland

A modern, native display color management utility designed to adjust screen saturation (digital vibrance) and contrast gamma curves in real-time under **KDE Plasma 6 Wayland** environments.

> **Disclosure:** VibrantWayland is a rework of [Maple Saturation Control for Wayland Plasma] (https://aur.archlinux.org/packages/maple-saturation-control-git), released under the [GNU General Public License v3 (GPL-3.0)](https://www.gnu.org/licenses/gpl-3.0.html). This project is distributed under the same license.

I have been looking around for a reliable tool to change Display Saturation on Wayland Desktop. However, while nVibrant works really well for Nvidia displays, Intel and AMD are still very much left in the dust. Maple Saturation is a program I found on the AUR, and the first one that actually works for Wayland. Seeing this, I decided to tidy up the code a bit, and redesign the UI a bit to make it a little more palatable, at least for me. I hope this program helps people with an issue I've been struggling with for a while, and I do plan to update this structurally in the future as well.

## Key Features

- **Dynamic Color Saturation:** Smooth sliders and precise stepper controls to adjust display saturation (from grayscale to 400% vividness).
- **Contrast Gamma Control:** Fine-tune contrast gamma curves dynamically to enhance readability, contrast, and depth.
- **KWin Wayland Native integration:** Uses native ArgyllCMS and colord pipelines via `kscreen-doctor` to avoid lagging external overlays or heavy GPU filters.
- **Alternating Double-Profile Cache:** Dynamically cycles between two fixed active profiles (`vway_active_a.icc` and `vway_active_b.icc`) to bypass KWin color cache limitations in real-time, preventing temporary file build-up.
- **Modern Premium Design System:** Gorgeous, cohesive dark-mode user interface utilizing custom HSL palettes, smooth micro-interactions, and step adjustments.
- **Startup Restore Support:** Runs seamlessly in the background or applies saved configurations instantly at system login via the `--apply` CLI parameter.

---

## Installation & Deployment

### Dependencies

Ensure the following packages are installed on your Arch Linux system:
- `python` & `python-pyqt6` (App environment and GUI layer)
- `argyllcms` & `colord` (Color management framework engines)
- `iccxml` (ICC profile compiler toolset)

### Method 1: Using the Desktop Launcher (Local)
Run the `start_app.sh` script to automatically check/install dependencies via Pacman or your AUR helper (`yay`/`paru`) and launch the application:
```bash
chmod +x start_app.sh
./start_app.sh
```

### Method 2: System-wide AUR Installation (Local Test Build)
You can compile and build the package locally using the provided standard Arch Linux `PKGBUILD` recipe:
```bash
# Clone the directory, navigate to it, and compile the package
makepkg -si
```

---

## Command Line Interface (CLI)

VibrantWayland comes with a silent startup command that is perfect for script execution or autostart items:

```bash
# Instantly restore and apply your saved color parameters at system login:
vibrantwayland --apply
```

---

## Usage

### Launching the App
Run the app either through the desktop launcher or directly from the terminal:
```bash
vibrantwayland
```

### Selecting a Display
Use the **Target Display Output** dropdown to select which connected monitor you want to adjust. On single-monitor setups this will already be selected automatically.

### Adjusting Saturation
The **Digital Vibrancy (Saturation)** slider controls colour intensity:
- `1.0` is the default — natural, unmodified colour
- Below `1.0` moves toward greyscale
- Above `1.0` increases vividness, up to `4.0` (400%)

Use the slider for broad adjustments or type a precise value directly into the number box. The `+` and `-` buttons step in increments of `0.05`.

### Adjusting Gamma
The **Contrast (Gamma Curve)** slider controls the brightness of midtones:
- `1.0` is the default — standard sRGB gamma
- Below `1.0` darkens midtones, increasing perceived contrast
- Above `1.0` brightens midtones, softening contrast

### Applying Settings
Click **Apply Settings** to push the current values to your display. Changes take effect immediately via KWin's colour management pipeline.

### Selecting Color Profile
Once you go to Display Settings, change the Color Profile to **ICC profile**, where the new profile with the updated settings will automatically be filled in. Apply the changes.

### Resetting to Default
Click **Reset Default Settings** to return both saturation and gamma to `1.0` and reapply.

### Autostart at Login
To restore your saved settings silently every time you log in, add the following command to your KDE autostart entries under **System Settings → Autostart**:
```bash
vibrantwayland --apply
```
This applies your last saved configuration without opening the GUI window.
