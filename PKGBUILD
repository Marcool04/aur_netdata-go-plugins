# Maintainer: hexchain <i at hexchain dot org>

pkgname=netdata-go-plugins
pkgver=0.25.0
pkgrel=1
pkgdesc="netdata go.d plugin"
url="https://github.com/netdata/go.d.plugin"
license=('GPL3')
arch=('x86_64')
depends=('glibc')
makedepends=('go')
source=(
    "$pkgname-$pkgver.tar.gz::https://github.com/netdata/go.d.plugin/archive/v$pkgver.tar.gz"
    "$pkgname-$pkgver-config.tar.gz::https://github.com/netdata/go.d.plugin/releases/download/v$pkgver/config.tar.gz")

prepare() {
    mkdir -p "$srcdir/build"
    export GOPATH="$srcdir/build"
    export CGO_LDFLAGS="$LDFLAGS"
    export GOFLAGS="-buildmode=pie -trimpath -mod=vendor -modcacherw"

    cd "$srcdir/go.d.plugin-$pkgver"
    go mod vendor
}

build() {
    export GOPATH="$srcdir/build"
    export CGO_LDFLAGS="$LDFLAGS"
    export GOFLAGS="-buildmode=pie -trimpath -mod=vendor -modcacherw"

    cd "$srcdir/go.d.plugin-$pkgver"
    go build -v -o go.d.plugin ./cmd/godplugin
}

package() {
    mkdir -p "$pkgdir/usr/lib/netdata/conf.d/"
    cp -rv --no-preserve=ownership "$srcdir/go.d.conf" "$srcdir/go.d" "$pkgdir/usr/lib/netdata/conf.d/"

    install -Dm755 "$srcdir/go.d.plugin-$pkgver/go.d.plugin" -t "$pkgdir/usr/lib/netdata/plugins.d/"
}

sha256sums=('7c7ce3503e13fd2f528d508f2239ec343d9103f3b8ffa660d02fc793f332c15b'
            '23262d53fab699e4feb04f48d71ee78fd18923359f2a1d4507074c08c5935ea6')

