## $Id$
# Maintainer: Chupligin Sergey (NeoChapay) <neochapay@gmail.com>

pkgname=ohm-plugins-misc
pkgver=1.10.0
pkgrel=1
pkgdesc="A miscallaneous set of OHM plugins"
arch=('x86_64' 'aarch64')
url="https://github.com/sailfishos/ohm-plugins-misc"
license=('LGPL-2.1-only')
depends=('glib2' 'ohm' 'libdres-ohm' 'libresource' 'python')
makedepends=('automake' 'autoconf')
source=("${url}/archive/refs/tags/$pkgver.tar.gz")
sha256sums=('5cee527151cca74a97abf4244449f865a2f066871c07df8b91b60386535be190')

prepare() {
    cd $pkgname-$pkgver
    echo "$pkgver" > .tarball-version
    ./autogen.sh
}

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr \
    --sysconfdir=/etc \
    --sbindir=/usr/bin \
    --disable-static \
    --enable-telephony \
    --disable-notification \
    --disable-videoep \
    --disable-fmradio
  make -j1
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="${pkgdir}" install
  sed -i 's/pre-user-session.target/graphical-session-pre.target/' "${pkgdir}/usr/lib/systemd/user/ohm-session-agent.service"
}
