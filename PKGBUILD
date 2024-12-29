# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=prometheus-x509-certificate-exporter
_pkgname=x509-certificate-exporter
pkgver=3.18.0 # renovate: datasource=github-releases depName=enix/x509-certificate-exporter
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
sha512sums=('669fe0b35cb58b701f6f5bf0adee801a61bfde2fc02397efecfed6c4bec029a82a60f5c557972019f823a2b364788341fdf5499a6558950fc2706e5c7e956382'
            '2fd59748f9cb4018456befcc07bb1e4a68cbe5d5bf30faa74e4bc607c241623ee66d6ea7765a5bcd707dfa2a1eb674b7e2e766e27fc0c462c0db1b5ec6aa13ac'
            'a95d01a84340bdcfbc833f5b78976432bdca1c567f55a3c56eb2ef3b95a64488d38482ddb965d535b6a8f66ea4b34f51a2bf0bd8098f7d3af81ff4fd63ec3b5a')
b2sums=('5866747b28aec780f5b399ac9f1b0bbd4f5c852ead316c89fe37bd316ebe36f169419d7e625d8c0e716e562e1c4f3c9e01a0dae138aef9c6d4e81510f43e363c'
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
