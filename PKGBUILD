# Maintainer: Christian Heusel <gromit@archlinux.org>
# Contributor: éclairevoyant
# Contributor: nullgemm <nullgemm@mailbox.org>

pkgname=ly
pkgver=1.0.1
pkgrel=1
pkgdesc="TUI display manager"
arch=(x86_64)
url="https://github.com/fairyglade/ly"
license=('WTFPL')
depends=(pam glibc)
makedepends=(git libxcb zig)
optdepends=('xorg-xauth: for X server sessions'
            'libxcb: for X server sessions')
backup=(etc/$pkgname/{config.ini,wsetup.sh,xsetup.sh})
source=("https://github.com/fairyglade/ly/archive/refs/tags/v1.0.1.tar.gz")
b2sums=('daf90c17ab467d71ba24f65ff42a36ca008c20a1b0706e158a580b1ee3c11bf0d93dacb3531359797d3c5cf2290daf792ef9c0621bbab8993b530536b2d08376')

build() {
    cd "$pkgname-$pkgver"
    zig build -Ddest_directory="$pkgdir" -Dname="ly-dm" -Dcpu=baseline
}

package() {
    cd "$pkgname-$pkgver"
    zig build -Ddest_directory="$pkgdir" -Dname="ly-dm" -Dcpu=baseline installsystemd
    # https://github.com/fairyglade/ly/issues/628
    chmod 644 "$pkgdir/etc/pam.d/ly" "$pkgdir/usr/lib/systemd/system/ly.service"
    sed -i "s;/usr/bin/ly;/usr/bin/ly-dm;g" "$pkgdir/usr/lib/systemd/system/ly.service"

    install -Dm644 license.md "$pkgdir/usr/share/licenses/$pkgname/WTFPL"
}

