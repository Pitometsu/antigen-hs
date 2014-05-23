# antigen-hs

A replacement for [antigen] which has a low overhead when starting up the
shell. I created this plugin because I realized that antigen were the main
cause of slow zsh startup times. After the switch, I went from a loading time
of 1.00 seconds to less than 0.10 seconds (wall clock).

## Installing

Since this plugin is not entirely written in zsh (unlike antigen), it has a few
more installation steps.

### Haskell and packages

Since this plugin is written in Haskell, you have to download it:

    sudo apt-get install ghc cabal-install

The code also depends on the [Shelly] Haskell library:

    cabal update
    cabal install shelly

### Clone and source

This plugin assumes that you put it in `~/.zsh/antigen-hs/`:

    git clone . ~/.zsh/antigen-hs/

Then source it from you zshrc:

    echo 'source ~/.zsh/antigen-hs/init.zsh' >> ~/.zshrc

### Create plugins file

    touch ~/.zsh/MyAntigen.hs
    vim ~/.zsh/MyAntigen.hs

And paste this example content

```haskell
{-# LANGUAGE OverloadedStrings #-}
{-# LANGUAGE ExtendedDefaultRules #-}
module MyAntigen where

import Antigen (AntigenConfiguration (..), bundle, antigen)
import Shelly (shelly)

bundles =
  [ bundle "Tarrasch/zsh-functional"
  , bundle "Tarrasch/zsh-bd"
  , bundle "zsh-users/zsh-syntax-highlighting"
  , bundle "zsh-users/zsh-history-substring-search"
  -- Add your plugins here
  ]

config = AntigenConfiguration bundles

main :: IO ()
main = shelly $ antigen config
```

Now edit this file accordingly by adding your own plugins. Then you're done! :)

## Usage

Reload your shell, execute `antigen-hs-compile` and reload zsh once more.
Each time you update `MyAntigen.hs` you have to run `antigen-hs-compile`

## Limitations

The antigen plugin does way more than it should (just look at its bloated
command list). This plugin tries to be minimal, if you are enough experienced
with computers to use a zsh plugin manager, you can delete and manage the
repositories in `~/.antigen-hs/repos` manually yourself!

[antigen]: https://github.com/zsh-users/antigen
[Shelly]: https://github.com/yesodweb/Shelly.hs
