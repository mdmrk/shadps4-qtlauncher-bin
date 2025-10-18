# Maintainer: mdmrk <mariodavo.20@gmail.com>

pkgname=shadps4-qtlauncher-bin
_pkgname=shadPS4QtLauncher
_pkgid=net.shadps4.shadPS4QtLauncher
pkgver=2025.10.18.4c9efe0
_date=2025-10-18
_commit=4c9efe028e673fbfdb507b9a627fa5bd94bdcd6d
_shortcommit=4c9efe0
pkgrel=1
pkgdesc="shadPS4 PlayStation 4 emulator Qt launcher"
arch=('x86_64')
url="https://shadps4.net/"
license=('GPL-2.0-only')
options=('!strip')
provides=('shadps4-qtlauncher')
conflicts=('shadps4-qtlauncher')
_appimage=shadPS4QtLauncher-qt.AppImage
source=("shadPS4QtLauncher-linux-qt-${_date}-${_shortcommit}.zip::https://github.com/mdmrk/shadps4-qtlauncher-bin/releases/download/shadPS4QtLauncher-2025-10-18-4c9efe028e673fbfdb507b9a627fa5bd94bdcd6d/shadPS4QtLauncher-linux-qt-2025-10-18-4c9efe0.zip")
sha256sums=('SKIP')

prepare() {
    cd "${srcdir}"
    chmod +x "${_appimage}"
    ./"${_appimage}" --appimage-extract
    sed -i "s|this_dir=\"\$(readlink -f \"\$(dirname \"\$0\")\")\"|this_dir=\"/opt/${_pkgname}\"|" "$srcdir/squashfs-root/AppRun"
}

package() {
    install -dm755 "$pkgdir/opt/${_pkgname}"
    mv "$srcdir"/squashfs-root/* "$pkgdir/opt/${_pkgname}"
    install -dm755 "$pkgdir/usr/bin"
    ln -sf "/opt/${_pkgname}/AppRun" "$pkgdir/usr/bin/shadps4-qtlauncher"
    install -Dm644 "$pkgdir/opt/${_pkgname}/${_pkgid}.svg" -t "$pkgdir/usr/share/pixmaps"
    install -Dm644 "$pkgdir/opt/${_pkgname}/${_pkgid}.desktop" -t "$pkgdir/usr/share/applications"
    sed -i "s|Exec=shadPS4QtLauncher|Exec=shadps4-qtlauncher|" "$pkgdir/usr/share/applications/${_pkgid}.desktop"
    chmod -R u+rwX,go+rX,go-w "$pkgdir/"
}
