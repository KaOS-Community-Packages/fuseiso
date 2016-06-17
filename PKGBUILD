pkgname=fuseiso
pkgver=07.07.08
pkgrel=1
pkgdesc="FUSE module to mount ISO filesystem images"
arch=('x86_64')
url="http://sourceforge.net/projects/fuseiso/"
license=('GPL')
depends=('fuse' 'glib2' 'zlib')
makedepends=('pkg-config')
source=("http://ubiz.ru/dm/${pkgname}-20${pkgver//./}.tar.bz2"
	"00-support_large_iso.patch"
	"01-fix_typo.patch"
	"02-prevent-buffer-overflow.patch"
	"03-prevent-integer-overflow.patch"
	"fuseisomenu.sh" 
	"fuseisomenu.desktop")
md5sums=('4bb50412b6d01f337565e28afddca3a5'
         'f48d99f3928c6caf62fc1d58c99b31ed'
         'd5b5f328f4dc23a7a97b46b09d30e48c'
         'fcc34d91eeab5e243c4ac7768b9f3c4c'
         'f2bacb988113ac28a71e3f136c61c4bf'
         'ab404d76ce88b5341c7203c393addf9d'
         '650f04ed8d862a405cc0ee166b2e5117')

build() {
  cd ${srcdir}/${pkgname}-20${pkgver//./}
  # Patchset from debian
  patch -Np1 -i "${srcdir}"/00-support_large_iso.patch
  patch -Np1 -i "${srcdir}"/01-fix_typo.patch
  patch -Np1 -i "${srcdir}"/02-prevent-buffer-overflow.patch
  patch -Np1 -i "${srcdir}"/03-prevent-integer-overflow.patch

  ./configure --prefix=/usr
  make
}

package() {
    install -Dm755 ../fuseisomenu.sh "$pkgdir/usr/share/kservices5/ServiceMenus/fuseisomenu.sh"
    install -Dm755 ../fuseisomenu.desktop "$pkgdir/usr/share/kservices5/ServiceMenus/fuseisomenu.desktop"
  cd ${srcdir}/${pkgname}-20${pkgver//./}
  make DESTDIR=${pkgdir} install
}
