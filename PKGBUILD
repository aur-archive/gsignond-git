# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Josip Ponjavic <josipponjavic@gmail.com>

pkgname=gsignond-git
pkgver=1.0.1.r18.9602d97
pkgrel=1
pkgdesc='gSSO glib daemon'
arch=('i686' 'x86_64')
url='https://01.org/gsso'
license=('LGPL2.1')
depends=('dbus' 'libgsignon-glib-git' 'sqlite')
makedepends=('git' 'gobject-introspection' 'gtk-doc')
provides=("${pkgname%-*}")
conflicts=("${pkgname%-*}")
backup=('etc/gsignond.conf')
source=("${pkgname%-*}::git+https://code.google.com/p/accounts-sso.gsignond/")
sha256sums=('SKIP')

pkgver() {
  cd ${pkgname%-*}

  printf "%s" "$(git describe --tags | sed 's/-/.r/; s/-g/./')"
}

build() {
  cd ${pkgname%-*}

  mkdir -p m4
  gtkdocize
  aclocal
  autoheader
  libtoolize --copy --force
  autoconf
  automake --add-missing --copy
  autoreconf --install --force
  ./configure --prefix='/usr' --sysconfdir='/etc' --enable-dbus-type='session' --enable-gtk-doc
  make
}

package() {
  cd ${pkgname%-*}

  make DESTDIR="${pkgdir}" install
}

# vim: ts=2 sw=2 et:
