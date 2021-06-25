# Raspberry Pi NAS (Network-Attached Storage)
This document provides a step by step procedure to setup a piNAS on a home network.

## Setup Raspian OS
- Download Raspberry pi imager from: https://www.raspberrypi.org/software/
- Flash a memory card with "Raspberry Pi OS Lite (32-bit)"
- Enable SSH by creating an empty file named "ssh" (no extension) in the "boot" drive
- Enable Wifi by creating the "wpa_supplicant.conf" file as described: https://www.raspberrypi.org/documentation/configuration/wireless/headless.md
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US

network={
        ssid="CV_12136_2A"
        key_mgmt=NONE
}
```
- Insert the flashed memory card into the raspberry pi. 
- Connect it to power, monitor, keyboard and mouse.
- Switch it on and let the boot sequence finish.
- Use default credentials login:"pi" and pass:"raspberry"
- run "sudo raspi-config"
- Under "1 System Options" -> "S3 Password", change default password
- run "sudo apt update" and "sudo apt upgrade"
- run "ip a" and find the ip address
- restart pi using "sudo reboot"

## Setup Openmediavault ([guide](https://openmediavault.readthedocs.io/en/5.x/new_user_guide/newuserguide.html))
- Using another PC, SSH into pi using the ip address, (on powershell- "ssh pi@10.3.15.10")
- Run the script from: https://github.com/OpenMediaVault-Plugin-Developers/installScript (the one which "skip network setup")
- Once installation is complete, open a browser and type the ip address.
- Use default credentials login:"admin" and pass:"openmediavault"
- In System -> General Settings -> Web Administrator Password, change password for OMV user "admin" 
- In System -> Date and Time, change timezone to "America/New_York". SAVE and APPLY.
- Under Storage -> File Systems, mount all the drives. Click APPLY.
- Under Access Rights Management -> Shared Folders, click Add, select Device and set Path as "/" to share complete drive. Repete for each drive. Click APPLY.
- Under Services -> SMB/CIFS, toggle Enable to ON in general settings. SAVE and APPLY.
- Under Services -> SMB/CIFS, go to Shares tab. Click Add. Select Shared folder, set Public to "Guests allowed", toggle ON for inherit permissions, extended attributes & store DOS attributes. SAVE and APPLY. repeat for each folder.





