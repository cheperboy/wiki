
# Installation
1. Format SD card FAT32
2. Download [Raspbian](https://www.raspberrypi.org/downloads/raspbian/)image
3. Flash image with [Etcher](https://www.balena.io/etcher/)
4. Create a file `boot/ssh` before booting raspbian to enable ssh

# Wifi setup before first boot
[help](https://howchoo.com/g/ndy1zte2yjn/how-to-set-up-wifi-on-your-raspberry-pi-without-ethernet)

From Windows PC with Notepad++ in SD card in partition “boot”
Create file `boot/wpa_supplicant.conf` 
(Raspbian will move it in `/etc/wpa_supplicant/` when the system is booted)
In Notepad++“Edit” > “EOL Conversion” > “UNIX/OSX Format”. “UNIX” is then shown in the status bar.
Add content:
```shell
country=FR # Your 2-digit country code
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="YOUR_NETWORK_NAME"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}
```

# Wifi setup after first boot
If conf is done after first boot, edit wpa_supplicant.conf
`sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`
```shell
network={
    ssid="YOUR_NETWORK_NAME"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}
```

# Configuration
## Hostname and password
1.  Modify hostname, Edit `/etc/hostname`. Set to chaudiere (recognized on network as *chaudiere.local*)
2.  Modify pi password `sudo passwd pi`
 
## Package install
**Update/upgrade system and existing packages**

`sudo apt-get update` met à jour la liste des dépôts

`sudo apt-get dist-upgrade -y` met à jour tous les paquets installés vers les dernières versions en installant de nouveaux paquets si nécessaire

`sudo apt-get upgrade -y` met à jour tous les paquets installés sur le système

**Install packages**

`sudo apt-get -y install supervisor git python-pip nginx`

`pip install virtualenv virtualenvwrapper`

[tuto virtualenv](https://virtualenvwrapper.readthedocs.io/en/latest/install.html)

**specific packages for chaudiere app**

`sudo apt-get install curl`

NEXMO need cryptographie and cffi

`sudo apt-get install build-essential libssl-dev libffi-dev python-dev`

**clean**

`sudo apt-get clean` supprime les paquets téléchargés et stockés sur carte SD


## bashrc
`nano ~/.bashrc`
```shell
# ls alias
alias ll='ls -l'
alias la='ls -A'
alias lla='ls -la'
alias l='ls -CF'

# supervisor alias
alias restart_all='sudo supervisorctl restart all'
alias status='sudo supervisorctl status'
alias start_script='sudo supervisorctl start script'
alias stop_script='sudo supervisorctl stop script'

# other alias
alias dev='cd /home/pi/Dev/chaudiere/'
alias prod='cd /home/pi/Prod/chaudiere/'

# load virtualenvwrapper for python (after custom PATHs)
export WORKON_HOME=~/Envs
source /home/pi/.local/bin/virtualenvwrapper.sh

# workon dev env when the consol is open 
workon dev
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjQ3OTY4NTA3LC04NzI1MjgyNCwtODIxOD
ExNTcyLDE2MjEwMzA3MTUsMTAyOTk4MTMyMF19
-->