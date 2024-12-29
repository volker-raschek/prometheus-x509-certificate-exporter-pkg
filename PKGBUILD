# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=prometheus-x509-certificate-exporter
_pkgname=x509-certificate-exporter
pkgver=3.17.0 # renovate: datasource=github-releases depName=enix/x509-certificate-exporter
pkgrel=1
pkgdesc="metric exporter for x509 certificates"
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/enix/$_pkgname"
license=('MIT')
makedepends=('go')
backup=(
  etc/conf.d/prometheus-x509-certificate-exporter
)

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
  'prometheus-x509-certificate-exporter'
  'systemd.service'
)
sha512sums=('d2a696ec8ac3c06316be033c55a8d888b878317b05496bf3eee94634f8b3d029a33568c9d028033c0c629e82ce5cf5dcc2ace467e5416debf46d2bfbe24c3fe3'
            '2fd59748f9cb4018456befcc07bb1e4a68cbe5d5bf30faa74e4bc607c241623ee66d6ea7765a5bcd707dfa2a1eb674b7e2e766e27fc0c462c0db1b5ec6aa13ac'
            'a95d01a84340bdcfbc833f5b78976432bdca1c567f55a3c56eb2ef3b95a64488d38482ddb965d535b6a8f66ea4b34f51a2bf0bd8098f7d3af81ff4fd63ec3b5a')
b2sums=('efcd30d91f0eb95963cf4d48e8bfb6cb42f08046747ef7a412ce6ba87c8b7d2812b470903972942461156ef8f740542de0db99bcbcf58bacb838023a6cdbe0d3'
        '41d9f7daeeedddc11056ac3b8e741afbab80c5779ce3823aa2d88f179e779c0715ccf8c471d645ef74df87f0f7c33cbec92a0ecdae148bd80f83670b6446038c'
        'c7bfafa8f30cbde623909875c6bce8784261bb3bf38a4c3cb6b36745866558df4d1cf2e7d95c12ac47622863f1e91cce7febb01a5499c51a024019026c165033')

build() {
  cd "$_pkgname-$pkgver/cmd/$_pkgname"
  go build -v \
    -buildmode=pie \
    -trimpath \
    -o $pkgname .
}

package() {
  # systemd integration
  install -D --mode 0644 systemd.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"

  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$_pkgname-$pkgver/cmd/$_pkgname/$pkgname"

  # extra args
  # NOTE: Set restrict file permissions by default to protect optional basic auth credentials
  install -D --mode 0600 --target-directory "$pkgdir/etc/conf.d" prometheus-x509-certificate-exporter

  # license
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$_pkgname-$pkgver/LICENSE"
}
