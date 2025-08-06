# Maintainer: artist for Artix Linux

pkgname=ly
pkgver=1.1.2
pkgrel=1
pkgdesc="Lightweight TUI (ncurses-like) display manager"
arch=(x86_64)
url="https://codeberg.org/AnErrupTion/ly"
license=('WTFPL')
depends=(pam glibc)
makedepends=(git libxcb zig)
optdepends=('brightnessctl: for controling brightness'
            'xorg-xmessage: for displaying a message or query in a window'
            'xorg-xauth: for X server sessions'
            'libxcb: for X server sessions')
backup=(etc/$pkgname/{config.ini,setup.sh}
        etc/pam.d/ly)
source=("git+$url.git#tag=v${pkgver}"
        config_ini.patch)
b2sums=('20464d125d8528f82676839ed21ea2d9b8f688732a19755b245d08e6d1269f15e89ebd26bc895462d66e4a6562cee11ce604ec0fee70e13246619df69f5dffc7'
        '7abef765e27adf9950538f6e70ba1b1970ea48196535a7507f148169ada1ad299ae334ca59cf0bc657bca4b1ccf22d005584b8af3ecfdf6b1a2b0f21db2051e1')

prepare() {
    cd "$pkgname"
    sed -i '/try install_service(allocator, patch_map);/d' build.zig
    patch -Np1 -i "$srcdir/config_ini.patch"
}

build() {
    cd "$pkgname"
    zig build -Ddest_directory="$pkgdir" -Dname="ly-dm" -Dcpu=baseline -Doptimize=ReleaseSafe
}

package() {
    cd "$pkgname"
    zig build -Ddest_directory="$pkgdir" -Dname="ly-dm" -Ddefault_tty=7 -Dcpu=baseline -Doptimize=ReleaseSafe installexe
    install -Dm644 license.md "$pkgdir/usr/share/licenses/$pkgname/WTFPL"
}

