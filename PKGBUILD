pkgname=vibrantwayland-git
_pkgname=VibrantWayland
pkgver=1.0.0
pkgrel=1
pkgdesc="A controller for Digital Vibrance (Saturation) and Contrast (Gamma) for KDE Plasma sessions on Wayland."
arch=('any')
url="https://github.com/CuberBeats/VibrantWayland"
license=('GPL3')
depends=('python' 'python-pyqt6' 'argyllcms' 'colord' 'iccxml')
makedepends=('git')
provides=('vibrantwayland')
conflicts=('vibrantwayland')
source=("git+https://github.com/CuberBeats/VibrantWayland")
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/$_pkgname"
  printf "1.0.0.r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
  cd "$srcdir/$_pkgname"
  
  # Install the main Python script
  install -Dm755 vibrantwayland.py "$pkgdir/usr/bin/vibrantwayland"
  
  # Install the .desktop entry
  install -Dm644 VibrantWayland.desktop "$pkgdir/usr/share/applications/vibrantwayland.desktop"
  
  # Update the executable path inside the installed .desktop entry to use system binary /usr/bin/vibrantwayland
  sed -i 's|Exec=.*|Exec=/usr/bin/vibrantwayland|' "$pkgdir/usr/share/applications/vibrantwayland.desktop"
}
