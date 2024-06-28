pkgname=nextcloud-client
pkgver=3.13.1
pkgrel=1
pkgdesc='Nextcloud desktop client'
arch=('x86_64')
url="https://nextcloud.com/"
license=('GPL2')
makedepends=('cmake')
depends=('karchive' 'openssl' 'qt5-graphicaleffects' 'qt5-quickcontrols2' 'qt5-svg'
         'qt5-tools' 'qt5-websockets' 'qtkeychain' 'qtwebengine' 'sqlite' 'xdg-utils')
backup=('etc/Nextcloud/sync-exclude.lst')
source=("https://github.com/nextcloud/desktop/archive/v${pkgver}.tar.gz")
md5sums=('aa99c899b187dd9af4886843875e1dad')

build() {
    mkdir -p build
    cd build

    cmake ../desktop-${pkgver} \
          -DCMAKE_BUILD_TYPE=Release \
          -DCMAKE_INSTALL_PREFIX=/usr \
          -DBUILD_SHELL_INTEGRATION_DOLPHIN=$(usex dolphin)
    make
}

package() {
    cd ${srcdir}/build
    make DESTDIR=${pkgdir} install
    rm -rf ${pkgdir}/usr/share/*-python
}
