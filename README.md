aur-scraper
===========

Generates a local list of package names from the Arch User Repository (AUR) at https://aur.archlinux.org.

The primary purpose of the script is to provide a list of package names that can be used for bash (or other shell) completion for the Aura package manager.

##### Installation

While I plan on creating an AUR package, it does not yet exist. Meantime, simply clone the repo and do the following:

1. Clone this repository.
2. Copy/link _aur-scraper_ to a location in your $PATH.
3. Create a directory called _.aura_ in your $HOME directory.
4. Copy the _icons_ directory to _.aura_.
5. Execute _aur-scraper_.

    $> git clone git@github.com:duggum/aur-scraper.git
    $> cd aur-scraper
    $> cp aur-scraper $HOME/bin
    $> mkdir -p $HOME/.aura
    $> cp -R icons $HOME/.aura
    $> aur-scraper
