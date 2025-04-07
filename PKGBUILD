# Maintainer: Christian Heusel <gromit@archlinux.org>
# Contributor: éclairevoyant
# Contributor: nullgemm <nullgemm@mailbox.org>

pkgname=ly
pkgver=1.0.3
pkgrel=2
pkgdesc="TUI display manager"
arch=(x86_64)
url="https://github.com/fairyglade/ly"
license=('WTFPL')
depends=(pam glibc libxcb)
makedepends=(git zig)
optdepends=('xorg-xauth: for X server sessions'
            'libxcb: for X server sessions')
backup=(
    etc/$pkgname/{config.ini,wsetup.sh,xsetup.sh}
    etc/pam.d/ly
)
source=("git+$url.git#tag=v${pkgver}")
b2sums=('f5ac7d949487d70e0102b595f5d8b31615071f3edcc90e1d15285ad46843147bcda2510e4c946dbe123c326f3d1ed407d2ed4e7adac0370a7af2750a757c61f8')

build() {
    cd "$pkgname"
    zig build -Ddest_directory="$pkgdir" -Dname="ly-dm" -Dcpu=baseline -Doptimize=ReleaseSafe
}

package() {
    cd "$pkgname"
    zig build -Ddest_directory="$pkgdir" -Dname="ly-dm" -Dcpu=baseline -Doptimize=ReleaseSafe installnoconf


    install -Dm644 license.md "$pkgdir/usr/share/licenses/$pkgname/WTFPL"
}
