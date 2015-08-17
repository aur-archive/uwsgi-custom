pkgname=('uwsgi-custom')
_pkgbase=uwsgi
pkgver=1.9.14
pkgrel=1
epoch=
pkgdesc="uWSGI with splitted plugins python2,gevent,rack,php,cgi,fiber. This is a custom package. It uses the latest stable uwsgi."
arch=(i686 x86_64 arm armv6h)
url="http://projects.unbit.it/uwsgi/"
license=('GPL2')
groups=()
depends=(libyaml jansson python2 php-embed ruby-rack python)
makedepends=(python python2)
checkdepends=()
provides=()
conflicts=(uwsgi uwsgi-core uwsgi-cgi uwsgi-php uwsgi-rack uwsgi-python2)
replaces=()
backup=()
options=()
install=
changelog=
source=(http://projects.unbit.it/downloads/$_pkgbase-$pkgver.tar.gz)
noextract=()
md5sums=('ec9cf333534604f17ef4e24051d9d65d')


build() {
  cd "$srcdir/$_pkgbase-$pkgver"
  python uwsgiconfig.py --build package
  python2 uwsgiconfig.py --plugin plugins/python core python27
  python uwsgiconfig.py --plugin plugins/python core python
  python uwsgiconfig.py --plugin plugins/gevent core gevent
  python uwsgiconfig.py --plugin plugins/php core php
  python uwsgiconfig.py --plugin plugins/rack core rack
  python uwsgiconfig.py --plugin plugins/fiber core fiber  
  python uwsgiconfig.py --plugin plugins/cgi core cgi

}

package() {
  cd "$srcdir/$_pkgbase-$pkgver"
  mkdir -p "$pkgdir/usr/bin"
  install -Dm755 uwsgi "$pkgdir/usr/bin/uwsgi"

  mkdir -p "$pkgdir/usr/lib/uwsgi/"
  install -Dm555 python27_plugin.so "$pkgdir/usr/lib/uwsgi"
  install -Dm555 python_plugin.so "$pkgdir/usr/lib/uwsgi"
  install -Dm555 gevent_plugin.so "$pkgdir/usr/lib/uwsgi"
  install -Dm555 php_plugin.so "$pkgdir/usr/lib/uwsgi"
  install -Dm555 rack_plugin.so "$pkgdir/usr/lib/uwsgi"
  install -Dm555 fiber_plugin.so "$pkgdir/usr/lib/uwsgi"
  install -Dm555 cgi_plugin.so "$pkgdir/usr/lib/uwsgi"

  ln -s "/usr/bin/uwsgi" "$pkgdir/usr/bin/uwsgi_php"
  ln -s "/usr/bin/uwsgi" "$pkgdir/usr/bin/uwsgi_rack"
  ln -s "/usr/bin/uwsgi" "$pkgdir/usr/bin/uwsgi_cgi"
  ln -s "/usr/bin/uwsgi" "$pkgdir/usr/bin/uwsgi_python27"
  ln -s "/usr/bin/uwsgi" "$pkgdir/usr/bin/uwsgi_python"
}

