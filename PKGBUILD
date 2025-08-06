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
        '17c966e9bd9f578e1e9dc14d3ca212af388d87eba3fcc03315afb67818e57d9127f43c5e49e71f46b5ca1f25e19a84568152b76b573e64a3a9ce9e59e84d8662')

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

