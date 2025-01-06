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

3. Install a recent version of Git and other tools
```zsh
brew install git
brew install coreutils (only-used by homebrew)
brew install curl (keg-only)
```

4. Install oh-my-zsh
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

5. Install `asdf` (and its dependencies)
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

6. Install pipx
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

7. Install Poetry
```zsh
pipx install poetry
```

8. Set Git Configurations
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

9. Authenticating to GitHub: SSH
I might had followed [this](https://coderefinery.github.io/installation/ssh/).
```zsh
ssh-keygen -t rsa -b 4096
cat /Users/vitorpavinato/.ssh/id_rsa.pub
ssh git@github.com
```

10. Install git-credential-manager
```zsh
brew install --cask git-credential-manager
brew upgrade --cask git-credential-manager
```

11. Display directory as trees
```zsh
brew install tree
```

12. Install htop
```zsh
brew install htop
```

13. Install [Mergiraf](https://mergiraf.org/installation.html).

Mergiraf is a tool that can solve a wide range of Git conflicts. At this point, I decide to use it iteractively instead of registering as a Git merge driver. To use it iteractivelly, follow an example [here](https://mergiraf.org/usage.html#registration-as-a-git-merge-driver).
```zsh
brew install mergiraf
```

14. Install [Diffstatic](https://difftastic.wilfred.me.uk).

Diffstatic is a structural diff tool that understands syntax.
```zsh
brew install difftastic
```

Then add these lines to `.gitconfig` file in the `alias` place. Setup described [here](https://difftastic.wilfred.me.uk/git.html).
```zsh
[alias]        
        # Difftastic aliases, so `git dlog` is `git log` with difftastic and so on.
        dlog = -c diff.external=difft log --ext-diff
        dshow = -c diff.external=difft show --ext-diff
        ddiff = -c diff.external=difft diff

        # `git log` with patches shown with difftastic.
        dl = -c diff.external=difft log -p --ext-diff

        # Show the most recent commit with difftastic.
        ds = -c diff.external=difft show --ext-diff

        # `git diff` with difftastic.
        dft = -c diff.external=difft diff
```

15. Setup a Git `difftool`. Tutorial found [here](https://borgs.cybrilla.com/tils/opendiff-as-difftool/).
```zsh
git config --global diff.tool opendiff
```

or, I added these lines to the `.gitconfig` file :
```zsh
[diff]
        tool = opendiff
```

16. Install GNU parallel
```zsh
brew install parallel
```

## Applications that make all the difference
1. Freedom (from Appstore)
Download from [here](https://freedom.to/dashboard)

2. Install Warp:
```zsh
brew install --cask warp

# Follow Warp Integration from here to set integrate Warp with
# Raycast and vscode (after having these two installed)
# https://docs.warp.dev/features/integrations-and-plugins
```

3. Install iTerm2 (optional):
```zsh
brew install iTerm2
```

4. Install vscode
```zsh
brew install --cask visual-studio-code

# Add the vscode plugin to .zshrc
plugins=(... vscode)

# Open the Command Palette via (F1 or ⇧⌘P) and type shell command to find the Shell Command:
$ Shell Command: Install 'code' command in PATH
```

5. Install Raycast
```zsh
brew install --cask raycast
```

6. Install BBEdit
```zsh
brew install --cask bbedit
```

7. Obsidian
```zsh
brew install obsidian
```

8. Install caffeine (maybe remove needs Rosetta)
```zsh
brew install --cask caffeine
# Need Rosetta. When I installed it, I didn' have Rosetta.
# Later, maybe because some AppStore App needed Rosetta, it was installed.
```

9. Goodnotes (from Appstore)

10. Install NewTerminalHere (from Appstore)

11. Install ReadCube Papers

12. Install Graphic (from Appstore)
Maybe was this one that installed Rosetta as a requirement.

13. Install Vivaldi Browser (non-AI internet)
```zsh
brew install vivaldi
```

14. Install pdfsam-basic (merge pdfs)
```zsh
brew install pdfsam-basic
```

15. Install Logitech Logi Options+
Download from Logitch website

16. Install Tiimo (iPad version from AppStore)

17. Install Microsoft Edge (to export Marp Markdown Slide dec)
```zsh
brew install microsoft-edge
```
18. Install BananaBin from [here](https://bananabin.app/)

19. Install Wolfram Player from [here](https://www.wolfram.com/player/)

20. Install cyberduck (for sftp connection)
```zsh
brew install --cask cyberduck
```

21. Install Mountain Duck (from the same company of cyberduck but it mount the sftp as an external drive) from [here](https://mountainduck.io/) 

22. Install Kindle (from App store)

23. Install Brain.fm desktop (from Brain.fm)

24. Install Proton family of softwares (Email/VNP/Drive/Pass from Proton.me website)
I am trying to move away from american email providers since US regulation on privacy is awful.
Proton.me services were built for privacy (the company was started by former CERN scientists).
Better be safe than sorry when we talk about privacy. I subscribed to the Pro membership which comes 
with email, storage, VPN, password manager etc. For the moment I only tested the email, storage and VPN and those are Desktop app. Proton pass is a browser extension (see below).

25. Install ZSA KeyMapp (from AppStore or from ZSA site???)
It is an app to flash and visualize the ZSA keyboard configuration.

26. Install Keybase (encrypted chat)
```zsh
brew install keybase
```
27. Install Signal (encrypted messaging app, from [here](https://signal.org)):

28. Install Xcode (from Applestore)
```zsh
sudo xcodebuild -license accept
```

## Suggestions from ArjanCode 

1. Install maccy (clipboard manager)
```zsh
brew install maccy
```
2. Install Hidden bar (from Appstore)

3. Install DevToys
```zsh
brew install --cask devtoys
```

## For VPN/remote access to TempleU office computer
1. Install Citrix Secure Access (from Appstore)
2. Install Microsoft Remote Access (from Appstore)

## For the R ecossystem
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

## Vscode extensions
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

## Vivaldi extensions
1. Papers by ReadCub
2. LibKey Nomad
3. Google Scholar Button
4. 1Password
5. Proton Pass (ready to migrate from 1Password to this)  

## Safari extensions
1. 1Password

## Some useful program for bioinformatics
1. Install Bedtools
```zsh
brew install bedtools
```

2. Install Samtools
```zsh
brew install samtools
```

3. Install Bcftools
```zsh
brew install bcftools
```
4. Install htslib
```zsh
brew install htslib
```

5. Install Vcftools
```zsh
brew install vcftools
```

6. Install SLiM/Eidos (from Messer's lab website)

7. Install NCBI-Datasets (binary from NCBI)
- Added the binaries in `~/bioinfo/tools`;
- Then created symlinks to `~/bioinfo/bin/` (see below for instructions to setup `~/bioinfo` folder).

#### Setup a folder for other bioinformatics tools:
In `$HOME`, create a directory called bioinfo. In this folder have this following tree structure:
```zsh
├── README.md
├── bin # Have symlinks to installed tools
├── src # Store source code
├── tools # Have the binaries of installed tools
└── data # Reference data
```
This folder being in $HOME, it avoids a lot of problem that comes with adding binaries to `/usr/local/bin`, which are:
- This location requires sudo to add stuff in there;
- Things in there can conflicts with package manager;
- It is harder to manage multiple versions;
- Stuff there could affect system stability.

To make the binaries in `~/bioinfo/bin` visible to the system, you should add this line to your `~/.zshrc` or `~/.bashrc` file:
```zsh
export PATH="$HOME/bioinfo/bin:$PATH"
```

The workflow for this directory structure:
1. Move to the `~/bioinfo/src` folder;
2. Download the source file;
3. Move to the unzipped/utar folder and run the installer directing the installation to tools (see below for an example);
4. Create a symlink of the program in `tool/` to `bin/` 

Why should I keep a source file after installation:
1. Record keeping of what version/source you used
2. Being able to recompile if needed
3. Having the source available for troubleshooting
4. Keeping track of any modifications you made to the source

Typical workflow when installing a new bioinformatic tool in `bioinfo/`:
```zsh
# Download to src
cd ~/bioinfo/src
wget https://github.com/samtools/samtools/releases/download/1.9/samtools-1.9.tar.bz2

# Extract and compile
tar xjf samtools-1.9.tar.bz2
cd samtools-1.9
./configure --prefix=$HOME/bioinfo/tools/samtools-1.9
make
make install

# Create symlink in bin
cd ~/bioinfo/bin
ln -s ../tools/samtools-1.9/bin/samtools .
```

## Some useful programs for Carpentry
1. Install Powershell
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

2. Install OpenRefine
```zsh
brew install --cask openrefine
```

## Some somehow useful programs
1. Install Zoom (from Zoom)

2. Install Whatsapp (from Appstore)

3. Install Slack 
```zsh
brew install --cask slack
```

4. Install Claude.ai desktop (from Claude.ai)

5. Install (Desktop) chatGPT
```zsh
brew install --cask chatgpt
```

6. Install MS Office (from TempleUPortal)

7. Install Dropbox (from Dropbox) --> I don't use it much, but sometimes is good to have to backup some files that are in my office computer. I hope to replace it with Proton Drive.

8. Install 1password (from Appstore) --> I hope to replace this for Proton Pass

9. NTSF for mac (from Seagate, it is not working)

## TODO's:
- Split this file in different subfolders;
- Make for each a short tutorial (e.g. how to setup a computer for bioinformatics);
- Create a icon for this repository.