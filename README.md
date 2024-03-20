# rpi-usb-headless
setup usb headless

cmdline.txt: add 'modules-load=dwc2,g_ether' before 'rootwait'

config.txt: add 'dtoverlay=dwc2,dr_mode=peripheral'

sudo nano /etc/network/interfaces

allow-hotplug usb0
iface usb0 inet static
        address 192.168.7.2
        netmask 255.255.255.0
        network 192.168.7.0
        broadcast 192.168.7.255
        gateway 192.168.7.1
