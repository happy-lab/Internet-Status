#
# This is the PKGBUILD for Internet Status Publish Through MQTT.
#

pkgname=internet-status
pkgver=1.1.1
pkgrel=1
pkgdesc="Internet Status Publish Through MQTT"
arch=('i686' 'x86_64' 'arm' 'armv6h' 'armv7h')
url="http://happy-lab.llc/"
depends=('python')
provides=('internet-status')
license=('MIT')
source=("LICENSE"
        "internet-statusd"
        "internet-status.service"
        "internet-status"
        "internet-status_pi"
        "internet-status_pi.service"
        "monitor.conf.example")
install=internet-status.install
sha256sums=('86efd6ff86cea002a35a41101f8e56966f30889bfc8b5a210707de9ec8d4945f'
            '9360be2266943921e8710a43e5c8612c2bbe78322731a6052825e0e373bd3cd5'
            '8c2d472cc2b1fd18bf7b925d62ad2a6b5713f49bcd7f85ae327bd37d6152a629'
            'fa5fa8d2985f71f974418c781203646d0d95b792336a5938b7ffaf4ae80c7052'
            '71e768af6ad0084e8b7dc574f6198cd1543875b94ecbe8cc8ee81d510118fc28'
            'adb2e82daded7e12c8d64e0aa720cd76883c92b2a55814cf1b48252610c0f00a'
            '379b6ca33a061c78c5af046ab855eb62e1f22cbc5d8598682d88cc6e293b18e1')

package() {

  # Daemons
  install -Dm755 "internet-statusd" "$pkgdir/usr/bin/internet-statusd"
  install -Dm755 "internet-status" "$pkgdir/usr/bin/internet-status"
  install -Dm755 "internet-status_pi" "$pkgdir/usr/bin/internet-status_pi"

  # Daemon systemd service file
  install -Dm644 "internet-status.service" "$pkgdir/usr/lib/systemd/system/internet-status.service"
  install -Dm644 "internet-status_pi.service" "$pkgdir/usr/lib/systemd/system/internet-status_pi.service"

  # Daemon configuration file
  install -Dm644 "monitor.conf.example" "$pkgdir/etc/$pkgname/monitor.conf.example"

  # Daemon PID file
  #echo 'pid_file /run/$pkgname.pid' >> "$pkgdir/etc/sensors/$pkgname.conf.example"

  # License
  install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

}

