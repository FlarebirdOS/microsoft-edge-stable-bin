pkgname=microsoft-edge-stable-bin
_pkgname=microsoft-edge
_pkgshortname=msedge
_channel=stable
pkgver=141.0.3537.99
pkgrel=1
pkgdesc="A browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier"
arch=('x86_64')
url="https://www.microsoftedgeinsider.com/en-us/download"
license=('custom')
depends=(
    'alsa-lib'
    'gtk3'
    'libcups'
    'libdrm'
    'libxtst'
    'mesa'
    'nss'
)
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
source=(https://packages.microsoft.com/yumrepos/edge/Packages/m/${_pkgname}-stable-${pkgver}-1.x86_64.rpm
    microsoft-edge-stable.sh)
sha256sums=(0958f244c3907ad3fbb4b354fd0b9ae5c472987d5dea57479350a2a36e8d8617
    dc3765d2de6520b13f105b8001aa0e40291bc9457ac508160b23eea8811e26af)

package() {
    cp --parents -a {opt,usr} ${pkgdir}

    # suid sandbox
    chmod 4755 ${pkgdir}/opt/microsoft/${_pkgshortname}/msedge-sandbox

    # install icons
    for res in 16 24 32 48 64 128 256; do
        install -Dm644 ${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_${res}.png \
            ${pkgdir}/usr/share/icons/hicolor/${res}x${res}/apps/${_pkgname}.png
    done

    # User flag aware launcher
    install -m755 microsoft-edge-stable.sh ${pkgdir}/usr/bin/microsoft-edge-stable

    rm ${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_*.png
}
