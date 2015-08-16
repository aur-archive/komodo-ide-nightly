# Maintainer: Robbo <robbo.clancy at gmail dot com>
# Forked from https://aur.archlinux.org/packages/komodo-ide

pkgname=komodo-ide-nightly
pkgver=9.0.0_rc1_87167
pkgrel=1
pkgdesc="ActiveState Komodo IDE 9.0 Nightly"
arch=('i686' 'x86_64')
url="http://komodoide.com"
license=('MPL')
depends=('glibc>=2.4' 'libjpeg>=6.2' 'gcc-libs' 'gtk2')
[ "$CARCH" = "i686" ] && _arch="x86" && sha1sums=('63bb708b730195a7908926430e822f908898def8')
[ "$CARCH" = "x86_64" ] && _arch="x86_64" && sha1sums=('d4c6be25edd2591525a8e97850882f20986c7847')
source=("http://downloads.activestate.com/Komodo/nightly/komodoide/latest-master/link/Komodo-IDE-linux-${_arch}.tar.gz")
options=(!strip)

package() {
  cd "${srcdir}/Komodo-IDE-${pkgver//_/-}-linux-${_arch}"
  ./install.sh -s -I "${pkgdir}/opt/${pkgname}" --dest-dir "/opt/${pkgname}"
  install -d "${pkgdir}"/usr/{bin,share/applications}
  ln -s "/opt/${pkgname}/share/desktop/komodo-ide-9.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  ln -sf "/opt/${pkgname}/lib/mozilla/komodo" "${pkgdir}/opt/${pkgname}/bin/komodo"
  ln -s "/opt/${pkgname}/lib/mozilla/komodo" "${pkgdir}/usr/bin/${pkgname}"
  grep -r -lZ "$pkgdir" "$pkgdir" 2>/dev/null | while read -rd '' file; do sed -i "s|$pkgdir||g" "$file"; done
}

post_install() {
	cat << EOF
*** Komodoe IDE License ***
==> Please place the license file named as ActiveState.lic into ${HOME}/.ActiveState/
==> or use the provided license file script to install it.
EOF
}
