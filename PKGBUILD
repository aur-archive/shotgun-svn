# Maintainer: kuri <sysegv@gmail.com>

pkgname=('shotgun-svn')
true && pkgname=('shotgun-svn' 'libshotgun-svn' 'shotgun-sawedoff-svn')
pkgver=81619
pkgrel=4
arch=('i686' 'x86_64')
url="http://www.enlightenment.org"
license=('custom')
depends=('eina' 'eet' 'evas' 'ecore' 'edje' 'elementary' 'efx-svn' 'e_dbus' 'e' 'edbus-svn')
makedepends=('subversion')
optdepends=()
options=('!libtool')
source=()
md5sums=()

_svntrunk="http://svn.enlightenment.org/svn/e/trunk/PROTO/shotgun"
_svnmod="shotgun"

build()
{
  cd $srcdir

  if [ $NOEXTRACT -eq 0 ]; then
    msg "Connecting to $_svntrunk SVN server...."
    if [ -d $_svnmod/.svn ]; then
      (cd $_svnmod && svn up -r $pkgver)
    else
      svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
    fi

    msg "SVN checkout done or server timeout"
    msg "Starting make..."

  fi
  cp -r $_svnmod $_svnmod-build
  cd $_svnmod-build

  ./autogen.sh --prefix=/usr
  make || return 1
}

package_libshotgun-svn()
{
   pkgdesc="libshotgun is an XMPP library using EFLs"
   depends=('eina' 'ecore')
   cd $_svnmod-build
   make DESTDIR=$pkgdir -C src/lib install || return 1
   install -Dm644 $srcdir/$_svnmod-build/COPYING \
  	$pkgdir/usr/share/licenses/libshotgun-svn/COPYING
}

package_shotgun-svn()
{
   pkgdesc="Shotgun is an XMPP Client using EFLs"
   depends=('eet' 'evas' 'ecore' 'edje' 'elementary' 'efx-svn' 'e_dbus')
   cd $_svnmod-build
   make DESTDIR=$pkgdir -C src/bin install || return 1
   install -Dm644 $srcdir/$_svnmod-build/COPYING \
  	$pkgdir/usr/share/licenses/shotgun-svn/COPYING
}

package_shotgun-sawedoff-svn()
{
   pkgdesc="Sawed-off is the shotgun module for integration in Enlightenment DR17"
   depends=('e' 'edbus-svn')
   cd $_svnmod-build
   make DESTDIR=$pkgdir -C src/modules/sawed-off install || return 1
   install -Dm644 $srcdir/$_svnmod-build/COPYING \
  	$pkgdir/usr/share/licenses/shotgun-sawedoff-svn/COPYING
}
