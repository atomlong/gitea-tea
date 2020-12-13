# Maintainer: John K. Luebs <jkl at johnluebs dot tld>

pkgname=gitea-tea
_pkgname=tea
pkgver=0.9.2
pkgrel=1
pkgdesc="A command line tool to interact with Gitea servers"
arch=('x86_64' 'i686' 'arm' 'armv6h' 'armv7h' 'aarch64')
url="https://gitea.io"
license=(MIT)
makedepends=(go-pie)
source=(https://gitea.com/gitea/tea/archive/v${pkgver}.tar.gz)
sha256sums=('edcd1e9af43c91c653b19ba2f58297b4815afd285657221282321ceb2930c537')

build() {
  cd ${_pkgname}
  make TEA_VERSION=v${pkgver}
}

package() {
  cd ${_pkgname}

  install -Dm755 ${_pkgname} -t "${pkgdir}"/usr/bin/
  install -Dm755 LICENSE -t "${pkgdir}"/usr/share/licenses/${pkgname}/
}
