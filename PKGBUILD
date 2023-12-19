pkgname=rogue-enemy-git
pkgver=1.5.1
pkgrel=2
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
    "rogue-enemy::git+https://github.com/NeroReflex/ROGueENEMY.git#branch=devel"
    "rogue-enemy.service"
    "stray-ally.service"
)
sha256sums=(
    'SKIP'
    '3ab522c778217c4633219824b1f950eb4526b89b3fae554f33c07ed388fcd71c' # rogue-enemy.service
    '0b93fbd7cd0910caba97f68dbfa23f5a7df5bdcc10fa49014ed4c7a7d62ecd0a' # stray-ally.service
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
    install -D -m644 stray-ally.service   -t "${pkgdir}/usr/lib/systemd/system/"

    mkdir -p "$pkgdir/etc/ROGueENEMY"

    install -D -m755 rogue-enemy/rogue-enemy_iio_buffer_on.sh -t "$pkgdir/usr/bin/"
    install -D -m755 rogue-enemy/rogue-enemy_iio_buffer_off.sh -t "$pkgdir/usr/bin/"
    install -D -m644 rogue-enemy/80-playstation.rules -t "$pkgdir/usr/lib/udev/rules.d/"

    install -D -m644 rogue-enemy/config.cfg.default   -t "$pkgdir/etc/ROGueENEMY/"
    mv "$pkgdir/etc/ROGueENEMY/config.cfg.default" "$pkgdir/etc/ROGueENEMY/config.cfg"

    # license
    install -D -m644 rogue-enemy/LICENSE.md -t "${pkgdir}/usr/share/licenses/${pkgname}"
}