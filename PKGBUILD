# Maintainer: artist for Artix Linux

pkgname=ly
pkgver=1.0.3
pkgrel=1
pkgdesc="TUI display manager"
arch=(x86_64)
url="https://github.com/fairyglade/$pkgname"
license=('WTFPL')
depends=(pam glibc libxcb)
makedepends=(git zig)
optdepends=('brightnessctl: for controling brightness'
            'xorg-xmessage: for displaying a message or query in a window'
            'xorg-xauth: for X server sessions'
            'libxcb: for X server sessions')
backup=(etc/$pkgname/{config.ini,wsetup.sh,xsetup.sh})
source=("git+$url.git#tag=v${pkgver}")
b2sums=('f5ac7d949487d70e0102b595f5d8b31615071f3edcc90e1d15285ad46843147bcda2510e4c946dbe123c326f3d1ed407d2ed4e7adac0370a7af2750a757c61f8')

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

