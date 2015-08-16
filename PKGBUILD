# Maintainer: Jaroslav Lichtblau <dragonlord@aur.archlinux.org>
# Contributor: Juanma Hernández <juanmah@gmail.com>

pkgname=libsyncml-svn
pkgver=1084
pkgrel=1
pkgdesc="An implementation of the syncml protocol."
url="http://libsyncml.opensync.org/"
license=('LGPL')
arch=('i686' 'x86_64')
depends=('openobex' 'libsoup' 'libwbxml' 'gnutls')
makedepends=('subversion' 'cmake')
replaces=('libsyncml')
conflicts=('libsyncml')
provides=('libsyncml')
source=()
md5sums=()

_svnmod=libsyncml
_svntrunk=https://svn.opensync.org/libsyncml/trunk/

build() {
  cd ${srcdir}

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf ${srcdir}/$_svnmod-build
  cp -r ${srcdir}/$_svnmod $srcdir/$_svnmod-build
  cd ${srcdir}/$_svnmod-build

  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release ${srcdir}/$_svnmod
  make
}

package() {
  cd ${srcdir}/$_svnmod-build

  make DESTDIR=${pkgdir} install
}
