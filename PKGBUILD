pkgname=st-toki83w
_pkgname=st-graphics
pkgver=0.9.2
pkgrel=1
pkgdesc="Simple (suckless) terminal"
url='https://github.com/toki83w/st-graphics'
arch=('x86_64')
license=('MIT')
options=()
depends=('libxft' 'imlib2' 'zlib' 'harfbuzz' 'dmenu')
makedepends=('ncurses' 'libxext' 'git')
source=(git+https://github.com/toki83w/st-graphics)
sha1sums=('SKIP')

provides=("$pkgname")
conflicts=("$pkgname" "$_pkgname" "st")

pkgver() {
    cd "$_pkgname"
    printf "%s.r%s.%s" "$(awk '/^VERSION =/ {print $3}' config.mk)" \
        "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    cd "$srcdir/$_pkgname"
    # skip terminfo which conflicts with ncurses
    sed -i '/tic /d' Makefile
    # create config.h
    cp config.def.h config.h
}

build() {
    cd "$_pkgname"
    make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
    cd "$_pkgname"
    make PREFIX=/usr DESTDIR="$pkgdir" install
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}
