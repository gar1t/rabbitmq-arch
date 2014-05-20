# Maintainer: Stefan J. Betz <info at stefan-betz dot net>
# Contributor: p2k <Patrick dot Schneider at uni-ulm dot de>
# Contributor: Garrett Smith <g at rre dot tt>
pkgname=rabbitmq
pkgver=2.5.1
pkgrel=1
pkgdesc="Highly reliable and performant enterprise messaging implementation of AMQP written in Erlang/OTP"
arch=(i686 x86_64)
url="http://rabbitmq.com"
license=('MPL')
depends=('erlang')
backup=('etc/rabbitmq/rabbitmq-env.conf')
install=rabbitmq.install
source=("http://www.rabbitmq.com/releases/rabbitmq-server/v${pkgver}/rabbitmq-server-generic-unix-${pkgver}.tar.gz" rabbitmq-env.conf rabbitmq-server)
md5sums=('d5c0749b0e6351e0874eee3c66c3d8b3'
         '1ed22ba6a754645768a08b0c9cfddecd'
         '049a3970f79f296a317f0eacb405c007')

build(){
  cd $srcdir

  for i in usr/lib/erlang/lib usr/bin var/log/rabbitmq var/lib/rabbitmq/mnesia etc/rabbitmq; do
    mkdir -p $pkgdir/$i
  done

  install -m 640 rabbitmq-env.conf $pkgdir/etc/rabbitmq/

  cp -R ${pkgname}_server-${pkgver} $pkgdir/usr/lib/erlang/lib/

  for i in rabbitmq-server rabbitmqctl rabbitmq-env; do
    ln -sf ../lib/erlang/lib/${pkgname}_server-${pkgver}/sbin/$i $pkgdir/usr/bin/
    sed -i 's/-sname/-setcookie ${COOKIE} -sname/' $pkgdir/usr/lib/erlang/lib/rabbitmq_server-${pkgver}/sbin/$i
    chmod 755 $pkgdir/usr/lib/erlang/lib/${pkgname}_server-${pkgver}/sbin/$i
  done

  install -D rabbitmq-server "$pkgdir/etc/rc.d/rabbitmq-server"
}
