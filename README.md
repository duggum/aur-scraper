## What does aur-scraper do?

Aur-scraper generates a list of package names from the Arch User Repository (AUR) at https://aur.archlinux.org.

#### Why aur-scraper?

The primary purpose of the script is to provide a locally stored list of AUR package names that can be used for bash (or other shell) completion with the [Aura](https://github.com/fosskers/aura) package manager, or any other [AUR helper](https://wiki.archlinux.org/index.php/Aur_helpers) for that matter. All one has to do is write or adapt a [bash completion](http://bash-completion.alioth.debian.org/) script that uses the AUR package list to generate a completion string.

I realize that this is probably very low on most people's _must have_ list. I simply started fiddling with the bash completion script for Aura one day and decided to see if I could incorporate AUR package completion in the same way it exists for official repository packages via [Pacman](https://wiki.archlinux.org/index.php/Pacman).

There may be other uses for such a list, but I haven't really given it much thought. If you have ideas, please share!

#### Installation

While I plan on creating an AUR package, it does not yet exist. Meantime, simply do the following:

1. Clone this repository.
2. Copy/link _aur-scraper_ to a location in your $PATH.
3. Create a directory called _.aura_ in your $HOME directory.
4. Copy the _icons_ directory to _.aura_.
5. Execute _aur-scraper_.

```
    $> git clone git@github.com:duggum/aur-scraper.git
    $> cd aur-scraper
    $> cp aur-scraper $HOME/bin
    $> mkdir -p $HOME/.aura
    $> cp -R icons $HOME/.aura
    $> aur-scraper
```

#### What aur-scraper does:

**tl;dr:** It creates a text file with a list of _most_ AUR package names in it.

It is important to note that the package list created by this script **does not** include packages flagged as _out of date_ or _orphaned_ (i.e., no maintainer). If you want such packages popping up in your bash completion, you are welcome to change the code and make it so.

The following search criteria are used to retrieve all AUR packages that are not flagged out of date:

* category -    any
* search by -   name only
* keywords -    empty
* out of date - not flagged
* sort by -     name
* sort order -  ascending
* per page -    250

Once the raw package data is retrieved, all orphan package entries are removed, then the individual package names are extracted from the HTML and stored in a plain text file.

That's it. You end up with a text file.

#### So, then what?

If you use Aura, a living, breathing bash completion example can be found in the [completions](https://github.com/duggum/aur-scraper/tree/master/completions) folder. Simply copy the completion file to:

    /usr/share/bash-completion/completions/aura

Otherwise, you can use your shell completion tool(s) to access the list and _tab+tab_ your way to AUR completion bliss.

For example, for Bash you might have something like this:

    aur_pkgs=$( cat "aur_pkg_list.txt" )
    COMPREPLY=($( compgen -W "$aur_pkgs" -- "$cur" ))

For the visually impressed:

![](https://www.copy.com/TLqStMfpML4w)

#### Beware!!

In case you didn't notice in the image above, you will end up with a list of 30,000+ package names (out of 47,630 at last check). Downloading and processing the raw HTML from the AUR website takes time:

![](https://copy.com/wLSRNLqxK78V)

While a few minutes on a one-off run isn't a big deal, the AUR is a moving target. Depending on your use of the repository, you may want to update your local list more or less frequently. Some options to do so include:

* run in background via cron job
* run in background at desktop session login
* run manually
* pay your kid five bucks to execute a key-combo every four hours throughout the day

If anyone knows of a more efficient way to get the necessary information without cycling through the standard AUR search pages, please let me know, or [fork](https://help.github.com/articles/fork-a-repo) and fix as you see fit.

#### Final disclaimer

I am a novice at all this stuff. I am not an expert at shell scripting, nor am I a real programmer. I simply found something that I thought would be interesting to work on, and I did so. Then, I thought I would share it with others. That's it, nothing more.

With that in mind, I welcome advice and constructive feedback. The script is heavily commented, so it shouldn't be hard for anyone to figure out the madness in my method.
