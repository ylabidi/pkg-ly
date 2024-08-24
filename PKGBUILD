# Maintainer: artist for Artix Linux

pkgname=ly
pkgver=1.0.2
pkgrel=1.4
pkgdesc="TUI display manager"
arch=(x86_64)
url="https://github.com/fairyglade/$pkgname"
license=('WTFPL')
depends=(pam glibc)
makedepends=(git libxcb zig)
optdepends=('brightnessctl: for controling brightness'
            'xorg-xmessage: for displaying a message or query in a window'
            'xorg-xauth: for X server sessions'
            'libxcb: for X server sessions')
backup=(etc/$pkgname/{config.ini,wsetup.sh,xsetup.sh})
source=("git+$url.git#tag=v${pkgver}")
b2sums=('39738a0a00cddf2c986a33e78f28d6f241a1d4b342aca59a8e723fd005f079a34e5da19b3a870bfdb2739f4f7e1b04eace2f3187db310c92cdf71a6f89962035')

prepare() {
    cd "$pkgname"
    git cherry-pick -n fadbbf676ad88e57cecffd501b5a4d4634064688
}

build() {
    cd "$pkgname"
    zig build -Ddest_directory="$pkgdir" -Dname="ly-dm" -Dcpu=baseline -Doptimize=ReleaseSafe
}

package() {
    cd "$pkgname"
    zig build -Ddest_directory="$pkgdir" -Dname="ly-dm" -Dcpu=baseline -Doptimize=ReleaseSafe installnoconf
    install -Dm644 res/config.ini "$pkgdir/etc/$pkgname/config.ini"
    sed -i 's|tty = 2|tty = 7|' "$pkgdir"/etc/$pkgname/config.ini
    sed -i 's|$CONFIG_DIRECTORY|/etc|' "$pkgdir"/etc/$pkgname/config.ini
    sed -i 's|$PREFIX_DIRECTORY|/usr|' "$pkgdir"/etc/$pkgname/config.ini
    install -Dm644 license.md "$pkgdir/usr/share/licenses/$pkgname/WTFPL"
}

