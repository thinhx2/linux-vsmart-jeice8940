# Kernel config based on: arch/arm/configs/PQ4001_defconfig

pkgname=linux-vsmart-jeice8940
pkgver=3.18.31
pkgrel=2
pkgdesc="Joy 1 kernel fork"
arch="armhf"
_carch="arm"
_flavor="vsmart-jeice8940"
url="https://kernel.org"
license="GPL2"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="perl sed installkernel bash gmp-dev bc linux-headers elfutils-dev devicepkg-dev gcc6"

# Compiler: this kernel was only tested with GCC6. Feel free to make a merge
# request if you find out that it is booting working with newer GCCs as
# well. See <https://postmarketos.org/vendorkernel> for instructions.
if [ "${CC:0:5}" != "gcc6-" ]; then
	CC="gcc6-$CC"
	HOSTCC="gcc6-gcc"
	CROSS_COMPILE="gcc6-$CROSS_COMPILE"
fi

# Source
_repository="joy-1"
_commit="c12cc104cdaf231bdbf306be63db77c66ae27591"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/thinhx2/$_repository/archive/$_commit.tar.gz
	$_config
"
builddir="$srcdir/$_repository-$_commit"

prepare() {
	default_prepare
	. downstreamkernel_prepare
}

build() {
	unset LDFLAGS
	make ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
	downstreamkernel_package "$builddir" "$pkgdir" "$_carch" "$_flavor"
}

sha512sums="3ee5d0b963028ccca58c05b6f41d09116b05dfce50cf8b13be6d8fe24326b78d67caab96098bda9a0ab9567c04aad0925502a3d6a1801300152230e3a6c22c74  linux-vsmart-jeice8940-c12cc104cdaf231bdbf306be63db77c66ae27591.tar.gz
c9662e9bd46b78a7e958a3db663a231664976f8b5bed6b4d2630a85c3c508ab566e029553c7684bfb120b9583e01c74e6bac97f15c90a8a7095c6cd9debc17e1  config-vsmart-jeice8940.armhf"
