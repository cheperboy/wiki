



# OS installation and configuration

## 1_ Install and configure Raspbian
1.  Format SD card FAT32
2.  Download [Raspbian](https://www.raspberrypi.org/downloads/raspbian/) image
3.  Flash image with [Etcher](https://www.balena.io/etcher/)
    

## 2_ Hardware setup

Add at the end of boot/config.txt
	# mj Enable the kernel module allowing 1-wire communication on GPIO-4
    dtoverlay=w1-gpio

  

###### # mj enable i2C for ADC ADS1115

###### dtparam=i2c1=on

  

Reboot and edit /etc/modules

###### w1-gpio

###### w1-therm
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAyOTk4MTMyMF19
-->