# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>

pkgname=qradiolink
_pkgver=0.10.2-1
pkgver="${_pkgver//-/_}"
pkgrel=1
pkgdesc='VOIP (radio over IP) GNU/Linux SDR (software defined radio) transceiver application'
arch=('x86_64')
url='https://codeberg.org/qradiolink/qradiolink'
license=('GPL-3.0-only' 'MIT' 'BSD' 'LGPL-3.0-only')
depends=('protobuf' 'boost-libs' 'qt5-base' 'qt5-multimedia' 'pulse-native-provider' 'log4cpp' 'abseil-cpp' 'opengl-driver'
         'libvolk' 'gnuradio' 'gnuradio-osmosdr' 'soapysdr' 'libuhd' 'freedv' 'codec2' 'libftdi-compat'
         'speex' 'libconfig' 'cppzmq' 'alsa-lib' 'libjpeg-turbo' 'libsndfile' 'gst-plugins-bad-libs' 'opus')
makedepends=('boost' 'limesuite' 'gst-plugins-bad')
optdepends=('limesuite: LimeSDR support')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$_pkgver.tar.gz")
sha512sums=('92f9981cf39fe646a05a226c7b19e68d88dcb35067d55ec6acb1c20519323c6f862ec00ea2e9dd6dc2d71ff0c4226de37dbc0bddb9257696589151a68d5f15ce')

prepare() {
  cd $pkgname

  cd src/ext

  protoc --cpp_out=. Mumble.proto
  protoc --cpp_out=. QRadioLink.proto
}

build() {
  mkdir -p $pkgname/build
  cd $pkgname/build

  qmake ..

  make
}

package() {
  cd $pkgname

  install -Dm 755 build/$pkgname "$pkgdir"/usr/bin/$pkgname
  install -Dm 755 $pkgname.desktop "$pkgdir"/usr/share/applications/$pkgname.desktop

  # Install docs
  install -dm 755 "$pkgdir"/usr/share/doc/$pkgname
  cp -r -a --no-preserve=ownership docs/* "$pkgdir"/usr/share/doc/$pkgname

  # Install licenses
  install -Dm 644 COPYRIGHT "$pkgdir"/usr/share/licenses/$pkgname/COPYRIGHT
  install -Dm 644 AUTHORS "$pkgdir"/usr/share/licenses/$pkgname/AUTHORS
  install -Dm 644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
  install -Dm 644 LICENSE.MIT "$pkgdir"/usr/share/licenses/$pkgname/LICENSE.MIT
  install -Dm 644 LICENSE.LGPL3 "$pkgdir"/usr/share/licenses/$pkgname/LICENSE.LGPL3
}
