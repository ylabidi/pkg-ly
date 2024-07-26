# Maintainer: Christian Heusel <gromit@archlinux.org>
# Contributor: éclairevoyant
# Contributor: nullgemm <nullgemm@mailbox.org>

pkgname=ly
pkgver=1.0.0
pkgrel=2
pkgdesc="TUI display manager"
arch=(x86_64)
url="https://github.com/fairyglade/ly"
license=('WTFPL')
depends=(pam glibc)
makedepends=(git libxcb zig)
optdepends=('xorg-xauth: for X server sessions'
            'libxcb: for X server sessions')
backup=(etc/$pkgname/{config.ini,wsetup.sh,xsetup.sh})
#source=("git+$url.git#tag=v${pkgver}")
source=("git+$url.git")
b2sums=('SKIP')

build() {
    cd "$pkgname"
    zig build -Ddest_directory="$pkgdir" -Dname="ly-dm" -Dcpu=baseline
}

package() {
    cd "$pkgname"
    zig build -Ddest_directory="$pkgdir" -Dname="ly-dm" -Dcpu=baseline installsystemd
    # https://github.com/fairyglade/ly/issues/628
    chmod 644 "$pkgdir/etc/pam.d/ly" "$pkgdir/usr/lib/systemd/system/ly.service"
    sed -i "s;/usr/bin/ly;/usr/bin/ly-dm;g" "$pkgdir/usr/lib/systemd/system/ly.service"

    install -Dm644 license.md "$pkgdir/usr/share/licenses/$pkgname/WTFPL"
}
