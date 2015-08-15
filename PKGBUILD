# $Id: PKGBUILD 25687 2010-09-09 08:42:38Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Sebastian Faltoni <sebastian.faltoni@gmail.com>

pkgname=dbmail3
pkgver=3.0.0_rc3
pkgrel=1
pkgdesc="Fast and scalable sql based mail services"
arch=('i686' 'x86_64')
depends=('gmime' 'libzdb' 'mhash')
makedepends=('asciidoc' 'xmlto' 'docbook-xsl' 'docbook-xml' 'postgresql-libs>=8.4.1'
	     'sqlite3' 'libmysqlclient' 'libldap>=2.4.18' 'libsieve')
optdepends=('postgresql-libs: for PostgreSQL storage backend'
	    'sqlite3: for SQLite storage backend'
	    'libmysqlclient: for MySQL storage backend'
	    'libldap: for LDAP authentication'
	    'libsieve: for dbmail-sieve')
url="http://www.dbmail.org"
license=('GPL')
options=('!libtool' 'zipman')
backup=(etc/conf.d/dbmail)
conflicts=('dbmail')
provides=('dbmail')
source=(http://www.dbmail.org/download/3.0/dbmail-${pkgver/_/-}.tar.gz
	dbmail.conf.d
	dbmail.rc.d)
md5sums=('52c3b9aad310efc90a6a2fff0552f73e'
         'e7f72bc360decdb2475266391ad12329'
         '099225611da20ec194c092ac9befc33c')

build() {
  cd $srcdir/dbmail-${pkgver/_/-}/

  [ -f Makefile ] || ./configure --prefix=/usr \
	--with-mysql --with-pgsql --with-sqlite --with-ldap --with-sieve
  make
}

package() {
  cd $srcdir/dbmail-${pkgver/_/-}/
  make DESTDIR=$pkgdir install
  (cd man && make && make install DESTDIR=$pkgdir)

  mkdir $pkgdir/etc
  install -Dm644 dbmail.conf $pkgdir/etc/dbmail.conf.sample
  install -Dm644 ../dbmail.conf.d $pkgdir/etc/conf.d/dbmail
  install -Dm755 ../dbmail.rc.d $pkgdir/etc/rc.d/dbmail
  mkdir $pkgdir/usr/share/dbmail
  cp -r sql/* $pkgdir/usr/share/dbmail/
  cp dbmail.schema $pkgdir/usr/share/dbmail/
}
