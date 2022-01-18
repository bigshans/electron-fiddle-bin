# Maintainer: bigshans <wo199710@hotmail.com>

pkgname=electron-fiddle-bin
_pkgname=fiddle
pkgver=0.27.2
pkgrel=1
pkgdesc="The easiest way to get started with Electron"
arch=('x86_64')
url="https://electronjs.org/fiddle"
license=('MIT')
depends=('electron')
conflicts=('electron-fiddle' 'electron-fiddle-git')
provides=("$pkgname" "$pkgname")
source=("$_pkgname-$pkgver.deb::https://github.com/electron/fiddle/releases/download/v${pkgver}/electron-fiddle_${pkgver}_amd64.deb ")
sha256sums=('d40aa80dc2a3467855cb3eaf60b3a529bbdc92c060f45e4c76b39b3c172b4d5e')

prepare() {
    ar -x $_pkgname-$pkgver.deb
    local extract_path=$srcdir/$_pkgname-$pkgver
    mkdir -p $extract_path
    tar xvf data.tar.xz --directory=$extract_path
	cd $extract_path
}

package() {
	cd "$srcdir/$_pkgname-$pkgver/usr/lib/electron-fiddle/resources"
	install -Dm644 app.asar "$pkgdir/usr/lib/electron-fiddle/app.asar"

	cd "$srcdir/$_pkgname-$pkgver/usr/share/icons/hicolor/scalable/apps"
	install -Dm644 electron-fiddle.svg "$pkgdir/usr/share/icons/hicolor/scalable/apps/electron-fiddle.svg"

	cd "$srcdir"
	echo "#!/bin/env sh
exec electron /usr/lib/electron-fiddle/app.asar \$@
" > electron-fiddle.sh
	install -Dm755 electron-fiddle.sh "$pkgdir/usr/bin/electron-fiddle"

	echo "[Desktop Entry]
Name=Electron Fiddle
Comment=The easiest way to get started with Electron
GenericName=Electron Fiddle
Exec=electron-fiddle %U
Icon=electron-fiddle
Type=Application
StartupNotify=true
Categories=GNOME;GTK;Utility;
" > electron-fiddle.desktop
	install -Dm755 electron-fiddle.desktop "$pkgdir/usr/share/applications/electron-fiddle.desktop"
	install -Dm644 $srcdir/$_pkgname-$pkgver/usr/share/doc/electron-fiddle/copyright "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

}
