# Maintainer: Daniel YC Lin <dlin.tw at gmail>
# vim:et sw=2 ts=2:

pkgname="fossil-fossil"
_pkgname=fossil
pkgver=20130120
pkgrel=1
pkgdesc="Simple, high-reliability, distributed software configuration management"
arch=('i686' 'x86_64')
license=('BSD')
url="http://www.fossil-scm.org"
depends=('openssl')
makedepends=('wget')
conflicts=('fossil')
provides=('fossil')
source=("fossil-xinetd" "bash.completion")

# The following two line let makepkg update pkgver automatically
_gitroot=GITURL
_gitname=MODENAME

build() {
  rm -f tip.tar.gz
  wget http://www.fossil-scm.org/index.html/tarball/tip.tar.gz
  tar xf tip.tar.gz
  cd tip
  ./configure --prefix=/usr
  # headers and translate targets are problematic with parallel jobs
  make -j1 bld bld/headers
  make
}

package() {
  cd $srcdir/tip
  install -Dm755 ${_pkgname} ${pkgdir}/usr/bin/${_pkgname}
  install -Dm644 COPYRIGHT-BSD2.txt \
          ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
  install -Dm644 $srcdir/fossil-xinetd $pkgdir/etc/xinetd.d/fossil
  install -Dm644 $srcdir/bash.completion $pkgdir/usr/share/bash-completion/completions/fossil
}
sha1sums=('a5a753e13fbc43dcd670542193a12736586d8977'
          '7e20136a383e11dcc81bd273b24ba3ea0141deb9')
