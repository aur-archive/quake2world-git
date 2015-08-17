# Maintainer: brent saner <bts@square-r00t.net>

pkgname=quake2world-git
pkgver=r2163.a706d35
pkgrel=1
pkgdesc="A free, stand-alone, multiplayer-only iteration of Quake2"
arch=('any')
url="http://quetoo.org"
license=('GPL')
source=(git+https://github.com/jdolan/quake2world.git)
md5sums=('SKIP')
depends=('sdl2' 'curl' 'sdl2_image' 'sdl2_mixer')
makedepends=('sdl2' 'sdl2_mixer' 'sdl2_image' 'physfs')
optdepends=(
'quake2world-data-git: the game data files'
)
install=quake2world.install
_pkgname=quake2world

pkgver() {
  cd "${srcdir}/${_pkgname}"
  ( set -o pipefail
    git describe --long --tags 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

package() {
  cd ${srcdir}/quake2world

  libtoolize
  autoreconf -i
  ./configure --prefix=/usr --without-mysql
  make
  make DESTDIR=${pkgdir} install
}
