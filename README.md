RTL8188FU driver for Linux kernel 6.1+ (Arch Linux)

info: rtl8188fu support will be add to rtl8xxxu module of Linux kernel. https://patchwork.kernel.org/project/linux-wireless/patch/b14f299d-3248-98fe-eee1-ba50d2e76c74@gmail.com/

Note: At this point there is no such support on Arch linux yet, and it seems that it won't suppor AP mode, which makes it useless for many of us.

------------------

## How to install

`sudo apt-get install build-essential git dkms linux-headers-$(uname -r)`

`git clone https://github.com/elchild/rtl8188fu`

`sudo dkms install ./rtl8188fu`

`sudo cp ./rtl8188fu/firmware/rtl8188fufw.bin /lib/firmware/rtlwifi/`

------------------

## Configuration

#### Disable Power Management

Run following commands for disable power management and plugging/replugging issues.

`sudo mkdir -p /etc/modprobe.d/`

`sudo touch /etc/modprobe.d/rtl8188fu.conf`

`echo "options rtl8188fu rtw_power_mgnt=0 rtw_enusbss=0" | sudo tee /etc/modprobe.d/rtl8188fu.conf`

#### Disable MAC Address Spoofing

Run following commands for disabling MAC Address Spoofing (Note: This is not needed on Ubuntu based distributions. MAC Address Spoofing is already disable on Ubuntu base).

`sudo mkdir -p /etc/NetworkManager/conf.d/`

`sudo touch /etc/NetworkManager/conf.d/disable-random-mac.conf`

`echo -e "[device]\nwifi.scan-rand-mac-address=no" | sudo tee /etc/NetworkManager/conf.d/disable-random-mac.conf`

#### Blacklist for kernel 5.15 and 5.16 (No needed for kernel 5.17 and up)

If you are using kernel 5.15 and 5.16, you must create a configuration file with following commands for preventing to conflict rtl8188fu module with built-in r8188eu module.

`echo 'alias usb:v0BDApF179d*dc*dsc*dp*icFFiscFFipFFin* rtl8188fu' | sudo tee /etc/modprobe.d/r8188eu-blacklist.conf`


------------------

## How to uninstall

`sudo dkms remove rtl8188fu/1.0 --all`

`sudo rm -f /lib/firmware/rtlwifi/rtl8188fufw.bin`

`sudo rm -f /etc/modprobe.d/rtl8188fu.conf`
