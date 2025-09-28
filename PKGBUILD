# Maintainer: artist for Artix Linux
# Maintainer: karpal

pkgname="ly"
pkgver="1.1.2"
pkgrel="1"
pkgdesc="Lightweight TUI (ncurses-like) display manager"
arch=("x86_64")
url="https://codeberg.org/fairyglade/ly"
license=("WTFPL")
depends=("pam" "glibc")
makedepends=("libxcb" "mise")
optdepends=("brightnessctl: for controling brightness"
            "xorg-xmessage: for displaying a message or query in a window"
            "xorg-xauth: for X server sessions"
            "libxcb: for X server sessions")

source=("https://codeberg.org/fairyglade/ly/archive/v${pkgver}.tar.gz"
        "dinit.patch"
        "config_ini.patch")

sha256sums=("8f491d09045bb680680b553556f9db7af89c6644a257352839f98c4e98028fd0"
            "7b3c76731bc040cbee0534db3972468d374ec041e57cfc7f4822c39552d00a68"
            "9bbc0bece696d34e92f0b83ed3b3edcc9806cf88c03ed0e48b600fece32795a9")

zig_version="0.14.1"

prepare() {
    mise use "zig@${zig_version}"
    mise reshim
    export PATH="${PATH}:$(mise where zig)"
    cd "${srcdir}/${pkgname}"
    patch -Np1 -i "${srcdir}/dinit.patch"
    patch -Np1 -i "${srcdir}/config_ini.patch"
}

build() {
    cd "${srcdir}/${pkgname}"
    zig build -Ddest_directory="${pkgdir}" -Dname="ly-dm" \
      -Dcpu=baseline -Doptimize=ReleaseSafe -Dinit_system=dinit \
      -Denable_x11_support=false
}

package() {
    cd "${pkgname}"
    zig build -Ddest_directory="${pkgdir}" -Dname="ly-dm" \
      -Ddefault_tty=1 -Dcpu=baseline -Doptimize=ReleaseSafe \
      -Dinit_system=dinit -Denable_x11_support=false installexe
    install -Dm644 license.md "${pkgdir}/usr/share/licenses/${pkgname}/WTFPL"
}

