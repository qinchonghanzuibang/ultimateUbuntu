# ultimateUbuntu

This repository will illustrate how I set up my Ubuntu22.04 ARM64(LTS) in parallel desktop. 

#### Update the system

```shell
sudo apt update
sudo apt upgrade
```
#### Install Gnome Tweaks
```shell
sudo apt install gnome-tweaks
```

#### Replace the snap-Firefox

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

