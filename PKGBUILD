# Maintainer: Daniel Micay <danielmicay@gmail.com>
# Contributor: ryooichi <ryooichi+arch AT gmail DOT com>

pkgname=metasploit-svn
pkgver=16518
pkgrel=1
pkgdesc="A development platform for creating security tools and exploits."
arch=('any')
url='http://metasploit.com/'
license=('BSD')
depends=('ruby' 'ruby-msgpack')
makedepends=('subversion')
provides=('metasploit')
conflicts=('metasploit')
options=('!strip')
optdepends=('java-runtime: msfgui' 'ruby-pg: database support')

_svntrunk=https://www.metasploit.com/svn/framework3/trunk
_svnmod=metasploit

build() {
  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d $_svnmod/.svn ]]; then
    cd $_svnmod && svn up -r $pkgver
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"  
}

package() {
  cd "$pkgdir"
  mkdir -p usr/{bin,src}

  svn export $srcdir/$_svnmod usr/src/$_svnmod
  rm usr/src/$_svnmod/msfupdate

  install -Dm644 usr/src/$_svnmod/COPYING usr/share/licenses/$pkgname/COPYING

  cd usr/bin

  for f in ../src/metasploit/msf*; do
    ln -s $f .
  done
}
