pkgname=nextcloud-client
pkgver=3.14.0
pkgrel=2
pkgdesc='Nextcloud desktop client'
arch=('x86_64')
url="https://nextcloud.com/"
license=('GPL2')
makedepends=('cmake' 'extra-cmake-modules' 'doxygen')
depends=('karchive6' 'openssl' 'qtkeychain-qt6' 'qt6-tools' 'qt6-webengine' 'qt6-svg' 'sqlite' 'xdg-utils')
backup=('etc/Nextcloud/sync-exclude.lst')
source=("https://github.com/nextcloud/desktop/archive/v${pkgver}.tar.gz")
md5sums=('18b88820573a0985904d2517ad703407')

build() {
    mkdir -p build
    cd build

    cmake ../desktop-${pkgver} \
          -DCMAKE_BUILD_TYPE=Release \
          -DCMAKE_INSTALL_PREFIX=/usr \
          -DBUILD_SHELL_INTEGRATION_DOLPHIN=on
    make
}

package() {
    cd ${srcdir}/build
    make DESTDIR=${pkgdir} install
    rm -rf ${pkgdir}/usr/share/*-python
}
