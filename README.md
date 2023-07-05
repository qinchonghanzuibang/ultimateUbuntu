# ultimateUbuntu

This repository will illustrate how I set up my Ubuntu22.04 ARM64(LTS) in parallel desktop. 

### Settings

Disable Panel mode (Settings/Appearance/Dock)

Set the position of Dock on the bottom (Settings/Appearance/Dock)

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
- **Blur my Shell**
- **Vitals**

### Install git

```shell
sudo apt-get install -y git
```

### Install vim

```shell
sudo apt-get install -y vim
```

