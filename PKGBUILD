# $Id$
# Maintainer: Daniel Micay <danielmicay@gmail.com>

pkgname=('termite-git-with-nN-cursor-move-patch')
pkgver=v15.r5.g9565563
pkgrel=1
pkgdesc="A simple VTE-based terminal"
arch=('x86_64')
url="https://github.com/thestinger/termite/"
license=('LGPL')
depends=('vte3-ng-with-nN-cursor-move-patch' 'ncurses') # ncurses now comes with the terminfo file
makedepends=('git' 'vte3-ng-with-nN-cursor-move-patch' 'ncurses')
conflicts=(termite)
provides=(termite)
source=("git+https://github.com/thestinger/termite.git"
        "0001-Move-cursor-along-with-next-prev-search-match-select.patch"
        "0002-Change-TERM-to-termite-instead-of-xterm-termite.patch"
        "682.1.patch"
        "682.2.patch")
sha256sums=('SKIP'
            'f3fea6df7829de9c606f7209a7a68108de9fab6995badc9c2e367de2e0359bf6'
            '066f0dcd27abfeb7a5af6dc1b37a7a66e5fc4389ddcdeb2316c37f9e3f72af39'
            '4c39323f7aaf1cf0801154265aadce271d2f5c744d3dfefb50da63e36f3f1aab'
            'f690906d5d42196df276ca567f7d76d4c452b2629b701ba8bdbe06a49f62b145')

pkgver() {
  cd termite
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd termite

  patch -p1 -i ${srcdir}/0001-Move-cursor-along-with-next-prev-search-match-select.patch
  patch -p1 -i ${srcdir}/0002-Change-TERM-to-termite-instead-of-xterm-termite.patch
  patch -p1 -i ${srcdir}/682.1.patch
  patch -p1 -i ${srcdir}/682.2.patch
}

build() {
  cd termite
  git submodule update --init
  make
}

package() {
  backup=(etc/xdg/termite/config)

  cd termite
  make PREFIX=/usr DESTDIR="$pkgdir" install
}
