# Maintainer: Jim Pryor <profjim@jimpryor.net>
# Warning: The chicken-* egg PKGBUILDS in AUR are auto-generated.
#          Please report errors you notice so that I can tweak the generation script.

pkgname=chicken-elliptic-curves
pkgver=1.0.1
pkgrel=4
pkgdesc="Chicken Scheme Egg: Arithmetic and Cryptography on Elliptic Curve Groups over Finite Fields"
arch=('i686' 'x86_64')
url="http://chicken.wiki.br/eggref/4/elliptic-curves"
license=('BSD')
depends=('chicken>=4.5.0' 'chicken-numbers' 'chicken-modular-arithmetic' 'chicken-defstruct' 'chicken-matchable' )
options=(docs !libtool !emptydirs)
install="chicken.install"
source=("$pkgname-$pkgver.chunked::http://chicken.kitten-technologies.co.uk/henrietta.cgi?name=elliptic-curves&version=$pkgver"
		"$pkgname-$pkgver.html::http://chicken.wiki.br/eggref/4/elliptic-curves.html")
md5sums=('486d0e3ec32c5a071ca20b97cfbdf5ba' '80ba798c65ea1ab78ecc4594f6bf0e65')

build() {
	# unchunk the blob that was downloaded from henrietta
	cd "$srcdir"
	mkdir -p "elliptic-curves-$pkgver"
	cat "$pkgname-$pkgver.chunked" | while :; do
		while read -r bar ver endbar fname len; do
			[[ -n "$ver" ]] && break
		done
		[[ "$endbar" = "|#" ]] || fname="$ver" len="$endbar"
		[[ -z "$fname" ]] && break
		fname="${fname:1:${#fname}-2}" # delete quotes around fname
		if [[ "${fname: -1}" == / ]]; then
			mkdir -p "elliptic-curves-$pkgver/$fname"
		elif [[ "$len" -eq 0 ]]; then
			touch "elliptic-curves-$pkgver/$fname"
		else
			dd iflag=fullblock of="elliptic-curves-$pkgver/$fname" ibs="$len" count=1 2>/dev/null
		fi
	done
	

	cd "$srcdir/elliptic-curves-$pkgver"
	cp ../$pkgname-$pkgver.html elliptic-curves.html
	
	
	mkdir -p "$pkgdir/usr/lib/chicken/5" "$pkgdir/usr/share/chicken/elliptic-curves"
		
	chicken-install -p "$pkgdir/usr"
	
		install -Dm644 "elliptic-curves.html" "$pkgdir/usr/share/doc/$pkgname/elliptic-curves.html"
}
