# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm64/configs/(CHANGEME!)
#	gcc7-give-up-on-ilog2-const-optimizations.patch
#	gcc8-fix-put-user.patch
#	gcc10-extern_YYLOC_global_declaration.patch
#	kernel-use-the-gnu89-standard-explicitly.patch


pkgname=linux-sony-kagura
pkgver=3.16.1
pkgrel=0
pkgdesc="Sony Xperia XZ kernel fork"
arch="aarch64"
_carch="arm64"
_flavor="sony-kagura"
url="https://kernel.org"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="
	bash
	bc
	bison
	devicepkg-dev
	flex
	openssl-dev
	perl
"

# Source
_repository="kernel-sony-kagura"
_commit="2db6193efd09a9c84523ef0e58e7ab6cd88fbcfa"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/lightwe1ght/$_repository/archive/$_commit.tar.gz
	$_config
"
builddir="$srcdir/$_repository-$_commit"
_outdir="out"

prepare() {
	default_prepare
	REPLACE_GCCH=0
	. downstreamkernel_prepare
}

build() {
	unset LDFLAGS
	make O="$_outdir" ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
	downstreamkernel_package "$builddir" "$pkgdir" "$_carch" \
		"$_flavor" "$_outdir"
}

sha512sums="
3d3f10484ec0a0ac77e6d41e4ac1640a41dfc98f02fe4da68f05887de7981f725c353ed41856ca842afad8d6864e4a707038b7bd5f825afb4be306b64c83f07d  linux-sony-kagura-2db6193efd09a9c84523ef0e58e7ab6cd88fbcfa.tar.gz
63e443159300d949bb2668a66b05666dc8317f74adbe6cf96ca0862419a196cdce9dc4f03b20eb2f2386450c19b5abde492fc61e9500f68c22c3bb0c990c4f80  config-sony-kagura.aarch64
"
