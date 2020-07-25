## Experiments With the PocketBeagle

The pocketbeagle is yet another small device capable of running Linux. The hardware is based on ARM technology. It was designed by Texas Instruments, who placed the hardware design in open source. The PocketBeagle is manufactured by ???, and is the smallest (and cheapest) of several similar devices including BeagleBone, Beagle Bone, Black, etc, etc.  

I have become interested in PocketBeagle as an alternative to the Raspberry Pi - specifically in terms of its reduced power consumption, direct analog input and open source documentation. It remains to be seen whether or not the PocketBeagle can be placed in a low-power sleep mode suitable for long-term battery-powered operation. Communication is another open question: as sold and shipped, the PocketBeagle has only a single USB port that serves both power and communication. However, PocketBeagle has several interfaces - GPIO, analog I/O, and auxiliary hardware boards are also available. Other members of the "Beagle Family" include Bluetooth, WiFi, etc - testament to the processor's ability to support comms.

### Baby Steps

First order of business is to power up the PocketBeagle, and make a connection. I will try this first with a Linux laptop, and then with a Raspberry Pi. The documentation states that the PocketBeagle communicates with the *outside world* over TCP/IP connections - HTTP and SSH for example. Which raises my first question: "*How does that work - this [Ethernet over USB](https://community.st.com/s/question/0D50X00009XkZ0GSAV/ethernet-over-usb)?*"  ([*See also Wikipedia re Ethernet-over-USB*](https://en.wikipedia.org/wiki/Ethernet_over_USB)) 

The Wikipedia article is informative. It contains at least two *revelations*: 

1. Ethernet over USB is now **transparent** to applications
2. Ethernet over USB is **20 years old** - maybe before you even knew what Ethernet or USB were! 

> The USB-eth module in Linux makes the computer running it a variation of an Ethernet device that uses USB as the physical medium. It creates a Linux network interface, which can be assigned an IP address and  otherwise treated the same as a true Ethernet interface.  ***Any  applications that work over real Ethernet interfaces will work over a  USB-eth interface without modification, because they can't tell that  they aren't using real Ethernet hardware***.[REF](https://www.embedded.com/linux-based-usb-devices/)  *(emphasis mine)* 
>
> On Linux hosts, the corresponding Ethernet-over-USB kernel module is called usbnet. The Bahia Network Driver[[2\]](https://en.wikipedia.org/wiki/Ethernet_over_USB#cite_note-2) is a usbnet-style driver available for Win32 hosts.

 #### Linux laptop connectivity:

With









#### Raspberry Pi connectivity:

Using an old RPi 1BP model running `buster`: With the PocketBeagle plugged into one of the RPi's USB ports, `ifconfig` shows a different picture than it did on the Linux laptop. Note the MAC addresses shown by the RPi are the same as with the Linux laptop, but they are assigned the same IP address as the native `eth0` used for networking this RPi.

Given that the PocketBeagle's MAC addresses appear in this list, it should be possible to route/transfer packets to them, and *initiate* a connection to the PocketBeagle from another host on the network. ***How?*** becomes the operative question! 



```bash
pi@raspberrypi1bp:~ $ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.179  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 2605:a601:a82a:e600::1bfa  prefixlen 128  scopeid 0x0<global>
        inet6 fe80::522e:669e:c4ee:3aaa  prefixlen 64  scopeid 0x20<link>
        ether b8:27:eb:3a:b9:78  txqueuelen 1000  (Ethernet)
        RX packets 6343845  bytes 808844488 (771.3 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 124862  bytes 14526766 (13.8 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.179  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::82b9:1242:f782:cf5b  prefixlen 64  scopeid 0x20<link>
        ether 60:64:05:fa:81:3d  txqueuelen 1000  (Ethernet)
        RX packets 1355  bytes 42333 (41.3 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 64  bytes 17947 (17.5 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth2: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.179  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::de2c:afba:63a4:d3bb  prefixlen 64  scopeid 0x20<link>
        ether 60:64:05:fa:81:3b  txqueuelen 1000  (Ethernet)
        RX packets 41  bytes 6226 (6.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 61  bytes 20337 (19.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

