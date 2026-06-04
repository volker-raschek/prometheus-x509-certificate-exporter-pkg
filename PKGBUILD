# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=prometheus-x509-certificate-exporter
_pkgname=x509-certificate-exporter
pkgver=3.19.1 # renovate: datasource=github-releases depName=enix/x509-certificate-exporter extractVersion='^v?(?<version>.*)$'
pkgrel=1
pkgdesc="metric exporter for x509 certificates"
arch=('aarch64' 'x86_64' 'riscv64')
url="https://github.com/enix/$_pkgname"
license=('MIT')
backup=(
  etc/conf.d/prometheus-x509-certificate-exporter
)

source_aarch64=(
  "${pkgname}-${pkgver}-linux-aarch64.tar.gz::https://github.com/enix/x509-certificate-exporter/releases/download/v${pkgver}/${_pkgname}-linux-arm64.tar.gz"
  'prometheus-x509-certificate-exporter'
  'systemd.service'
)

source_riscv64=(
  "${pkgname}-${pkgver}-linux-riscv64.tar.gz::https://github.com/enix/x509-certificate-exporter/releases/download/v${pkgver}/${_pkgname}-linux-riscv64.tar.gz"
  'prometheus-x509-certificate-exporter'
  'systemd.service'
)

source_x86_64=(
  "${pkgname}-${pkgver}-linux-x86_64.tar.gz::https://github.com/enix/x509-certificate-exporter/releases/download/v${pkgver}/${_pkgname}-linux-amd64.tar.gz"
  'prometheus-x509-certificate-exporter'
  'systemd.service'
)

sha256sums_aarch64=('614b127e56f8b008070f43f6ea5899e2c43264ca1fef2e363bc2bfcbc4f9260e'
                    '166c40406cf301f817b33d62529bcea00d4c93d278161b0f2e25b268d9a51083'
                    'f20db363daf15a32040781fc5b1972b178725e4d5021c47aa11dd65a862fc837')
sha256sums_x86_64=('4ccc43f593bc6aafa435771fa8622854f10a645e974d923a93072c5eba762b89'
                   '166c40406cf301f817b33d62529bcea00d4c93d278161b0f2e25b268d9a51083'
                   'f20db363daf15a32040781fc5b1972b178725e4d5021c47aa11dd65a862fc837')
sha256sums_riscv64=('d24eb885f418ffb5abb81c9aa8e42cee5e43c63043d556349ae5cb058aed2455'
                    '166c40406cf301f817b33d62529bcea00d4c93d278161b0f2e25b268d9a51083'
                    'f20db363daf15a32040781fc5b1972b178725e4d5021c47aa11dd65a862fc837')

package() {
  # systemd integration
  install -D --mode 0644 systemd.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"

  # binary
  install -D --mode 0755 "$_pkgname" "$pkgdir/usr/bin/$pkgname"

  # extra args
  # NOTE: Set restrict file permissions by default to protect optional basic auth credentials
  install -D --mode 0600 prometheus-x509-certificate-exporter "$pkgdir/etc/conf.d/prometheus-x509-certificate-exporter"
}
