# Maintainer: Ramiro Rivera <ramarivera@gmail.com>
#
# Packages the official Screenpipe desktop .deb. The app looks for its bundled
# bun next to its own executable, and Arch's extra/bun owns /usr/bin/bun, so the
# deb's usr/ tree lives under /opt/screenpipe-desktop with a /usr/bin symlink.
# Updates come from pacman; the in-app updater only knows how to replace
# AppImages.

pkgname=screenpipe-desktop-bin
_pkgname=screenpipe
pkgver=2.7.130
pkgrel=1
pkgdesc="Screenpipe desktop app: local 24/7 screen and audio memory for AI agents (official binary)"
arch=('x86_64')
url="https://screenpi.pe"
license=('LicenseRef-Screenpipe-Commercial')
depends=(
  'cairo'
  'dbus'
  'ffmpeg'
  'gcc-libs'
  'gdk-pixbuf2'
  'glib2'
  'glibc'
  'gtk3'
  'hicolor-icon-theme'
  'libayatana-appindicator'
  'libpipewire'
  'libpulse'
  'libsoup3'
  'libxcb'
  'mesa'
  'openblas'
  'openssl'
  'tesseract'
  'tesseract-data-eng'
  'wayland'
  'webkit2gtk-4.1'
  'xz'
)
provides=('screenpipe-desktop')
conflicts=('screenpipe-desktop')
options=('!strip' '!debug')
source=(
  "${_pkgname}-${pkgver}.deb::https://screenpi.pe/api/app-update/download/stable/${pkgver}/x86_64-unknown-linux-gnu/${_pkgname}_${pkgver}_amd64.deb"
  "LICENSE-${pkgver}.md::https://raw.githubusercontent.com/screenpipe/screenpipe/app-v${pkgver}/LICENSE.md"
)
noextract=("${_pkgname}-${pkgver}.deb")
sha256sums=('274a38989bafaedc09ab9409bd54d2028538986b5f39d7d1fc621bf272d55da3'
            '17e39cd5eb995ea4b41afc66d1e8b5ee7f4c7a67383dc24b2ddecca33230d5c7')

prepare() {
  mkdir -p deb
  bsdtar -xf "${_pkgname}-${pkgver}.deb" -C deb
  bsdtar -xf deb/data.tar.* -C deb
}

package() {
  install -d "${pkgdir}/opt/screenpipe-desktop/usr"
  cp -a deb/usr/bin deb/usr/lib "${pkgdir}/opt/screenpipe-desktop/usr/"

  install -d "${pkgdir}/usr/bin"
  ln -s /opt/screenpipe-desktop/usr/bin/screenpipe-app "${pkgdir}/usr/bin/screenpipe-app"

  install -Dm644 deb/usr/share/applications/screenpipe.desktop \
    "${pkgdir}/usr/share/applications/screenpipe.desktop"
  for size in 32x32 128x128 256x256 512x512 1024x1024; do
    install -Dm644 "deb/usr/share/icons/hicolor/${size}/apps/screenpipe-app.png" \
      "${pkgdir}/usr/share/icons/hicolor/${size}/apps/screenpipe-app.png"
  done

  install -Dm644 "LICENSE-${pkgver}.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.md"
}
