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
source=("git+$url.git#tag=v${pkgver}")
b2sums=('6735af4944bac5b259f2da064c8f0ca57df908e21315a16af846d28650c6372476b633ce2d5449aca29e7077728e0b40205bce9f47def5924f1755f60bf07025')

prepare() {
    cd "$pkgname"
    git cherry-pick -n cbe7b37564f307fddfeba3732c68d5024d30f4f7
}

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

