# VibrantWayland: Saturation and Contrast Controller for Wayland

A modern, native display color management utility designed to adjust screen saturation (digital vibrance) and contrast gamma curves in real-time under **KDE Plasma 6 Wayland** environments.


## Key Features

- **Dynamic Color Saturation:** Smooth sliders and precise stepper controls to adjust display saturation (from grayscale to 400% vividness).
- **Contrast Gamma Control:** Fine-tune contrast gamma curves dynamically to enhance readability, contrast, and depth.
- **KWin Wayland Native integration:** Uses native ArgyllCMS and colord pipelines via `kscreen-doctor` to avoid lagging external overlays or heavy GPU filters.
- **Alternating Double-Profile Cache:** Dynamically cycles between two fixed active profiles (`maple_active_a.icc` and `maple_active_b.icc`) to bypass KWin color cache limitations in real-time, preventing temporary file build-up.
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

Maple Saturation Control comes with a silent startup command that is perfect for script execution or autostart items:

```bash
# Instantly restore and apply your saved color parameters at system login:
maple-saturation-control --apply
```
