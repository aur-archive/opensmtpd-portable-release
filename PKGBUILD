# Maintainer: Ariel Popper a \at/ arielp \dot/ com

_pkgbase="opensmtpd"

pkgname="opensmtpd-portable-release"
pkgver="5.3p1"
pkgrel="2"
pkgdesc="FREE implementation of the server-side SMTP protocol."
arch=('i686' 'x86_64')
url="http://www.opensmtpd.org/portable.html"
license=('BSD')
depends=('libevent')
conflicts=('smtp-server' 'smtp-forwarder')
provides=('smtp-server' 'smtp-forwarder')
backup=("etc/$_pkgbase/smtpd.conf")
install="$_pkgbase.install"
source=("http://www.opensmtpd.org/archives/$_pkgbase-$pkgver.tar.gz"
		"$_pkgbase.service"
		"$_pkgbase.conf.linux")
md5sums=('e98dfbfa17be1ff8f1e091319dfca4d8'
         'e5d13d921f84cc40862ac416396a232b'
         '5f1a1d446bf94b7a42361f48796b5773')

build () {
	cd "$srcdir/$_pkgbase-$pkgver"
	./bootstrap
	./configure --prefix=/usr --sysconfdir="/etc/$_pkgbase" --with-pam
	make
}

package () {
	cd "$srcdir/$_pkgbase-$pkgver"
	make DESTDIR="$pkgdir" install
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
	ln -s smtpctl "$pkgdir/usr/sbin/sendmail"

	cd "$srcdir"
	install -Dm644 "$_pkgbase.service" \
		"$pkgdir/usr/lib/systemd/system/$_pkgbase.service"
	install -Dm644 "$_pkgbase.conf.linux" "$pkgdir/etc/$_pkgbase/smtpd.conf"
}

