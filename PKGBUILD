# $Id$
# Maintainer: spigell <spigelly@gmail.com>

pkgname=dwm-spigell
pkgver=6.2
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
provides=(dwm)
conflicts=(dwm)
license=('MIT')
options=(zipman)
optdepends=('lightdm: lightdb-support (switch-to-greeter)'
            'light-locker: locker-support (--lock)'
           )
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
        https://dwm.suckless.org/patches/systray/dwm-systray-6.2.diff
        https://dwm.suckless.org/patches/pertag/dwm-pertag-6.2.diff
        statusallmons-patch-compatible-with-systray.patch
	config.h
	dwm.desktop)
sha256sums=('97902e2e007aaeaa3c6e3bed1f81785b817b7413947f1db1d3b62b8da4cd110e'
            'd60e6b4533e9079e6bc57bde9e25d6ac0b620122098ff5d34f806fecf8d1a7a6'
            '055da0f12dbfde9e50df54e1f2d87966466404a36c056efb94bb21ab03b94b10'
            'bcae437c3c5d8d67bdf555ea69cd66c4855a815c27d2e192d5b65b3f034905c1'
            '1d61f12fa72a46074c43a13ebd8d8731b4177c884789c90fc1024ec9918b8cd5'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81')

prepare() {
  mv dwm-$pkgver $pkgname-$pkgver
  cd "$srcdir/$pkgname-$pkgver"
  cp "$srcdir/config.h" config.h
  patch -p1 < "$srcdir/dwm-systray-6.2.diff"
  patch -p1 < "$srcdir/dwm-pertag-6.2.diff"
  patch -p1 < "$srcdir/statusallmons-patch-compatible-with-systray.patch"
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
