# ultimateUbuntu

This repository will illustrate how I set up my Ubuntu22.04 ARM64(LTS) in parallel desktop. 

## Table of Contents<a id="content"></a>

- [Basic Settings](#bs)
- [Update the System](#uts)
- [Install Gnome Tweaks](#igt)
- [Replace the snap-Firefox](#rtsf)
- [Install Extension Manager](#iem)
- [Install Git](#ig)
- [Install Vim](#iv)
- [Install Zsh and oh-my-zsh](#izao)
- [Configure the Terminal](#ctt)
- [Install Visual Studio Code](#ivsc)
- [Install Neovim](#ineov)
- [Configure Neovim][#cv]

### Basic Settings<a id="bs"></a>

- Disable Panel mode (`Settings/Appearance/Dock`)
- Set the position of Dock on the bottom (`Settings/Appearance/Dock`)
- Change the wallpaper (can be found in the repo)
- Enable Auto-hide the Dock (`Settings/Appearance/Dock`)

Actually, I undo some of the basic settings to step out of the comfort zone. 

[Back to top](#content)

### Update the System<a id="uts"></a>

```shell
sudo apt update
sudo apt upgrade
```
[Back to top](#content)

### Install Gnome Tweaks<a id="igt"></a>
```shell
sudo apt install gnome-tweaks
```
[Back to top](#content)

### Replace the snap-Firefox<a id="rtsf"></a>

Remove the Firefox snap and add Mozilla team PPA. 

```shell
sudo snap remove firefox
sudo add-apt-repository ppa:mozillateam/ppa
```
Alter the Firefox package priority to ensure PPA/deb/apt version of Firefox is preferred. (Remember to copy and paste it whole instead of line by line).

```shell
echo '
Package: *
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001
' | sudo tee /etc/apt/preferences.d/mozilla-firefox
```

To make the it install upgrades automatically. 

```shell
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:${distro_codename}";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox
```

Finally, install the Firefox via apt.

```shell
sudo apt install firefox
```
[Back to top](#content)

### Install Extension Manager<a id="iem"></a>

```shell
sudo apt install gnome-shell-extension-manager
```

List of extensions I would recommend (I have emphasized the currently being used ones):

- User Themes.
- Net Speed Simplified
- <u>*Blur my Shell*</u>
- <u>*Vitals*</u>
[Back to top](#content)

### Install Git<a id="ig"></a>

```shell
sudo apt-get install -y git
```
[Back to top](#content)

### Install Vim<a id="iv"></a>

```shell
sudo apt-get install -y vim
```
[Back to top](#content)

### Install Zsh and oh-my-zsh<a id="izao"></a>

After install the zsh, we change the default shell from bash to zsh.  Please reboot the machine after you change the shell. 

```shell
sudo apt install zsh
chsh -s /usr/bin/zsh
```

Installing oh-my-zsh, either via curl or wget. 

```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```
[Back to top](#content)

### Configure the Terminal<a id="ctt"></a>

I have changed the Initial terminal size to 140*40 and disabled Terminal bell. Also, I have changed the shortcuts to suit my own needs. 

1. **Make the terminal look prettier. I personally have chosen the [dracula theme](https://draculatheme.com/gnome-terminal).**

```shell
sudo apt-get install dconf.cli
git clone https://github.com/dracula/gnome-terminal
cd gnome-terminal
./install.sh
```

2. **Install oh-my-zsh plugins (Strongly recommended).** 

- zsh-autosuggestions

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Add the plugin for oh-my-zsh to load inside `~/.zshrc`. This step will be the same for all other plugins. 

```sh
plugins=( 
    # other plugins...
    zsh-autosuggestions
)
```

- zsh-syntax-highlighting

```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

3. **Install more Fonts.** 

Install font-manager and create a folder for fonts.

```sh
sudo apt install font-manager
mkdir ~/.fonts
```

Install [Cascadia Code Releases](https://github.com/microsoft/cascadia-code/releases). After extracting the file and install by opening the .ttf file. 
[Back to top](#content)

### Install Visual Studio Code<a id="ivsc"></a>

Download the debian packages [here]([Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/Download)).

```sh
sudo apt install ./<file>.deb
```
[Back to top](#content)


### Install [Neovim](https://github.com/neovim/neovim)<a id="ineov"></a>

This will normally work. However, I am using parallel desktop on a m1 macos and problems occurs that I could only install nvim 0.6 which is way too old. 

```shell
sudo apt update
sudo apt install neovim
```

Install from [sources](https://github.com/neovim/neovim/wiki/Building-Neovim).


```sh
sudo apt-get install ninja-build gettext cmake unzip curl
git clone https://github.com/neovim/neovim
cd neovim
```

I have chosen to install the stable version.

```sh
git checkout stable
make CMAKE_BUILD_TYPE=RelWithDebInfo
sudo make install
```
[Back to top](#content)

### Configure Neovim<a id="cn"></a>

Create required directories and files. (The file tree was generated by `tree`). 

```sh
sudo apt-get install tree
```

All the neovim configuration files are stored inside the `~/.config/nvim`.

```sh
.
├── after
│   └── plugin
│       ├── betterTerm.lua
│       ├── coc.lua
│       ├── code_runner.lua
│       ├── colorscheme.lua
│       ├── fugitive.lua
│       ├── hardline.lua
│       ├── harpoon.lua
│       ├── telescope.lua
│       ├── treesitter.lua
│       └── undotree.lua
├── coc-settings.json
├── init.lua
├── lua
│   └── moonquake
│       ├── init.lua
│       ├── packer.lua
│       ├── remap.lua
│       └── settings.lua
└── plugin
    └── packer_compiled.lua
```

Plugins I use in my neovim:

- [packer](https://github.com/wbthomason/packer.nvim)
- [telescope](https://github.com/nvim-telescope/telescope.nvim)
- [tokyonight](https://github.com/folke/tokyonight.nvim)
- [treesitter](https://github.com/nvim-treesitter/nvim-treesitter)
- [harpoon](https://github.com/ThePrimeagen/harpoon)
- [undotree](https://github.com/mbbill/undotree)
- [vim-fugitive](https://github.com/tpope/vim-fugitive)
- [nvim-autopairs](https://github.com/windwp/nvim-autopairs)
- [coc](https://github.com/neoclide/coc.nvim)
- [code_runner](https://github.com/CRAG666/code_runner.nvim/tree/main)
- [betterTerm](https://github.com/CRAG666/betterTerm.nvim)

You may refer to my [dotfiles](https://github.com/qinchonghanzuibang/dotfiles/tree/main). 

Some problems that might occur: 

1. Cannot use PackerSync or other packer functions unless we source the `packer.lua` first. 

- Solution: Add `require()` statement in the inner `init.lua`. 

2. After installing the tree-sitter plugin, tree-sitter cli not found

- Solution: First install nodejs and npm and export the tree-sitter path in the `~/.zshrc`.

```sh
sodu npm install --global tree-sitter-cl
```

