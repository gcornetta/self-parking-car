## How to configure Raspberry Pi for P2P connnection

### Step 1: Configure the network

Log into the Raspberry Pi, then go to `/etc/network`folder:

```
$ cd /etc/network`
```
Edit the `interfaces` file; however, for safety, save a backup copy:

```
$ sudo cp interfaces interfaces.backup
```
Raspberry Pi has several network interfaces. You must make sure to select the wireless lan to enable P2P over WiFi.
To get information about network interfaces type:

```
$ ifconfig
```
The figure shows the available network interfaces. The wireless interface is named `wlan0` and has been assigned the IP address `192.168.1.10`.

![alt ifconfig output](../screenshots/ifconfig.png "The network interfaces of Raspberry Pi")

To manually configure the network interface `wlan0`, you must edit `/etc/network/interfaces`:
```
$ sudo nano /etc/network/interfaces
```
and add the following commands:
```
1   auto wlan0
2   iface wlan0 inet static
3     address 192.168.100.1
4     netmask 255.255.255.0
5     wireless_channel 1
6     wireless_essid PiRobotCar
7.    wireless_mode ad hoc
```
Line 1 starts the interface at boot. Line 2 assigns a static IP address to the interface. The static address is specified in line 3, whereas lines 4 defines the network submassk. This configuratio has a 24-bit network submask which corresponds to a Class A network (255 possible addresses). Finally, lines 6 defines the name of the network (in this case `PiRobotCar`.

### Step 2: Install the dhcp server
To install the DHCP server execute the following command:
```
$ apt-get install isc-dhcp-server
```

### Step 3: Configure the dhcp server
First edit the server configuration file:
```
$ sudo nano /etc/default/isc-dhcp-server`
```
and add the following line:
```
INTERFACES V4 = "wlan0"

Then edit the dhcp daemon configuration file as follows:
