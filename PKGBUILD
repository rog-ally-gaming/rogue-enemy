pkgname=rogue-enemy-git
pkgver=1.1.0
pkgrel=3
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
    "config.cfg"
)
sha256sums=(
    'SKIP'
    'f0571dc1047fa892a200ccdaede9fed4d0af2478808e42da20d68f4673170927' # rogue-enemy.service
    '3ae95a193ba346e805e6234f1c325b1d2830272d834a74623f7a3bb54bb420d1' # config.cfg
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
    #DESTDIR="$pkgdir" cmake --install build
    #cd "${pkgname}-${pkgver}"
    mkdir -p "$pkgdir/usr/bin"
    install -D -m755 build/ROGueENEMY      -t "$pkgdir/usr/bin/"
    
    # systemd
    install -D -m644 rogue-enemy.service   -t "${pkgdir}/usr/lib/systemd/system/"
    
    mkdir -p "$pkgdir/etc/ROGueENEMY"
    install -D -m644 config.cfg   -t "$pkgdir/etc/ROGueENEMY/"

    # license
    install -D -m644 rogue-enemy/LICENSE.md -t "${pkgdir}/usr/share/licenses/${pkgname}"
}