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
source=(tea-v${pkgver}.tar.gz::https://gitea.com/gitea/tea/archive/v${pkgver}.tar.gz)
sha256sums=('edcd1e9af43c91c653b19ba2f58297b4815afd285657221282321ceb2930c537')

prepare() {
  cd "${_pkgname}"

  # create directory for build output
  mkdir build

  # fix zsh completion
  sed -i "s/\$PROG/tea/" contrib/autocomplete.zsh

  # download dependencies
  export GOPATH="${srcdir}"
  go mod download
}

build() {
  cd "${_pkgname}"

  # set Go flags
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export GOPATH="${srcdir}"
  local TAGS=""

  go build -v \
    -buildmode=pie \
    -mod=readonly \
    -modcacherw \
    -ldflags "-compressdwarf=false \
    -linkmode external \
    -extldflags ${LDFLAGS} \
    -X main.Version=${pkgver} \
    -X main.Tags=${TAGS}" \
    -o build \
    .
}

package() {
  cd "${_pkgname}"

  # binary
  install -vDm755 -t "$pkgdir/usr/bin" build/tea

  # license
  install -vDm644 -t "$pkgdir/usr/share/licenses/$pkgname" LICENSE

  # completions
  install -vDm644 contrib/autocomplete.sh "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -vDm644 contrib/autocomplete.zsh "$pkgdir/usr/share/zsh/site-functions/_tea"
}
