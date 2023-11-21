pkgname=rogue-enemy-git
pkgver=1.0.0
pkgrel=2
pkgdesc='Convert ROG Ally [RC71L] input to DualShock4 and allows mode switching with a long CC press'
arch=('x86_64')
url='https://github.com/NeroReflex/ROGueENEMY/'
license=('GPLv2')
depends=()
makedepends=('cmake')
provides=('rogue-enemy')
source=(
    "rogue-enemy::git+https://github.com/NeroReflex/ROGueENEMY.git#branch=main"
    "rogue-enemy.service"
)
sha256sums=(
    'SKIP'
    'f0571dc1047fa892a200ccdaede9fed4d0af2478808e42da20d68f4673170927' # rogue-enemy.service
)

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
    #cd "${pkgname}-${pkgver}"
    
    # systemd
    install -D -m644 rogue-enemy.service   -t "${pkgdir}/usr/lib/systemd/system/"
    
    # license
    #install -D -m644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}