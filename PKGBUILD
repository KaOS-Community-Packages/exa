pkgname=exa
pkgver=0.10.1
pkgrel=1
pkgdesc='A modern version of ls'
arch=('x86_64')
url='https://the.exa.website'
license=('MIT')
depends=('git' 'zlib')
makedepends=('git' 'rust' 'pandoc')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/ogham/exa/archive/v${pkgver}.tar.gz")
sha256sums=('ff0fa0bfc4edef8bdbbb3cabe6fdbd5481a71abbbcc2159f402dea515353ae7c')

build() {
	cd "${pkgname}-${pkgver}"

	cargo build --release
	for manpage in exa.1 exa_colors.5; do
		pandoc --standalone -f markdown -t man man/$manpage.md > $manpage
	done
}

package() {
	cd "${pkgname}-${pkgver}"

	install -Dm755 "target/release/${pkgname}" -t "${pkgdir}/usr/bin"
	install -Dm644 completions/completions.bash \
		"${pkgdir}/usr/share/bash-completion/completions/${pkgname}"
	install -Dm644 completions/completions.zsh \
		"${pkgdir}/usr/share/zsh/site-functions/_${pkgname}"
	install -Dm644 completions/completions.fish \
		"${pkgdir}/usr/share/fish/vendor_completions.d/${pkgname}.fish"
	install -Dm644 LICEN?E \
		"${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	install -Dm644 exa.1 "${pkgdir}/usr/share/man/man1/exa.1"
	install -Dm644 exa_colors.5 "${pkgdir}/usr/share/man/man5/exa_colors.5"
}
