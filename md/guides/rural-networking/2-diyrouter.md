## Elden Guides - DIY Router
So you got yourself a plan for your phone and a plan for your use. But now you
have a new problem: no consumer router supports this shit. OpenWRT might; *if*
you're lucky enough that your Walmart special router is supported, and *if* it
has a USB port. But it sucks. And the CPU in it probably also sucks for
handling VPN traffic. This is why you need to make your own.

### 1. Assembling Your Shit
Here is a basic overview of what you need:
- A computer with a gigabit ethernet port that can run Linux. This is basically
any computer. Bonus points if it has hardware AES.
- A favorite Linux distro. If you're gonna play sysadmin with it, you better
actually like it or be prepared to learn it. A minimal install is also
recommended; you can install X and a lightweight window manager later if you
have reasons.
- A switch. Unmanaged ones are cheap and will do exactly what you think they do
out of the box.
- A wireless access point. These are also cheap if you don't need Wifi 6
(likely the case if you're here), and often consumer routers can be set to act
as one. And if yours has enough ports, you might not need a standalone switch.
I do not recommend using onboard adapters (or most USB ones) in AP mode, you
*will* have problems and it *will* suck major asshole the entire time it does
actually work.
- Cat5e or Cat6 cables. You probably don't have enough, and half of the ones
you do have are probably missing clips. Just buy some.

Connect your switch and AP and get your OS installed. You will probably have to
tether your phone for the initial installation, if you don't have an existing
service.

### 2. Packages
First you need to install the following packages:
- `dnsmasq`
- `dhcpcd` (unless you use Debian, that comes with netplan)
- `iptables-persistent`
- `libimobiledevice` and `usbmuxd` if you use an iPhone

Also, if you're using Debian, go ahead and stop the `dnsmasq` service now.
Debian likes to start things immediately after you install them, which is
actually fucking stupid for things that basically always need configuring.

### 3. IP Forwarding
In order for your DIY router to pass traffic between the wider internet and
your LAN, you need to enable forwarding. Create a text
file at `/etc/sysctl.d/10-forward.conf` with the following line:
```
net.ipv4.ip_forward=1
```
This will automatically enable packet forwarding on every boot. And yes. The
filename is a TNG reference.

### 4. Setting a LAN IP
You have to serve your network from somewhere, usually the first address in
your network's range. Here we're gonna use the `10.0.0.0/24` subnet, with your
router being `10.0.0.1`. You *can* expand this later if you have that much shit
or want to organize it with static leases.

#### dhcpcd (most distros)
Open `/etc/dhcpcd.conf` and add this:
```
interface eth0
    static ip_address=10.0.0.1/24
```
Replace `eth0` with your LAN adapter's name.

#### netplan (Debian)
Open `/etc/network/interfaces` and add this:
```
auto eth0
iface eth0 inet static
    address 10.0.0.1
    netmask 255.255.255.0
```
As above, make sure the interface name is correct.

I should also say that in my experience, netplan starts way before dnsmasq does
for some reason. I could never get dnsmasq to wait until dhcpcd assigned the
address, and it would fail on the first try.

### 5. DNS and DHCP
Forwarding traffic is a basic function of the kernel. These two services are
what turns a Linux box into what the average Joe considers a "router". And like
basically every firmware out there for consumer routers, we're using `dnsmasq`
for both. It's very simple to customize further and you should be able to "get
it" from reading the config I provide you.

Go ahead and delete `/etc/dnsmasq.conf` and then open
that path again in your editor to make a fresh one. Then paste this in:
```
bind-interfaces
localise-queries
cache-size=500
server=1.1.1.1
interface=eth0
dhcp-range=10.0.0.1,10.0.0.254,255.255.255.0,15m
dhcp-option=3,10.0.0.1
dhcp-option=6,10.0.0.1
local=/lan/
domain=lan
expand-hosts
```

This will assign addresses on the range `10.0.0.2` to `10.0.0.254` with a 15
minute lease, and use Cloudflare for upstream DNS. Again, replace `eth0` if you
need to.

If you want to assign a static lease for something, you need to find its MAC
address and add a line like this to your `dnsmasq.conf`:
```
dhcp-host=xx:xx:xx:xx:xx:xx,some-device,10.0.0.2
```

### 6. Firewall Rules
Now you need to tell your router where and how it is *allowed* to pass traffic.
Open your IPv4 firewall rules file under `/etc/iptables`. It might be named
`rules.v4` or `iptables.rules` depending on your distro. Then replace its
content with this:
```
*nat
:PREROUTING ACCEPT [0:0]
:INPUT ACCEPT [0:0]
:POSTROUTING ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:MINIUPNPD - [0:0]

-A POSTROUTING -s 10.0.0.0/24 -o eth1 -j MASQUERADE

COMMIT

*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:MINIUPNPD - [0:0]

-A INPUT -s 10.0.0.0/24 -p tcp -m tcp --dport 53 -j ACCEPT
-A INPUT -s 10.0.0.0/24 -p udp -m udp --dport 53 -j ACCEPT
-A INPUT -i eth0 -p udp -m udp --dport 67 -j ACCEPT

-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT

COMMIT
```

Again, you should make sure all interface names are correct. `eth0` should be
your LAN and `eth1` your phone.

Another note, explicitly defining the `MINIUPNPD` chain is not necessary, but
if you set up UPnP later for gaming reasons it will prevent headaches.

### 7. Reboot
If you did everything right, you should be able to reboot, connect to your AP
and use this.

### Notes
- You can have as many WAN interfaces and NAT rules as you want. If you happen
to steal your neighbor's internet service (with permission) you can just add a
masquerade rule for it below your phone. It will failover as you'd expect.
- Unconventional WAN interfaces like cellular modems and store-bought wifi
adapters might need extra software and out-of-tree drivers.

[Previous: Rural Internet Options](/guides/rural-networking/1-rural-internet.html)<br/>
[Next: Tethering Considerations](/guides/rural-networking/3-tethering.html)

### Comments
