pkgname=nextcloud-client
pkgver=2.3.3.253.e9b3656
pkgrel=1
pkgdesc='Nextcloud desktop client'
arch=('x86_64')
url="https://nextcloud.com/"
license=('GPL2')
depends=('qtwebkit-tp' 'qtkeychain' 'qt5-base' 'sqlite')
makedepends=('cmake')
conflicts=('owncloud-client')
replaces=('owncloud-client')
provides=('owncloud-client')
source=("${pkgname}::git+https://github.com/nextcloud/client_theming.git"
        'nextcloud.desktop')
md5sums=('SKIP'
         '365934e2d2afa9fe4cca7c9f0737fc3b')

pkgver() {
    cd ${pkgname}
    echo $(git tag | tail -1 | sed -e 's/^v//' | sed -e 's/\-beta[0-9]//').$(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

prepare() {
    cd ${pkgname}
    git submodule update --init --recursive
}

build() {
    mkdir -p build
    cd build
    
    cmake -DOEM_THEME_DIR=${srcdir}/${pkgname}/nextcloudtheme ../${pkgname}/client \
          -DCMAKE_INSTALL_PREFIX=/usr \
          -DCMAKE_INSTALL_LIBDIR=lib
    make
}

package() {
    cd ${srcdir}/build
    make DESTDIR=${pkgdir} install
    rm ${pkgdir}/usr/share/applications/nextcloud.desktop
    rm -rf ${pkgdir}/usr/share/*-python
    install -Dm644 ${srcdir}/nextcloud.desktop \
            ${pkgdir}/usr/share/applications/nextcloud.desktop
}
