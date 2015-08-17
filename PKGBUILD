# Maintainer: György Balló <ballogy@freestart.hu>
pkgname=tasque
pkgver=0.1.9
pkgrel=5
pkgdesc="Easy quick task management"
arch=('any')
url="http://live.gnome.org/Tasque"
license=('MIT')
depends=('notify-sharp' 'sqlite3' 'hicolor-icon-theme' 'xdg-utils')
makedepends=('intltool' 'gnome-common')
install=$pkgname.install
source=(http://ftp.gnome.org/pub/GNOME/sources/$pkgname/${pkgver%.*}/$pkgname-$pkgver.tar.bz2
        drop-gnome-sharp-dependency.patch
        drop-gconf-dependency.patch
        use-dbus-sharp.patch)
sha256sums=('1749b0c5a60d74f05f36193ff4aaf5b130ed3a47726f0b8e48c712805d1341af'
            'f6b319b32579d8f5e3df7bd0691d90c138df6a714d9e20c359a4bdf4bffdcb36'
            'da51a83d35b21bfc62459fa1c9cd22976dc1b82c6f725ed7ab75e502f00922f8'
            '69974bd9e3b055d9de6c7f8e143a999ea57c1ccc5d2badc26d754225adf5bf0c')

build() {
  cd "$srcdir/$pkgname-$pkgver"

  # Remove some dependencies
  patch -Np1 -i "$srcdir/drop-gnome-sharp-dependency.patch"
  patch -Np1 -i "$srcdir/drop-gconf-dependency.patch"
  patch -Np1 -i "$srcdir/use-dbus-sharp.patch"
  sed -i 's/pkglib_DATA/pkgdata_DATA/' Makefile.am

  autoreconf -fi
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
              --disable-static --disable-backend-eds
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
  install -Dm644 COPYING ${pkgdir}/usr/share/licenses/$pkgname/COPYING
}
