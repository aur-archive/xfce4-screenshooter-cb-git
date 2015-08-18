# Maintainer: Zegoti
pkgname=xfce4-screenshooter-cb-git
pkgver=1.8.1.r158.g0672f29
pkgrel=1
pkgdesc="Plugin that makes screenshots for the Xfce panel - modified to support copy URL to clipboard."
arch=('i686' 'x86_64')
url="http://goodies.xfce.org/projects/applications/xfce4-screenshooter"
license=('GPL2')
groups=('xfce4-goodies')
depends=('xfce4-panel' 'libsoup' 'hicolor-icon-theme')
makedepends=('xfce4-dev-tools' 'intltool' 'git')
provides=('xfce4-screenshooter')
conflicts=('xfce4-screenshooter' 'xfce4-screenshooter-plugin')
replaces=('xfce4-screenshooter-plugin')
install=$pkgname.install
source=("$pkgname::git://git.xfce.org/apps/xfce4-screenshooter"
		"_cb.patch")
sha256sums=('SKIP' 'SKIP')
pkgver() {
	cd "$srcdir/$pkgname"
	git describe --long | sed -r 's/^xfce4-screenshooter-//;s/([^-]*-g)/r\1/;s/-/./g'
}
prepare() {
	cd "$srcdir/$pkgname"
	patch -Np1 < ../_cb.patch || return 1
#	sed -i '/^AC_USE_SYSTEM_EXTENSIONS()$/d' configure.ac.in
}
build() {
	cd "$srcdir/$pkgname"
	./autogen.sh \
		--prefix=/usr \
		--sysconfdir=/etc \
		--libexecdir=/usr/lib \
		--localstatedir=/var \
		--disable-static \
		--disable-debug
	make
}
package() {
	cd "$srcdir/$pkgname"
	make DESTDIR="$pkgdir" install
}
# vim:set ts=2 sw=2 et: 
