
_compiler=gcc

_realname=objfw-rel
pkgbase=mingw-w64-${_realname}

pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")

pkgver=0.8.1
pkgrel=0
pkgdesc="A portable framework for the Objective-C language (mingw-w64)"
arch=('any')
url="https://heap.zone/objfw/"
license=("GPL")
makedepends=("autoconf"
			 "make"
			 "${MINGW_PACKAGE_PREFIX}-binutils"
			 "${MINGW_PACKAGE_PREFIX}-gcc")
#			 "${MINGW_PACKAGE_PREFIX}-clang")

depends=("${MINGW_PACKAGE_PREFIX}-clang")

conflicts=("${MINGW_PACKAGE_PREFIX}-objfw")

source=("https://github.com/Midar/objfw/archive/${pkgver}-release.tar.gz")

sha256sums=('SKIP')

noextract=(${pkgver}-release.tar.gz)

prepare() {
	plain "Extracting ${pkgver}-release.tar.gz"
	[[ -d ${srcdir}/objfw-${pkgver}-release ]] || tar -xzf ${pkgver}-release.tar.gz -C ${srcdir} || true

	cd "${srcdir}"/objfw-${pkgver}-release

	[[ -f ./configure ]] || ./autogen.sh || true

}

configure_objfw() {
	cd "${srcdir}"/objfw-${pkgver}-release

	./configure --prefix="" \
	 --enable-static \
	 --enable-runtime \
	 --enable-seluid24 \
	 OBJC=${_compiler}
}

build() {
	cd "${srcdir}"/objfw-${pkgver}-release

	[[ -f ./buildsys.mk ]] && make distclean && configure_objfw || configure_objfw || true

	make
}

package_objfw-rel() {
	pkgdesc="A portable framework for the Objective-C language (mingw-w64)"
	url="https://heap.zone/objfw/"
	depends=("${MINGW_PACKAGE_PREFIX}-clang")

	cd "${srcdir}"/objfw-${pkgver}-release

	make DESTDIR="${pkgdir}" install
}

package_mingw-w64-i686-objfw-rel() {
	package_objfw-rel
}

package_mingw-w64-x86_64-objfw-rel() {
	package_objfw-rel
}