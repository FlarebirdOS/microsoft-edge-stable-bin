pkgname=microsoft-edge-stable-bin
_pkgname=microsoft-edge
_pkgshortname=msedge
_channel=stable
pkgver=142.0.3595.94
pkgrel=2
pkgdesc="A browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier"
arch=('x86_64')
url="https://www.microsoftedgeinsider.com/en-us/download"
license=('custom')
depends=(
    'alsa-lib'
    'gtk3'
    'libcups'
    'libdrm'
    'libxml2'
    'libxtst'
    'mesa'
    'nss'
)
makedepends=('imagemagick')
provides=(
    'edge-stable'
    'microsoft-edge-stable'
)
conflicts=(
    'edge'
    'edge-stable'
    'edge-stable-bin'
    'microsoft-edge-stable'
)
options=('!strip' '!zipman')
source=(https://packages.microsoft.com/repos/edge/pool/main/m/${_pkgname}-${_channel}/${_pkgname}-${_channel}_${pkgver}-1_amd64.deb
    microsoft-edge-stable.sh)
sha256sums=(3fe98f5e0d20556aa526a052d85fd3b9fe36062927b4f3b447af77c0f0122907
    dc3765d2de6520b13f105b8001aa0e40291bc9457ac508160b23eea8811e26af)

package() {
    bsdtar -xf data.tar.xz -C ${pkgdir}

    # suid sandbox
    chmod 4755 ${pkgdir}/opt/microsoft/${_pkgshortname}/msedge-sandbox

    # 256 and 24 are proper colored icons
    for res in 128 64 48 32; do
        magick ${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_256.png \
            -resize ${res}x${res} \
            ${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_${res}.png
    done
    for res in 22 16; do
        magick ${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_24.png \
            -resize ${res}x${res} \
            ${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_${res}.png
    done

    # install icons
    for res in 16 24 32 48 64 128 256; do
        install -Dm644 ${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_${res}.png \
            ${pkgdir}/usr/share/icons/hicolor/${res}x${res}/apps/${_pkgname}.png
    done

    # User flag aware launcher
    install -m755 microsoft-edge-stable.sh ${pkgdir}/usr/bin/microsoft-edge-stable

    rm ${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_*.png
}
