# Cablize_between_Odroid_and_Tablet

# Introduction
* This document describe how to config Odroid to have a wired ethernet-like network interface with Tablet.

# Procedures
* make sure the NetworkManager.conf content
        odroid@odroid:~$ cat /etc/NetworkManager/NetworkManager.conf 
        [main]
        plugins=ifupdown,keyfile,ofono
        dns=dnsmasq
        
        [ifupdown]
        managed=false
* make sure the /etc/network/interfaces
        $ cat /etc/network/interfaces
        # interfaces(5) file used by ifup(8) and ifdown(8)
        # Include files from /etc/network/interfaces.d:
        source-directory /etc/network/interfaces.d
        
        auto usb0
        iface usb0 inet static
           address 192.168.42.180 
           netmask 255.255.255.0
           network 192.168.42.0
           gateway 192.168.42.129
           dns-nameservers 8.8.8.8
* make sure the ROS_IP=192.168.42.180 in ~/.bashrc
        $ cat ~/.bashrc
        #export ROS_IP=`/sbin/ifconfig | awk -F'[ :]+' '/Bcast/{print $4}'`
        export ROS_IP=192.168.42.180
