# PKGBUILD
# skrypt budujący i instalujący program projector za pomocą makepkg w Arch Linux  
# parviaij 2023

pkgname='projector'
pkgrel=1
pkgver=1.0.0
arch=('x86_64')
makedepends=('go' 'git')	# zależności potrzebne do budowania programu
source=('git+https://github.com/jordus100/projector')	# lokalizacja plików źródłowych programu
sha256sums=('SKIP')

# własne pomocnicze zmienne
_static_files="usr/share/proj"
_exe_files="usr/bin"
_scripts="usr/local/bin"
_service_files="usr/lib/systemd/system"
_src="$pkgname/src"

build() {
	cd "$srcdir/$_src"
	go build -o laplace -ldflags "-X main.staticDir=/$_static_files/files" main.go 
}

package() {
	cd "$srcdir/$_src"
	install -D "laplace" "$pkgdir/$_exe_files/laplace"	# instalacja pliku wykonywalnego 
	cd "$srcdir/$pkgname"
	install -D "proj-start" "$pkgdir/$_scripts/proj-start" # instalacja skryptów pomocniczych, które nie są integralną częścią oprogramowania 
	install -D "proj-klient" "$pkgdir/$_scripts/proj-klient"
	install -D -m 644 "projector.service" "$pkgdir/$_service_files/projector.service" # instalacja pliku serwisu systemd
	cd "$srcdir/$pkgname/files"
	install -dD "files" "$pkgdir/$_static_files" # instalacja plików serwowanych przez serwer http
	cp -r . "$pkgdir/$_static_files/files"
}
