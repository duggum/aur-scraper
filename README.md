## What does aur-scraper do?

Aur-scraper generates a list of package names from the [Arch User Repository (AUR)](https://aur.archlinux.org).

### Why aur-scraper?

The primary purpose of the script is to provide a locally stored list of AUR package names that can be used for bash (or other shell) completion with an [AUR helper](https://wiki.archlinux.org/index.php/Aur_helpers). All one has to do is write or adapt a [bash completion](http://bash-completion.alioth.debian.org/) script to use the AUR package list to generate a completion string.

There may be other uses for such a list, but I haven't really given it much thought. If you have ideas, please share!

**Note:** I realize that this is probably very low on most people's _must have_ list. I was simply messing around with the bash completion script for [Aura](https://github.com/fosskers/aura) one day and decided to see if I could incorporate AUR package completion in the same way it exists for official repository packages via [Pacman](https://wiki.archlinux.org/index.php/Pacman).

### Installation

Since this is an Arch Linux specific package, and until an AUR package is available, it is highly recommended that you install it by using the included PKGBUILD, as follows:

1. download the PKGBUILD to a convenient location
2. change into that directory and...

```bash
$> makepkg -c
$> makepkg -i
```
**or**

````bash
$> makepkg -c
$> pacman -U aur-scraper-1.0.0.pkg.tar.xz
$> sudo aur-scraper
````

**then**

````bash
$> sudo aur-scraper
````

As an alternative, you can clone the repo and place the files anywhere you want as long as you have write access and change the following directory variables to match your setup:

````bash
DATA_DIR="/usr/share/aur-scraper"
LOG_DIR="/var/log"
TEMP_DIR="/tmp"
````

**Note:** An existing package list is provided with the installation, but you should update that immediately since it will be outdated.

### What aur-scraper does:

**tl;dr:** It creates a text file with a list of _most_ AUR package names in it.

It is important to note that the package list created by this script **does not** include packages flagged as _out of date_ or _orphaned_ (i.e., no maintainer). If you want such packages popping up in your bash completion, you are welcome to change the code and make it so.

1. The following search criteria are used to retrieve all AUR packages that are not flagged out of date:
    * category -    any
    * search by -   name only
    * keywords -    empty
    * out of date - not flagged
    * sort by -     name
    * sort order -  ascending
    * per page -    250
2. ll orphan package entries are removed from the raw HTML.
3. The individual package names are extracted and stored in a plain text file.

That's it. You end up with a text file.

### So, then what?

If you use Aura, a living, breathing bash completion example can be found in the completions folder at:

````
/usr/share/aur-scraper/completions/aura_bash-completion
````

Simply do this as root:

````bash
$> mv /usr/share/bash-completion/completions/aura /usr/share/bash-completion/completions/aura.bak
$> cp /usr/share/aur-scraper/completions/aura_bash-completion /usr/share/bash-completion/completions/aura
````

Otherwise, you can use your favourite shell completion tool(s) to access the list and _\<tab\>+\<tab\>_ your way to AUR completion bliss.

For example, for Bash you might have something like this:

````bash
aur_pkgs=$( cat "aur_pkg_list.txt" )
COMPREPLY=($( compgen -W "$aur_pkgs" -- "$cur" ))
````

For those who require visuals:

![AUR Completion in Action](https://copy.com/TLqStMfpML4w)

### Beware!!

In case you didn't notice in the image above, you will end up with a list of 30,000+ package names (out of 47,630 at last check). Downloading and processing the raw HTML from the AUR website takes time:

![aur-scraper Run Time](https://copy.com/wLSRNLqxK78V)

While a few minutes on a one-off run isn't a big deal, the AUR is a moving target. Depending on your use of the repository, you may want to update your local list more or less frequently. Some options to do so include:

* run in background via cron job
* run in background at desktop session login
* run manually
* pay your kid five bucks to execute a key-combo every four hours throughout the day

If anyone knows of a more efficient way to get the necessary information without cycling through the standard AUR search pages, please let me know, or [fork](https://help.github.com/articles/fork-a-repo) and fix as you see fit.

### Final disclaimer

I am a novice at all this stuff. I am not an expert at shell scripting, nor am I an experienced programmer. I simply found something that I thought would be interesting to work on, I did so, and now I feel like sharing what I did with others. That's it, nothing more.

With that in mind, I welcome advice and constructive feedback. The script is heavily commented, so it shouldn't be hard for anyone to figure out the method to my madness.
