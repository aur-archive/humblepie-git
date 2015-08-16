# Maintainer: Josh McGee <j.s.mcgee115@gmail.com>
pkgname=humblepie-git
pkgver=20120621
pkgrel=2
pkgdesc="humblepie downloads files from the Humble Indie Bundle Releases"
arch=('any')
url="http://github.com/zendeavor/humblepie"
license=('MIT')
depends=('links')
makedepends=('git')
provides=('humblepie')
install=$pkgname.install
options=('!strip')

_gitroot=https://github.com/zendeavor/humblepie.git
_gitname=humblepie

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
} 

package() {
  cd "${srcdir}/$_gitname-build"
  _supp="supplementary"
  install -Dm644 "${_supp}/humblepie.rc" "${pkgdir}/usr/share/humblepie/humblepie.rc"
  install -Dm644 "README.md" "${pkgdir}/usr/share/humblepie/README.md"
  install -Dm755 "humblepie" "${pkgdir}/usr/bin/humblepie"
  find "$srcdir" -type f -name $install -exec rm -f {} +
}

# vim:set ts=2 sw=2 et:
