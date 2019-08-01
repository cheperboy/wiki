
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU4MTE1MjQ2LDEwMjk5ODEzMjBdfQ==
-->