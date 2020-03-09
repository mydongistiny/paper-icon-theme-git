pkgname=paper-icon-theme-git
pkgver=830.d1ed2975
pkgrel=1
pkgdesc="Paper is an icon theme for GTK based desktops and fits perfectly the paper-gtk-theme"
arch=(any)
url="https://github.com/snwh/paper-icon-theme"
license=('CC BY-SA 4.0')
depends=('gtk-update-icon-cache')
makedepends=('git' 'meson')
provides=('paper-icon-theme')
source=("0001-Paper-scalable-fix-svg-namespace-definitions.patch"
        "0002-Remove-Adwaita-from-Inherits-section.patch"
        "0003-icons-apps.patch"
        "$pkgname"::'git+https://github.com/snwh/paper-icon-theme.git')
md5sums=('64e960f72eedcd32f5baa19404fb415d'
         '43266ea4b4968632a8ebb038940c17d2'
         '72190dd9a5016046e06710701217a0d4'
         'SKIP')

pkgver() {
  cd "$srcdir/$pkgname"
  echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

prepare () {
  cd "${pkgname}"
  # Apply patch fixing svg's
  git am < "$srcdir"/0001-Paper-scalable-fix-svg-namespace-definitions.patch;
  git am < "$srcdir"/0002-Remove-Adwaita-from-Inherits-section.patch;
  git am < "$srcdir"/0003-icons-apps.patch;
}

build() {
  cd "${pkgname}"
  meson build --prefix=/usr
}

package() {
  cd "${pkgname}"
  DESTDIR="$pkgdir" ninja -C "build" install
}
