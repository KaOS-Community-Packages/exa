pkgname=exa
pkgver=0.9.0
pkgrel=1
arch=('x86_64')
pkgdesc='A modern version of ls'
url='https://the.exa.website'
license=('custom:MIT')
depends=('libssh2' 'zlib')
makedepends=('make' 'rust' 'git')
source=("git+https://github.com/ogham/exa.git#tag=v${pkgver}")
sha1sums=('SKIP')

build() {
  make -C "${srcdir}/${pkgname}"
}

package() {
  cd "${srcdir}/${pkgname}"
  mkdir -p "${pkgdir}/usr/bin"
  make PREFIX="${pkgdir}/usr" install
  install -Dm644 contrib/completions.bash \
    "${pkgdir}/etc/bash_completion.d/$pkgname"
  install -Dm644 contrib/completions.zsh \
    "${pkgdir}/usr/share/zsh/site-functions/_$pkgname"
  install -Dm644 contrib/completions.fish \
    "${pkgdir}/usr/share/fish/vendor_completions.d/$pkgname.fish"
  install -Dm644 LICEN?E \
    "${pkgdir}/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 "${srcdir}/${pkgname}/contrib/man/${pkgname}.1" \
    "${pkgdir}/usr/share/man/man1/${pkgname}.1"
}
