pkgname=nextcloud-client
pkgver=2.2.3
pkgrel=1
pkgdesc='Nextcloud desktop client'
arch=('x86_64')
url='https://nextcloud.com/'
license=('GPL2')
depends=('qt5-webkit' 'neon' 'qtkeychain' 'qt5-base' 'sqlite')
makedepends=('cmake' )
conflicts=('owncloud-client')
source=("${pkgname}::git+https://github.com/nextcloud/client_theming.git")
sha256sums=('SKIP')
backup=('etc/Nextcloud/sync-exclude.lst')

prepare() {
  cd "${srcdir}/${pkgname}"
  git submodule update --init
  cd client
  git submodule update --init

  mkdir "${srcdir}/${pkgname}/build-linux"
}

build() {
  cd "${srcdir}/${pkgname}/build-linux"

  cmake -D OEM_THEME_DIR=${srcdir}/${pkgname}/nextcloudtheme ../client \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=lib \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_SYSCONFDIR=/etc/${pkgname}

  make
}

package() {
  cd "${srcdir}/${pkgname}/build-linux"
  make DESTDIR="${pkgdir}" install
}
