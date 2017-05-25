pkgname=yubikey-hotplug
pkgver=1
pkgrel=1
pkgdesc="udev hotplug event for Yubikey devices"
arch=('any')
url="https://github.com/fuhry/yubikey-hotplug"
license=('MIT')
depends=('bash' 'yubikey-manager')
source=('yubikey-hotplug' '95-yubikey-hotplug.rules')
install='yubikey-hotplug.install'
sha256sums=('b4b351492b0ed2acea010d3103624f82349d7752f7bfbf6ccac246b931bc5c8c'
            '0b314b6da0b6674a5440c80112a00f0edce2713d8e104b35966a0e67336e03d7')

package() {
  install -d -m0755 "${pkgdir}/etc/udev/rules.d"
  install -m0644 "${srcdir}/95-yubikey-hotplug.rules" "${pkgdir}/etc/udev/rules.d/"
  install -d -m0755 "${pkgdir}/usr/bin"
  install -m0755 "${srcdir}/yubikey-hotplug" "${pkgdir}/usr/bin/"
}
