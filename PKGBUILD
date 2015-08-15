pkgname=babel
pkgver=20130117
pkgrel=2
pkgdesc="Package manager for the Nimrod programming language."
arch=(i686 x86_64)
url="https://github.com/nimrod-code/babel"
license=("BSD")
makedepends=(nimrod git)
_gitroot="https://github.com/nimrod-code/babel.git"
_gitname="babel"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  nimrod c -d:release babel.nim
}

package() {
  cd "$srcdir/$_gitname-build"
  install -Dm755 "babel" "$pkgdir/usr/bin/babel"
  install -Dm644 "license.txt" "$pkgdir/usr/share/licenses/$pkgname/license.txt"
}
