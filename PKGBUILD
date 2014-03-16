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
source=(https://github.com/duggum/${pkgname}/archive/${pkgver}.tar.gz)
md5sums=('cdd4a9185f299ec862f99f6804d47957')

package() {

    local file spref shdir sdir ddir
    spref="$srcdir/$pkgname-$pkgver"
    shdir="usr/share/aur-scraper"

    cd "$spref"

    # Installing initial package list
    install -Dm 644 "$spref/aur_pkg_list.txt" "$pkgdir/$shdir/aur_pkg_list.txt"

    # Installing icons
    sdir="$spref/icons"
    ddir="$pkgdir/$shdir/icons"
    for file in $( ls "$sdir" ); do
        install -Dm 644 "$sdir/$file" "$ddir/$file"
    done

    # Installing completion files
    sdir="$spref/completions"
    ddir="$pkgdir/$shdir/completions"
    for file in $( ls "$sdir" ); do
        install -Dm 644 "$sdir/$file" "$ddir/$file"
    done

    # Installing main script
    install -Dm 755 "$spref/aur-scraper" "$pkgdir/usr/bin/aur-scraper"

    unset file spref shdir sdir ddir
}
