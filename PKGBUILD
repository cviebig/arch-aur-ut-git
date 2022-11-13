pkgname=ut
pkgver=1.1.9.31.g5bff64a
pkgrel=1
pkgdesc="UT: C++20 μ(micro)/Unit Testing Framework"
arch=("x86_64")
url="https://github.com/boost-ext/ut"
license=("BSL-1.0")
makedepends=('cmake' 'git')
source=('git+https://github.com/boost-ext/ut')
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/${pkgname}"
  git describe --always --tags | sed -e 's|^v||' -e 's|-|.|g'
}

build() {
  cmake -B "build/" -S "${pkgname}" \
    -D CMAKE_BUILD_TYPE:STRING="Release" \
    -D CMAKE_INSTALL_PREFIX:PATH="/usr/" \
    -Wno-dev

  cmake --build "build/"
}

package() {
  DESTDIR="${pkgdir}" cmake --install "build/"

  install -D --target-directory="${pkgdir}/usr/share/licenses/${pkgname}/" \
    --mode=644 \
    "${pkgname}/LICENSE.md"

  mkdir "${pkgdir}/usr/include/boost/"
  mv "${pkgdir}/usr/include/ut-1.1.9/include/boost/ut.hpp" "${pkgdir}/usr/include/boost/"
  rm -r "${pkgdir}/usr/include/ut-1.1.9"
}
