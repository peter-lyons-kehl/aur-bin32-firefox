# Maintainer: aus <austin@theaus.xyz>
# Contributor: Felix Golatofski <contact@xdfr.de>
# Contributor: Swift Geek
# Contributor: c0nd0r <gcesarmza@gmail.com>
# Contributor: Thomas Dziedzic < gostrc at gmail >
# Contributor: webjdm <web.jdm@gmail.com>
# Contributor: magedon <magedon.zt@gmail.com>
# Contributor: Ali Akbar

pkgname=bin32-firefox-bin
pkgver=130.0
pkgrel=1
pkgdesc="Standalone web browser from mozilla.org - 32bit version for 64bit systems"
arch=('x86_64')
_arch=i686
license=('MPL' 'GPL' 'LGPL')
provides=('bin32-firefox')
conflicts=('bin32-firefox')
url="https://www.mozilla.org/en-US/firefox/"
depends=('bash' 'lib32-alsa-lib' 'lib32-at-spi2-core' 'lib32-cairo' 'lib32-dbus' 'lib32-fontconfig' 'lib32-freetype2'
	'lib32-gcc-libs' 'lib32-gdk-pixbuf2' 'lib32-glib2' 'lib32-glibc' 'lib32-gtk3' 'lib32-libx11' 'lib32-libxcb'
	'lib32-libxcomposite' 'lib32-libxcursor' 'lib32-libxdamage' 'lib32-libxext' 'lib32-libxfixes' 'lib32-libxi'
	'lib32-libxrandr' 'lib32-libxrender' 'lib32-nspr' 'lib32-nss' 'lib32-pango')
optdepends=('lib32-librsvg: svg_loader.so library'
            'lib32-ffmpeg: extra codec support (x264)')
source=(https://download-installer.cdn.mozilla.net/pub/firefox/releases/$pkgver/linux-$_arch/en-US/firefox-$pkgver.tar.bz2
        'firefox32.desktop')
sha256sums=('fca72dcd3748bea7bbeff81d9241c7d566159c91e36b1789c6b465670a1151ed'
            '8477bb0a22be7fc39fcad1daad444862fac359b74662b447954811fdae1a5bf2')
validpgpkeys=('14F26682D0916CDD81E37B6D61B7B526D98F0353') # Mozilla Software Releases <release@mozilla.com>

package() {
  # directory and files
  cd ${pkgdir}
  mkdir -p {usr/bin,usr/lib32}
  cp -r ${srcdir}/firefox usr/lib32/${pkgname}
  mv usr/lib32/${pkgname}/firefox usr/lib32/${pkgname}/firefox32
  mv usr/lib32/${pkgname}/firefox-bin usr/lib32//${pkgname}/firefox32-bin
  cat <<EOF > usr/bin/bin32-firefox
#!/bin/bash
MOZ_PLUGIN_PATH="/opt/mozilla/lib/plugins:/usr/lib32/mozilla/plugins" /usr/lib32/${pkgname}/firefox32 \$*
EOF
  chmod +x usr/bin/bin32-firefox

  # desktop icons
  cd ${srcdir}
  install -d ${pkgdir}/usr/share/applications
  install -Dm644 firefox32.desktop ${pkgdir}/usr/share/applications
  install -Dm644 firefox/browser/chrome/icons/default/default128.png ${pkgdir}/usr/share/pixmaps/firefox32.png
}
