# Maintainer: Your Name <your.email@example.com>
pkgname=mumble-9m2pju-git
pkgver=1.6.870.r117.gc0fa619
pkgrel=1
pkgdesc="Open source, low-latency, high-quality voice chat software (Client only, 9m2pju custom Git version)"
arch=('x86_64' 'aarch64')
url="https://www.mumble.info"
license=('BSD-3-Clause')
depends=(
  'alsa-lib'
  'avahi'
  'libcap'
  'libpulse'
  'libsndfile'
  'openssl'
  'opus'
  'poco'
  'protobuf'
  'qt6-base'
  'qt6-svg'
  'rnnoise'
  'speex'
  'speexdsp'
)
makedepends=(
  'boost'
  'cmake'
  'git'
  'ninja'
  'pkgconf'
  'qt6-tools'
)
provides=('mumble' 'mumble-client')
conflicts=('mumble' 'mumble-client')
source=("mumble::git+https://github.com/mumble-voip/mumble.git")
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/mumble"
  git describe --long --tags --abbrev=7 2>/dev/null | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g' || \
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "$srcdir/mumble"
  git submodule update --init --recursive
}

build() {
  export CFLAGS="${CFLAGS/-Wp,-D_FORTIFY_SOURCE=?/}"
  export CXXFLAGS="${CXXFLAGS/-Wp,-D_FORTIFY_SOURCE=?/}"
  export CPPFLAGS="${CPPFLAGS/-Wp,-D_FORTIFY_SOURCE=?/}"

  cmake -B build -S mumble \
    -G Ninja \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -Dclient=ON \
    -Dserver=OFF \
    -Doverlay=ON \
    -Dplugins=ON \
    -Dspeechd=OFF \
    -Dwarnings-as-errors=OFF
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
  install -Dm644 "$srcdir/mumble/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
