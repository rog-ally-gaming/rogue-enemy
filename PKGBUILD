pkgname=rogue-enemy-git
pkgver=1.3.0
pkgrel=1
pkgdesc='Convert ROG Ally [RC71L] input to DualShock4 and allows mode switching with a long CC press'
arch=('x86_64')
url='https://github.com/NeroReflex/ROGueENEMY/'
license=('GPLv2')
depends=(
    'libconfig'
    'libevdev'
)
makedepends=('cmake')
provides=('rogue-enemy')
source=(
    "rogue-enemy::git+https://github.com/NeroReflex/ROGueENEMY.git#branch=main"
    "rogue-enemy.service"
)
sha256sums=(
    'SKIP'
    'e7c8d03c3a9a516541bbacffd5cf3cf2c1ac209fde303e946d36ce1290bb7081' # rogue-enemy.service
)
options=(lto)

prepare() {
    cd "rogue-enemy"
    #mkdir "ally-motion-evdev/build"
    cd ..
}

build() {
    cmake \
        -B build \
        -S "rogue-enemy" \
        -G 'Unix Makefiles' \
        -DCMAKE_BUILD_TYPE:STRING='Release' \
        -DCMAKE_INSTALL_PREFIX:PATH='/usr' \
        -Wno-dev
    cmake --build build
}

#check() {
#    ctest --test-dir build --output-on-failure
#}

package() {
    DESTDIR="$pkgdir" cmake --install build

    # systemd
    install -D -m644 rogue-enemy.service   -t "${pkgdir}/usr/lib/systemd/system/"

    mkdir -p "$pkgdir/etc/ROGueENEMY"
    install -D -m644 rogue-enemy/config.cfg.default   -t "$pkgdir/etc/ROGueENEMY/config.cfg"

    # license
    install -D -m644 rogue-enemy/LICENSE.md -t "${pkgdir}/usr/share/licenses/${pkgname}"
}