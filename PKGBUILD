pkgname=paper-icon-theme-git
pkgver=827.ab51c46f
pkgrel=1
pkgdesc="Paper is an icon theme for GTK based desktops and fits perfectly the paper-gtk-theme"
arch=(any)
url="https://github.com/snwh/paper-icon-theme"
license=('CC BY-SA 4.0')
depends=('gtk-update-icon-cache')
makedepends=('git' 'meson')
provides=('paper-icon-theme')
source=("0001-Paper-scalable-fix-svg-namespace-definitions.patch"
        "$pkgname"::'git+https://github.com/snwh/paper-icon-theme.git')
md5sums=('9c3d3a14785f8b47fdc56e4bf162b76e'
         'SKIP')

pkgver() {
  cd "$srcdir/$pkgname"
  echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

prepare () {
  cd "${pkgname}"
  # Apply patch fixing svg's
  patch -p1 -i ../0001-Paper-scalable-fix-svg-namespace-definitions.patch
}

build() {
  cd "${pkgname}"
  meson build --prefix=/usr
}

package() {
  cd "${pkgname}"
  DESTDIR="$pkgdir" ninja -C "build" install
}
