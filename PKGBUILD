# Maintainer: SkyyySi

pkgname=calamares-git
_pkgname=calamares
pkgver=3.2.25.r38.g91f87ba83
pkgrel=1
pkgdesc='Distribution-independent installer framework (with configuration by SkyyySi)'
arch=('i686' 'x86_64')
license=('GPL')
url='https://calamares.io/'
depends=('kconfig'
         'kcoreaddons'
         'kiconthemes'
         'ki18n'
         'kio'
         'solid'
         'yaml-cpp'
         'kpmcore>=4.1.0'
         'boost-libs'
         'hwinfo'
         'qt5-svg'
         'polkit-qt5'
         'gtk-update-icon-cache'
         'plasma-framework'
         'qt5-xmlpatterns'
         'squashfs-tools'
         'libpwquality'
         'appstream-qt'
)
source=(
        "calamares::git+https://github.com/calamares/calamares.git#branch=master"
        "20-nopasswd-calamares.rules"
)

sha256sums=(
            "SKIP"
            "c9b7cae731437bad71c1387543d85cf658ed14fd112bec003d1b0e28d7e5a364"
)

pkgver() {
	cd "$srcdir/$_pkgname"
	git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
	cd ${srcdir}/calamares
	mkdir -p build && cd build
	cmake .. -DCMAKE_INSTALL_PREFIX=/usr
	make
}

package() {
	cd ${srcdir}/calamares/build
	make DESTDIR="$pkgdir" install
	install -Dm644 "../settings.conf" "$pkgdir/etc/calamares/settings.conf"
	install -Dm644 "$srcdir/20-nopasswd-calamares.rules" "$pkgdir/etc/polkit-1/rules.d/20-nopasswd-calamares.rules"
}
