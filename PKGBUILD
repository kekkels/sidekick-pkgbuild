# Maintainer:Kekkels <kekkels@protonmail.com>
pkgname=sidekick-git
_gitname=${pkgname%-git}
pkgver=2025.124.549.r13.gbbbf4ed
pkgver() {
	cd "$_gitname"
	git describe --long --tags --abbrev=7 | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}
pkgrel=1
pkgdesc="A pricecheck/map regex tool for POE2"
arch=(x86_64)
url="https://github.com/Sidekick-Poe/Sidekick"
license=('MIT')
groups=()
depends=(
  dotnet-runtime-8.0
  aspnet-runtime-8.0
  nodejs
)
makedepends=(
  dotnet-sdk-8.0
  npm
  git
)
checkdepends=()
optdepends=()
provides=("sidekick=$pkgver")
conflicts=(sidekick)
replaces=()
backup=()
options=()
install=
changelog=
source=(
  "git+$url.git#branch=main"
  Sidekick.desktop
  sidekick-start.sh
)
noextract=()
md5sums=('SKIP'
         '5a5a42d482aee5de2712641abc374331'
         '89161d4c123787f6f6cf783267b2057b')

prepare() {
	cd "$srcdir"
	mv Sidekick "$_gitname"
	cd "$_gitname"
	patch -N --strip=0 --input=../../sidekick-sln.patch
}

build() {
	cd "$srcdir/$_gitname"
	dotnet build /p:Configuration=Linux-Release
}

check() {
	cd "$srcdir/$_gitname"
#	make -k check
}

package() {
	cd "$srcdir/$_gitname"
	#make directories
	mkdir -p "${pkgdir}/opt/sidekick/"

	#install libraries
	cp -r "${srcdir}/${_gitname}/src/" "${pkgdir}/opt/sidekick/"
	#install script
	install -Dm 755 "${srcdir}/sidekick-start.sh" "${pkgdir}/usr/bin/sidekick"

	#install desktop
	install -Dm 644 "${srcdir}/Sidekick.desktop" "${pkgdir}/usr/share/applications/${_gitname}.desktop"
	#install licenses
	install -Dm 644 "${srcdir}/${_gitname}/LICENSE" "${pkgdir}/usr/share/licenses/${_gitname}/LICENSE"
}
