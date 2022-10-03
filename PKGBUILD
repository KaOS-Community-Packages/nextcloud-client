pkgname=nextcloud-client
pkgver=3.6.0
pkgrel=1
pkgdesc='Nextcloud desktop client'
arch=('x86_64')
url="https://nextcloud.com/"
license=('GPL2')
depends=('qtkeychain' 'qt5-base' 'sqlite')
makedepends=('cmake')
backup=('etc/Nextcloud/sync-exclude.lst')
source=("https://github.com/nextcloud/desktop/archive/v${pkgver}.tar.gz"
        'nextcloud.desktop')
md5sums=('bde47b6eb64a1434c5695ef0075c3076'
         '365934e2d2afa9fe4cca7c9f0737fc3b')

build() {
    mkdir -p build
    cd build
    
    cmake ../desktop-${pkgver} \
          -DCMAKE_BUILD_TYPE=Release \
          -DCMAKE_INSTALL_PREFIX=/usr
    make
}

package() {
    cd ${srcdir}/build
    make DESTDIR=${pkgdir} install
}
