# Maintainer: Julian Xhokaxhiu    <info at julianxhokaxhiu dot com>
# Contributor: almostalive   <almostalive2003 at gmail dot com>
# Contributor: Themaister    <maister@archlinux.us>

pkgname=retroarch-rbp-git
pkgver=1.2.2.3581.g3433a51
pkgrel=1
pkgdesc="Reference frontend for the libretro API."
arch=('arm' 'armv6h' 'armv7h')
url="http://github.com/libretro/RetroArch"
license=('GPL')
depends=('mesa' 'mesa-libgl' 'libusb' 'openal' 'python')
makedepends=('git')
provides=('retroarch' 'retroarch-git')
conflicts=('retroarch')

_gitname=RetroArch
source=("git+https://github.com/libretro/${_gitname}.git")
md5sums=('SKIP')

pkgver() {
  cd "${_gitname}"
  local version=$(git describe --tags)
  local version=${version/v/}
  local version=${version//-/.}
  echo $version
}

build() {
  cd "${_gitname}"
  export CFLAGS="$CFLAGS -I/opt/vc/include"
  export LDFLAGS="${LDFLAGS//-Wl,--as-needed} -L/opt/vc/lib/ -lGLESv2 -lEGL -lopenmaxil -lbcm_host -lvcos -lvchiq_arm -lpthread"
  ./configure --prefix=/usr --enable-neon --enable-dispmanx --enable-floathard --enable-udev
  make
}

package() {
  cd "${_gitname}"
  make install DESTDIR="${pkgdir}"
}
