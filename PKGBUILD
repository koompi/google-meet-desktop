# Maintainer: Pichponereay NGOR <isaacjacksonreay at gmail dot com>

pkgname=google-meet-desktop
pkgver=2.0.0
pkgrel=1
pkgdesc="Google Meets desktop built with electron"
arch=("any")
license=("MIT")
url='https://meet.google.com'
depends=("nodejs" "npm" "unzip")
source=(
  "${pkgname}.png"
  "${pkgname}.desktop"
)
sha256sums=(
  "8fad9e94012e93e8f1a1ea70aa5a47a23135687a2341c99451ed27d2306c7a9f"
  "281c5d311e4b8bd67bf1bc576c93a5e22274f2c8e5392d2219e2958660954318"
)

build() {
  cd "${srcdir}"
  npm i -g nativefier

  nativefier \
    --name "Google Meet" \
    --icon "${pkgname}.png" \
    --user-agent 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4464.5 Safari/537.36' \
    --verbose \
    --internal-urls "(.*?meet\.google\.com.*?|.*?accounts\.google\.com.*?)" \
    --single-instance \
    "${url}"
}



package() {

  # install main file
  install -d -m755 "${pkgdir}"/opt
  cp -Rr "${srcdir}"/GoogleMeet* "${pkgdir}"/opt/GoogleMeet

  chmod +x "${pkgdir}"/opt/GoogleMeet/GoogleMeet

  # intall desktop Entry
  install -D -m644 "${pkgname}".desktop "${pkgdir}"/usr/share/applications/"${pkgname}".desktop

  # install icon
  install -D -m755 "${srcdir}"/"${pkgname}.png" "${pkgdir}"/usr/share/icons/GoogleMeet/"${pkgname}.png"    # link the binary
  
  install -d -m755 "${pkgdir}/usr/bin"
  ln -sr "${pkgdir}/opt/GoogleMeet/GoogleMeet" "${pkgdir}/usr/bin/${pkgname}"
}
