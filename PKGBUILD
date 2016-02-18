# Maintainer:
# Contributor: Peter Pickford <arch@netremedies.ca>

pkgname=vocp
pkgver=0.9.3
pkgrel=1
pkgdesc="VOCP is a complete messaging solution for voice modems, with voicemail, fax, email pager, DTMF command shell and Text-to-Speech support, 3 GUIs and a web interface. Send and receive faxes and voicemail, listen to emails and execute programs on the host."
url="http://vocp.psychogenic.net/index.php?mode=function"
license=('GPL')
arch=('i686' 'x86_64')
depends=('mgetty-vgetty' 'perl-audio-dsp' 'perl-crypt-blowfish' 'perl-crypt-cbc' 'perl-mime-tools' 'perl-tk' 'perl-xml-mini' 'perl-modem-vgetty'  )
conflicts=('mgetty')
makedepends=('make' 'perl')
install='vocp.install'
source=('http://prdownloads.sourceforge.net/vocp/VOCP-0.9.3.tar.bz2'
'convert_sound.pl'
'install_vocp.pl'
	)
md5sums=('1a570a1f5af11786b39f6aed4304b5c3'
         'b6d69da8f3221d7d51e3be4d2c067c00'
         '3abd17fdd551aee139b8f40efd7a93a0')

build(){
  cd "$srcdir/$pkgname-$pkgver/prog/VOCP"

  # Install module in vendor directories.
  PERL_MM_USE_DEFAULT=1 perl Makefile.PL INSTALLDIRS=vendor
  make
}
check(){
  cd "$srcdir/$pkgname-$pkgver/prog/VOCP"
  #make test
}
package(){
  cd "$srcdir/$pkgname-$pkgver/"
  $srcdir/install_vocp.pl "$pkgdir/"
  cd "$srcdir/$pkgname-$pkgver/prog/VOCP"
  
  make install DESTDIR="$pkgdir/"
  # remove perllocal.pod and .packlist
  find "$pkgdir" -name .packlist -o -name perllocal.pod -delete
  install -D -m555 $srcdir/convert_sound.pl $pkgdir/usr/local/vocp/bin/convert_sound.pl
}