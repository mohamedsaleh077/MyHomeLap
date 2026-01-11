# My Home Lap!
I used my 12-years-old x86 pc as a server in my room! and here I am documenting everything related to it. I will leave a refrence for any thing you may can not understand!
## Hardware
### Server Specs:
![photo of my pc](https://www.hardware-corner.net/wp-content/uploads/compare/main/HP_EliteDesk_800_G1_SFF_main.jpg)
- Model: [HP EliteDesk 800 G1 SFF](https://www.hardware-corner.net/desktop-models/HP-EliteDesk-800-G1-SFF/)
- CPU: [Intel(R) Celeron(R) G1840 (2) @ 2.80 GHz](https://www.intel.com/content/www/us/en/products/sku/80800/intel-celeron-processor-g1840-2m-cache-2-80-ghz/specifications.html).
    - 2 [core](https://en.wikipedia.org/wiki/Multi-core_processor), 2 [thread](https://en.wikipedia.org/wiki/Thread_(computing)).
- Generation: [HASWELL](https://en.wikipedia.org/wiki/Haswell_(microarchitecture))
- Power Supply: 270W, if I am not wrong.
- Memory: 6GB
    - 3 slots of 2GB ddr3 with about 1300mhz or something like that.
- GPU: Intel Xeon E3-1200 v3/4th Gen Core Processor Integrated Graphics Controller @ 1.05 GHz [Integrated]
    - aka: intel HD integrated GPU
- Storage:
    - WDC [WD5000AAKX](https://www.newegg.com/Western-Digital-Blue-WD5000AAKX-500GB/p/N82E16822136769?recaptcha=pass) (WD blue 500GB 7200RPM) 2015 
    - WDC [WD6400AARS](https://www.newegg.com/western-digital-wd-green-wd6400aars-640gb/p/N82E16822136737) (WD Green 640GB 5400RPM - 12% health) 2010 :( I am using it as a read-only archive for useless stuff, it is dangerouse to keep important data on it.
- cheap old [ZTE router](https://www.amazon.eg/-/en/Zte-H108n-Adsl2-Wireless-Router/dp/B091J99485) for 150EGP (10USD ig).
- cheap CAT6 LAN cable, two meters, for 20EGP (0.4USD).

This is a very old pc made for simple bussines, very cheap and used, I bought it without any disks and 4gb of ram in 2020 or 2021 for 600EGP (40USD) in that time.

My dad got the old 640GB HDD many years ago when we was using a Pentium Dual Core TawerPC with 1GB of ram, so we changed it in 2023 with another used HDD, the 500GB blue one, it was about 200EGP (7USD) in that time, this HDD in his half life time, but works fine ig.

also I had a 2gb slot of ram from my previouse PC, it was ddr2 and I replaced it, with no charge lol.

### Router: ZXHN H108N V2.5 2015
I have edited some settings to get the max possible speed in local network, you can access the admin panel from `192.168.1.1` using `admin`, `admin` as credintials, here it is:
- Network > WLAN 	 	
    - Mode: mixed(802.11b,802.11g,802.11n)
    - Band Width: 40Mhz
    - Channel: 13	
    - SGI Enable: yes	
    - Beacon Interval 100 ms
    - Transmitting Power: 80%	
    - QoS Type: WMM
    - RTS Threshold: 2300 	
    - DTIM Interval: 1
- Netwrok > LAN > DHCP Binding
    - here I acossiated a static IP (192.168.1.20) for my PC MAC address.
- Security > Firewall > Firewall level: low
- also DNS is `1.1.1.1` and `8.8.8.8`

you can use any Ai tool like Gemini or whatever to guide you if you are lazy to search for each property.

Speed in SFTP is about 5MB/s to 10MB/s and this is enough for me.

## SoftwareDebian
- [OS](https://en.wikipedia.org/wiki/Operating_system): [Debian](https://en.wikipedia.org/wiki/Debian) GNU/Linux 13 (trixie) x86_64
- [Kernel](https://en.wikipedia.org/wiki/Kernel_%28operating_system%29): [Linux](https://en.wikipedia.org/wiki/Linux) 6.12.43+deb13-amd64
- [Packages](https://en.wikipedia.org/wiki/List_of_software_package_management_systems): 1653 ([dpkg](https://en.wikipedia.org/wiki/Deb_(file_format)))
- 3GB [ZRAM](https://en.wikipedia.org/wiki/Zram) ([zstd](https://en.wikipedia.org/wiki/Zstd) algorithm)
- NO [SYSTEMD](https://en.wikipedia.org/wiki/Systemd)! I nuked it and using [sysvinit](https://en.wikipedia.org/wiki/Init#SYSV) (The OG).

### what is systemd and sysvinit?
these peices of software is used to manage services, start the system and preparing userspace in youe linux os

### why I nuked systemd?
systemd is a good piece of software and offer many benifits, but it becomes useless when it eat your resources, why to use this while you can use any other old simple way to manage your services and hardware?

### what any simple init system offers?
- faster boot time (since it is a simple script starts services).
- lower ram usage (because it is just a process handle other proccess or a proccess just start other proccess, like runit).
- much simpler in usage and doesn't have many features that you do not need.

### why it is not widly used?
- systemd aim to make everything the same in all linux distrobutions, this may make you happy since you wont suffer here and there, but will kill the varity, but stability and compatability is the priority now!
- systemd is now supported everywhere and most apps works out-of-box with it, not like other simple init systems, this is because of developers and time not init system fault or red hat is evil.
- provide more and more and more features you may need, who know? in logging and mangment drivers, etc etc.
- much easier for most users since it is now more known and have many tutorials about it, not like the forgotten init systems.

in my case, I need the performance as the first priority, and I am expert enough to handle it so why not?

there is still many distrobutions using init systems because of their developers phylosiphi, like [Voidlinux](https://en.wikipedia.org/wiki/Void_Linux), [Artix](https://en.wikipedia.org/wiki/Artix_Linux), [MXLinux](https://en.wikipedia.org/wiki/MX_Linux)(have option to switch from systemd to [openrc](https://en.wikipedia.org/wiki/OpenRC)) and [Devuan](https://en.wikipedia.org/wiki/Devuan).

### why I picked sysvinit?
for no reason really, Internet in Egypt is limited so I have already debian, instead of wasting my quota on devuan, I changed it by myself, it is dangrouse and expermential proccess but I will discuess all of this here.

### why not [runit](https://en.wikipedia.org/wiki/Runit) or [dinit](https://github.com/davmac314/dinit) since they are much better?
sysvinit is the easist one to install on debian, others will bring me to the hell...