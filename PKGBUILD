pkgname=switchhosts-bin
pkgver=3.5.8
pkgrel=5556
pkgdesc="Switch hosts quickly!"
arch=('any')
url="https://oldj.github.io/SwitchHosts"
license=("MIT")
options=(!strip)
depends=("gconf" "gtk2" "libnotify" "libxtst" "nss" "python2" "xdg-utils" "desktop-file-utils" "alsa-lib")
makedepends=("imagemagick" "npm")

source=(
    "https://github.com/oldj/SwitchHosts/releases/download/v${pkgver}/SwitchHosts._linux_x64_${pkgver}.${pkgrel}.zip"
    "https://github.com/oldj/SwitchHosts/raw/master/assets/app.png"
    "${pkgname}.install"
    "${pkgname}.desktop"
)

md5sums=('2af4d0bdb4ce9800d12fffd8bf6226b3'
         '07a3df33379137283501b39e3e8581b2'
         '0b6211b511da48346cecdc1d2f963c76'
         'c6594fabba5e7f9d5ae0736524f6f634')

package() {
    install -dm755 "$pkgdir/"{opt,usr/bin}
    cp -r "${srcdir}" "${pkgdir}/opt/${pkgname}"
    ln -s "/opt/${pkgname}/switchhosts" "$pkgdir/usr/bin/switchhosts"
    install -Dm644 ${srcdir}/${pkgname}.desktop "$pkgdir"/usr/share/applications/${pkgname}.desktop
    # icons generation
    mkdir -p "icons"
    cd "icons"
    mv ${srcdir}/app.png logo_icon.png
    convert -background transparent logo_icon.png -define icon:auto-resize=16,32,48,64,128,256 app.ico
    convert app.ico logo_icon.png
    # icons installation
    sizes=(16 32 48 64 128 256)
    for i in 0 1 2 3 4 ; do
      install -d "${pkgdir}/usr/share/icons/hicolor/${sizes[$i]}x${sizes[$i]}/apps"
      install -Dm644 "logo_icon-${i}.png" \
      "${pkgdir}/usr/share/icons/hicolor/${sizes[$i]}x${sizes[$i]}/apps/${pkgname}.png"
    done
}
