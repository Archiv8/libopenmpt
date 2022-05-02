# Maintainer: Andrew Lin <andrewlin16 at gmail dot com>
# Contributor: Simon Thorpe <simon at hivetechnology dot com dot au>
pkgname=openmpt
pkgver=1.30.04.00
pkgrel=1
pkgdesc="Open-source audio module tracker"
arch=('i686' 'x86_64')
url="https://openmpt.org/"
license=('BSD')
depends=('wine')
makedepends=('gendesk' 'imagemagick' 'unzip')
optdepends=(
  'bash-completion: tab completion support'
  'ccache: for Wine native host support'
)
source=(
  'openmpt'
  'openmpt-bash-completion'
  'x-mptm.xml'
)
source_i686=("$pkgname-$pkgver.zip::https://download.openmpt.org/archive/openmpt/$(echo $pkgver | grep -Po '^\d+.\d+')/OpenMPT-$pkgver-portable-x86.zip")
source_x86_64=("$pkgname-$pkgver.zip::https://download.openmpt.org/archive/openmpt/$(echo $pkgver | grep -Po '^\d+.\d+')/OpenMPT-$pkgver-portable-amd64.zip")
noextract=("$pkgname-$pkgver.zip")
sha512sums=('7247f304a9cd00c3d60de1286336ae44cf47c10951901c3099baa7afa75898ba3d901bb282ca89599fa8346ebbae9cc0a309d3f69fdb53ec565374854cdef210'
            '7d698b7f16f20c0d4eacfc92b3284a2fb90a94ed35a53b1ed5569fb0a4c80ba33e79985056cd8be3a189931daec79b88b26fdf008802b82c63864f02cd84fe03'
            'd9ff9df37721ea66b6cc56209936efcece972cff3c84f0272f5c3a1a924743c8fb9d40d1824e4bb247909e2f214390b3310a1796f8bd15d916800fb7d26b9eb1')
sha512sums_i686=('c04726f2bb923ad4d9af7f597931357164b949d848683d77f8ed5040de367bdd06dadbc32d7d6a5633d50a04e5ae568474ab5fae806c67a896f8b385b348b06f')
sha512sums_x86_64=('c04726f2bb923ad4d9af7f597931357164b949d848683d77f8ed5040de367bdd06dadbc32d7d6a5633d50a04e5ae568474ab5fae806c67a896f8b385b348b06f')


prepare() {
  cd "$srcdir"
  mkdir -p "$pkgname-$pkgver"
  unzip -o -d "$pkgname-$pkgver" "$pkgname-$pkgver.zip"

  convert "$pkgname-$pkgver/OpenMPT File Icon.ico" "icon.png"
  gendesk -n -f --pkgname "$pkgname" --pkgdesc "$pkgdesc" \
    --name='OpenMPT' \
    --mimetype='audio/x-mod;audio/x-s3m;audio/x-xm;audio/x-it;audio/x-mptm' \
    --categories 'Audio;Sequencer;Midi;AudioVideoEditing;Music;AudioVideo;'
}

package() {
  mkdir -p "$pkgdir/usr/share"
  cp -r "$srcdir/$pkgname-$pkgver" "$pkgdir/usr/share/openmpt"
  # Since OpenMPT 1.29, portable installations are identified by the presence of the "OpenMPT.portable" file.
  # That file is removed here to keep existing installations configured properly.
  rm "$pkgdir/usr/share/openmpt/OpenMPT.portable"
  install -Dm755 "$srcdir/openmpt" "$pkgdir/usr/bin/openmpt"
  install -Dm644 "$srcdir/icon-2.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"
  install -Dm644 "$srcdir/$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"
  install -Dm644 "$srcdir/x-mptm.xml" "$pkgdir/usr/share/mime/application/x-mptm.xml"
  install -Dm644 "$srcdir/openmpt-bash-completion" "$pkgdir/usr/share/bash-completion/completions/openmpt"
}

# vim:set ts=2 sts=2 sw=2 et:
