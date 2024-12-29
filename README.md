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

7. Set Git Configurations
```zsh
gig config --global --edit
git config --global user.name "Vitor Pavinato"
git config --global user.email "vitorpavinato@users.noreply.github.com"
git config --global core.editor "code --wait"
git config --global core.autocrlf input
git config --global init.defaultBranch main
git config --global alias.graph "log --all --graph --decorate --oneline"
git config --list
```

8. Authenticating to GitHub: SSH
I might had followed [this](https://coderefinery.github.io/installation/ssh/).
```zsh
ssh-keygen -t rsa -b 4096
cat /Users/vitorpavinato/.ssh/id_rsa.pub
ssh git@github.com
```

9. Install git-credential-manager
```zsh
brew install --cask git-credential-manager
brew upgrade --cask git-credential-manager
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

~~5. Install Arc Browser

~~Download from Arc page
Removed

7. Install Raycast
```zsh
brew install --cask raycast
```

7. Install Zoom (from Zoom)

8. Install Dropbox (from Dropbox)

9. Install caffeine (maybe remove needs Rosetta)
```zsh
brew install --cask caffeine
# Need Rosetta. When I installed it, I didn' have Rosetta.
# Later, maybe because some AppStore App needed Rosetta, it was installed.
```

10. Display directory as trees
```zsh
brew install tree
```

11. Obsidian
```zsh
brew install obsidian
```

12. Goodnotes (from Appstore)

13. Install 1password (from Appstore)

14. Whatsapp (from Appstore)

15. Install MS Office (from TempleUPortal)

16. Install NewTerminalHere (from Appstore)

17. Install ReadCube Papers

18. Install Graphic (from Appstore)
Maybe was this one that installed Rosetta as a requirement.

19. Install Slack 
```zsh
brew install --cask slack
```

20. Install Vivaldi Browser (non-AI internet)
```zsh
brew install vivaldi
```

21. Install GNU parallel
```zsh
brew install parallel
```

22. Install Xcode (from Applestore)
```zsh
sudo xcodebuild -license accept
```

23. Install Keybase (encrypted chat)
```zsh
brew install keybase
```

24. Install pdfsam-basic (merge pdfs)
```zsh
brew install pdfsam-basic
```

25. Install htop
```zsh
brew install htop
```

26. Install Powershell
```zsh
brew install powershell
```

To initialize the powershell, type in the terminal
```zsh
pwsh
```

Then run this code to make brew available in the powershell
```zsh
New-Item -Path (Split-Path -Parent -Path $PROFILE.CurrentUserAllHosts) -ItemType Directory -Force
  Add-Content -Path $PROFILE.CurrentUserAllHosts -Value '$(/opt/homebrew/bin/brew shellenv) | Invoke-Expression'
```

27. Install (Desktop) chatGPT
```zsh
brew install --cask chatgpt
```

28. Install Logitech Logi Options+
Download from Logitch website

29. Install Tiimo (Ipad version from AppStore)

30. Install iTerm2 (optional):
```zsh
brew install iTerm2
```

31. Install Microsoft Edge (to export Marp Markdown Slide dec)
```zsh
brew install microsoft-edge
```

32. Install BananaBin from [here](https://bananabin.app/)

33. Install Wolfram Player from [here](https://www.wolfram.com/player/)

34. Install OpenRefine
```zsh
brew install --cask openrefine
```

35. Install cyberduck (for sftp connection)
```zsh
brew install --cask cyberduck
```

36. Install Mountain Duck (from the same company of cyberduck but it mount the sftp as an external drive) from [here](https://mountainduck.io/) 

37. Install Kindle (from App store)

38. Install Claude.ai desktop (from Claude.ai)

39. Install Brain.fm desktop (from Brain.fm)

40. Install Proton (mail/VNP/Storage from Proton.me website)
I am trying to move away from american email providers since US regulation on privacy is awful.
Proton.me services were built for privacy (the company was started by former CERN scientists).
Better be safe than sorry when we talk about privacy. I subscribed to the Pro membership which comes 
with email, storage, VPN, password manager etc. For the moment I only tested the email, storage and VPN.

41. SLiM/Eidos (from Messer's lab website)

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

### For VPN/remote access to TempleU office computer
1. Install Citrix Secure Access (from Appstore)
2. Install Microsoft Remote Access (from Appstore)

### For the R ecossystem
I tried to find something similar I have for Python: `asdf` for managing Python versions and `Poetry` for package/installation management.

I found [rig](https://github.com/r-lib/rig) that is R installation manager. Coupled with `renv` they should work just fine.

1. Install rig:
```zsh
brew tap r-lib/rig
brew install --cask rig

brew upgrade --cask rig
```

Usage:
```zsh
# Install an R version (latest)
rig add release

# Set it as default
rig default release
```

Install renv 
```zsh
# Install renv
R
# > install.packages("renv")
```

Install Rstudio (optional but I like to have vscode and Rstudio set up for R):
```zsh
brew install rstudio
```

## For the GO language
I installed GO from the package manager downloaded at [go.dev](https://go.dev/doc/install).
It seems to be the easiest way to install and the go installation allow the installation of 
multiple versions. (throught ASDF is also possible but seems too complicated; see [here](https://gist.github.com/felipemeamaral/7ef508e59a42c4fa0d0b74f219f726c1)).

```zsh
The package installs the Go distribution to /usr/local/go. 
The package should put the /usr/local/go/bin directory in your PATH environment variable. 
You may need to restart any open Terminal sessions for the change to take effect.
```

Check if go is accessible via terminal
```zsh
go version
```

### vscode extensions
1. CMake (twxs)
2. Cmake Tools
3. C/C++
4. C/C++ Themes
5. Code Runner (Jun Han) 
6. Codeium
7. Jupyter
8. Jupyter Cell Tags
9. Jupyter Keymap
10. Jupyter Notebook Renders
11. Jupyter Slide Show
12. learn-markdown
13. Marp for VS Code
14. Pylint
15. Python
16. Python Debugger
17. R Extension
18. R debugger
19. Go (official vscode extension)


