pkgname=nextcloud-client
pkgver=3.15.0
pkgrel=1
pkgdesc='Nextcloud desktop client'
arch=('x86_64')
url="https://nextcloud.com/"
license=('GPL2')
makedepends=('cmake' 'extra-cmake-modules' 'doxygen' 'librsvg')
depends=('karchive6' 'openssl' 'qtkeychain-qt6' 'qt6-tools' 'qt6-webengine' 'qt6-svg' 'sqlite' 'xdg-utils')
backup=('etc/Nextcloud/sync-exclude.lst')
source=("https://github.com/nextcloud/desktop/archive/v${pkgver}.tar.gz")
md5sums=('713ef1e3cca202b66b7691b9dbc30e00')

prepare() {
    cd "desktop-${pkgver}"

    # Force use of rsvg-convert instead of inkscape to generate icons
    sed -i 's|inkscape inkscape.exe ||' cmake/modules/GenerateIconsUtils.cmake
}

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
