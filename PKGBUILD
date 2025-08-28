pkgname=sudo
pkgver=1.9.17p2
pkgrel=1
pkgdesc="Give certain users the ability to run some commands as root"
arch=('x86_64')
url="https://www.sudo.ws/sudo/"
license=('custom')
groups=('base-devel')
depends=('glibc' 'libxcrypt' 'openssl' 'zlib')
backup=(
    etc/sudo.conf
    etc/sudo_logsrvd.conf
    etc/sudoers
)
options=('!lto')
source=(https://www.sudo.ws/dist/${pkgname}-${pkgver}.tar.gz)
sha256sums=(4a38a1ab3adb1199257edc2a7c4a2bd714665eb605b04368843b06dada2cfcfb)

build() {
    cd ${pkgname}-${pkgver}

    local configure_args=(
        --libexecdir=/usr/lib64
        --with-secure-path
        --with-env-editor
        --with-passprompt="[sudo] password for %p: "
        --docdir=/usr/share/doc/${pkgname}-${pkgver}
        --with-all-insults
        ${configure_options}
    )

    ./configure "${configure_args[@]}"

    make
}

package() {
    cd ${pkgname}-${pkgver}

    make DESTDIR=${pkgdir} install

    # Remove sudoers.dist; not needed since pacman manages updates to sudoers
    rm ${pkgdir}/etc/sudoers.dist

    rm -rf ${pkgdir}/run
}
