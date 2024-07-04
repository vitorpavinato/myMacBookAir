# My MacBook Air M2 Setup

Setup of tools and apps for research in computational biology.

## Command-line tools minimun setup
1. Install Xcode command-line tools
```zsh
# In the terminal, type:
xcode-select --install

# Then follow the instruction in the popup window
```

2. Install Homebrew
```zsh
# Check the latest instructions in the Homebrew page:
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Last part of Homebrew installation log:
==> Pouring portable-ruby-3.3.3.arm64_big_sur.bottle.tar.gz
Warning: /opt/homebrew/bin is not in your PATH.
  Instructions on how to configure your shell for Homebrew
  can be found in the 'Next steps' section below.
==> Installation successful!

==> Homebrew has enabled anonymous aggregate formulae and cask analytics.
Read the analytics documentation (and how to opt-out) here:
  https://docs.brew.sh/Analytics
No analytics data has been sent yet (nor will any be during this install run).

==> Homebrew is run entirely by unpaid volunteers. Please consider donating:
  https://github.com/Homebrew/brew#donations

# Do this part below:
==> Next steps:
- Run these two commands in your terminal to add Homebrew to your PATH:
    (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/vitorpavinato/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"
- Run brew help to get started
- Further documentation:
    https://docs.brew.sh
```

3. Install oh-my-zsh
```zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Make some modification in .zshrc:
- set ZSH_THEME="agnoster"
- add plugins: vscode (setup it latter after installing vscode)
- define how the user name would appear
Note: zsh-autosuggestions not installed this type because warp already has it.
```
From Biostar book: add safe versions of the default commands.
They will ask permissions before overwriting files.
```zsh
alias rm='rm -i'
alias mv='mv -i'
alias cp='cp -i'
```

4. Install `asdf` (and its dependencies)
```zsh
# First `asdf` dependencies
brew install coreutils curl git

# Then download
# This is the git installation version
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.0

# Add the following to ~/.zshrc:
. "$HOME/.asdf/asdf.sh"

# append completions to fpath
fpath=(${ASDF_DIR}/completions $fpath)

# initialise completions with ZSH's compinit
autoload -Uz compinit && compinit

# Add asdf python plugin
asdf plugin add python

# Install latest python 3 version
asdf install python latest

# Set it globally
asdf global python latest

# Install python 2.7.18 (latest python 2)
asdf install python 2.7.18
```

5. Install pipx
```zsh
# First install pipix with brew
brew install pipx

# Then run the following pipx command
pipx ensurepath
pipx install argcomplete
pipx completions

# Add this to the .zshrc to allow pipx auto-completions
eval "$(register-python-argcomplete pipx)"

# sudo pipx ensurepath --global
```

6. Install Poetry
```zsh
pipx install poetry
```

## Applications that make all the difference
1. Install Warp:
```zsh
brew install --cask warp

# Follow Warp Integration from here to set integrate Warp with
# Raycast and vscode (after having these two installed)
# https://docs.warp.dev/features/integrations-and-plugins
```

2. Install vscode
```zsh
brew install --cask visual-studio-code

# Add the vscode plugin to .zshrc
plugins=(... vscode)

# Open the Command Palette via (F1 or ⇧⌘P) and type shell command to find the Shell Command:
$ Shell Command: Install 'code' command in PATH
```

3. Install BBEdit
```zsh
brew install --cask bbedit
```

4. Freedom (from Appstore)
Download from [here](https://freedom.to/dashboard)

5. Install Arc Browser
Download from Arc page

6. Install Raycast
```zsh
brew install --cask raycast
```

7. Install Zoom (from Zoom)

8. Install Dropbox (from Dropbox)

<!-- 2. Install caffeine (maybe remove needs Rosetta)
```zsh
brew install --cask caffeine
``` -->

9. Display directory as trees
```zsh
brew install tree
```

10. Obsidian
```zsh
brew install obsidian
```

11. Goodnotes (from Appstore)

12. Install 1password (from Appstore)

13. Whatsapp (from Appstore)

14. Install MS Office (from TempleUPortal)

15. Install NewTerminalHere (from Appstore)

16. Install ReadCube Papers

17. Install Graphic (from Appstore)

Suggestions from ArjanCode 

1. Install maccy (clipboard manager)
```zsh
brew install maccy
```
2. Install Hidden bar (from Appstore)

3. Install DevToys
```zsh
brew install --cask devtoys
```

### vscode extensions
1. Python extension for Visual Studio Code
2. Flake8
3. Pylance
4. Python Debugger
5. yapf
6. Black Formatter   
7. Codeium (auto-pilot)
8. learn-markdown 

### For VPN/remote access to TempleU office computer
1. Install Citrix Secure Access (from Appstore)
2. Install Microsoft Remote Access (from Appstore)