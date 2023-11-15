# Maintainer: Bims <mail@bims.sh>
pkgname=miru-app-git
_pkgname=miru-app
pkgver=275.287a924
pkgrel=1
pkgdesc="A versatile application that is free, open-source, and supports extension sources for videos, comics, and novels, available on Android, Windows, and Web platforms."
arch=("x86_64")
url="https://github.com/miru-project/${_pkgname}"
license=("APGL-3.0")
provides=($_pkgname)
conflicts=($_pkgname)
replaces=($_pkgname)
depends=("webkit2gtk-4.1")
makedepends=("git" "flutter" "clang" "ninja" "pkgconf")
source=("git+https://github.com/miru-project/$_pkgname.git")
md5sums=('SKIP')

pkgver() {
  cd $_pkgname
  echo $(git rev-list --count dev).$(git rev-parse --short dev)
}

prepare(){
  cd $_pkgname

  # Prepare Flutter
  flutter --no-version-check config --no-analytics
  flutter --no-version-check config --enable-linux-desktop
  flutter --no-version-check pub get
}

build() {
  cd $_pkgname

  # Build the Flutter application
  flutter --no-version-check build linux --release
}

package() {
  cd "$_pkgname/build/linux/x64/release/bundle/"

  # Create target directories
  install -dm 755 "$pkgdir/opt/$_pkgname" "$pkgdir/usr/bin/"

  # Copy the bundled output to /opt
  cp -rdp --no-preserve=ownership . "$pkgdir/opt/$_pkgname/"

  # Symlink to /usr/bin so the app can be found in PATH
  ln -s "/opt/$_pkgname/miru" "$pkgdir/usr/bin/$_pkgname"
}
