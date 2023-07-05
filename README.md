# ultimateUbuntu

This repository will illustrate how I set up my Ubuntu22.04 ARM64(LTS) in parallel desktop. 

### Basic Settings

- Disable Panel mode (`Settings/Appearance/Dock`)

- Set the position of Dock on the bottom (`Settings/Appearance/Dock`)

- Change the wallpaper

### Update the system

```shell
sudo apt update
sudo apt upgrade
```
### Install Gnome Tweaks
```shell
sudo apt install gnome-tweaks
```

### Replace the snap-Firefox

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

### Install extension manager

```shell
sudo apt install gnome-shell-extension-manager
```

List of extensions I would recommend (I have emphasized the currently being used ones):

- User Themes.
- Net Speed Simplified
- *Blur my Shell*
- *Vitals*

### Install git

```shell
sudo apt-get install -y git
```

### Install vim

```shell
sudo apt-get install -y vim
```

### Install zsh and oh-my-zsh

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

### Configure the terminal

I have changed the Initial terminal size to 140*40 and disabled Terminal bell. Also, I have changed the shortcuts to suit my own needs. 

1. **Make the terminal look prettier. I personally have chosen the [dracula theme]([Dark theme for Gnome Terminal and 342+ apps — Dracula (draculatheme.com)](https://draculatheme.com/gnome-terminal)).**

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

3. 
