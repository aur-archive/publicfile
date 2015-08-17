# Maintainer: Andres Erbsen <andres@krutt.org>
pkgname=publicfile
pkgver=0.52
pkgrel=4
pkgdesc="HTTP and FTP server for public files"
arch=('i686' 'x86_64' 'armv6h')
url="http://cr.yp.to/publicfile.html"
license=('proprietary')
depends=('glibc')
optdepends=('ucspi-tcp' 'ucspi-ssl' 'daemontools')
source=("http://cr.yp.to/$pkgname/$pkgname-$pkgver.tar.gz"
        "http://djbware.csi.hu/patches/publicfile-$pkgver.errno.patch"
        "http://publicfile.org/redirect-slash-patch"
        "http://www.superscript.com/patches/publicfile.sslserver")
md5sums=('e493d69627b4fb2c7c764c0ff34330d7'
         'cb576aa2528b53e4a00fe1dd0d38db26'
         'c03ffd7a672ee5bc27bc5b2f4a2e4da3'
         '1abfad5628f536f9dcfff4faf112cd69')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
	patch -p1 < "../publicfile-$pkgver.errno.patch"
	patch < ../publicfile.sslserver
  patch < ../redirect-slash-patch
  echo "gcc ${CFLAGS}" > conf-cc
  echo "/usr" > conf-home
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make || return 1
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
	install -m 755 -D httpd "$pkgdir/usr/bin/httpd"
	install -m 755 -D ftpd "$pkgdir/usr/bin/ftpd"
	install -m 755 -D configure "$pkgdir/usr/bin/publicfile-configure"
}

# vim: sw=2 ts=2 ft=sh et :
