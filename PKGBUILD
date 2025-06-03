# Maintainer: artist for Artix Linux

pkgname=ly
pkgver=1.1.0
pkgrel=1
pkgdesc="Lightweight TUI (ncurses-like) display manager"
arch=(x86_64)
url="https://codeberg.org/AnErrupTion/ly"
license=('WTFPL')
depends=(pam glibc)
makedepends=(libxcb zig)
optdepends=('brightnessctl: for controling brightness'
            'xorg-xmessage: for displaying a message or query in a window'
            'xorg-xauth: for X server sessions'
            'libxcb: for X server sessions')
backup=(etc/$pkgname/{config.ini,setup.sh}
        etc/pam.d/ly)
source=("$url/archive/v$pkgver.tar.gz"
        config_ini.patch)
b2sums=('94eadef7552110288c3dfa0b564b6982f58f4ec6b46d7a9803acd2e102ca3d43367fb7cf67e39bc56e0a571a99b52a02b7fa5cd63afcd8f7cd5c070d957f9456'
        '17c966e9bd9f578e1e9dc14d3ca212af388d87eba3fcc03315afb67818e57d9127f43c5e49e71f46b5ca1f25e19a84568152b76b573e64a3a9ce9e59e84d8662')

prepare() {
    cd "$pkgname"
    sed -i '/try install_service(allocator, patch_map);/d' build.zig
    patch -Np1 -i $srcdir/config_ini.patch
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

