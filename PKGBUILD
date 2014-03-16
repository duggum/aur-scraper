# Maintainer: Dave Jopson <duggum at duggum dot com>
pkgname=aur-scraper
pkgver=1.0.0
pkgrel=1
pkgdesc="A utility to generate a list of packages in the Arch User Repository (AUR)."
url="https://github.com/duggum/aur-scraper"
license=('GPL3')
arch=('any')
optdepends=('sudo: execute applications as non-root'
            'libnotify: status notifications')
source=(https://github.com/duggum/aur-scraper/archive/${pkgname}-${pkgver}.tar.gz)
md5sums=('49fe6d22fac3cb54b4e6668c02d2a21d')

package() {
    cd ${srcdir}/${pkgname}-${pkgver}

    # Installing initial package list
    install -Dm 644 "${srcdir}/${pkgname}-${pkgver}/aur_pkg_list.txt" "$pkgdir/usr/share/aur-scraper/aur_pkg_list.txt"

    # Installing icons
    install -Dm 644 "${srcdir}/${pkgname}-${pkgver}/icons" "$pkgdir/usr/share/aur-scraper/icons"

    # Installing completion files
    install -Dm 644 "${srcdir}/${pkgname}-${pkgver}/completions" "$pkgdir/usr/share/aur-scraper/completions"

    # Installing main script
    install -Dm 755 "${srcdir}/${pkgname}-${pkgver}/aur-scraper" "$pkgdir/usr/bin/aur-scraper"
}
