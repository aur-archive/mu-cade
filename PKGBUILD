# Maintainer: Anntoin Wilkinson <anntoin gmail com>
# Contributor: Nick B <Shirakawasuna at gmail _dot_com>

pkgname=mu-cade
pkgver=0.11
pkgrel=7
pkgdesc="A tabletop physics shoot-em-up game by Kenta Cho."
arch=('i686' 'x86_64')
url="http://www.asahi-net.or.jp/~cs8k-cyu/windows/mcd_e.html"
license=('custom')
depends=('libbulletml' 'glu' 'ode' 'sdl_mixer')
makedepends=('gdc1')
source=('http://abagames.sakura.ne.jp/windows/mcd0_11.zip'
        'http://ftp.de.debian.org/debian/pool/main/m/mu-cade/mu-cade_0.11.dfsg1-6.debian.tar.gz')
md5sums=('59915ec27f7899cdf1e417987ead4ace'
         '678f95f1ee150244f69018aef7d65e70')

prepare() {
	cd $srcdir/mcd

  _patchdir="../debian/patches/"
  cat $_patchdir/series | egrep -v '^#|^\ #' | sed "s:^:$_patchdir/:" | xargs -n1 patch -p1 -i

	sed -i 's:share\/games:share:' ./src/abagames/util/sdl/{sound,texture}.d \
                                 ./src/abagames/mcd/barrage.d
  sed -i 's:gdmd-v1:gdmd1:' Makefile
  sed -i 's:gdc-v1:gdc1:' Makefile
}

build() {
	cd $srcdir/mcd
	make
}

package() {
  cd $srcdir/mcd

  # Install binaries
  install -D -m755 $pkgname $pkgdir/usr/bin/$pkgname

  # Install other resources
  find {barrage,images,sounds} -type f -exec install -Dm644 {} $pkgdir/usr/share/$pkgname/{} \;

  # Install man page and debian copyright notice
  install -D -m644 ../debian/$pkgname.6 $pkgdir/usr/share/man/man6/$pkgname.6
  install -D -m644 ../debian/copyright $pkgdir/usr/share/licenses/$pkgname/copyright

  # Install desktop file and icon
  install -D -m644 ../debian/$pkgname.desktop $pkgdir/usr/share/applications/$pkgname.desktop
  install -D -m644 ../debian/$pkgname.xpm $pkgdir/usr/share/pixmaps/$pkgname.xpm
}

# vim:set ts=2 sw=2 et:
