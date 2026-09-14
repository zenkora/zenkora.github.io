## Elden Guides - Tethering Considerations
So you got yourself a tethering-friendly carrier. Or you didn't, and will do it
anyway. Regardless this isn't standard home broadband. You have more to do if
you want to have a good time.

### TTL Mangling
The simplest and most common way that carriers detect tethering traffic to
count, rate-limit or block it is by inspecting the time-to-live (TTL) values on
your outgoing packets. This starts at a given value dependent on operating
system (64 for Unix, 128 for Windows) and serves to keep errant packets from
looping through the internet forever. Every time a packet goes through a router
(like your tethered phone) this value is decremented by one, and if it reaches
zero the packet is dropped.

To beat this, you will want to make sure all of your traffic has the same TTL
going out, and this can be done by mangling the packets. Add this table to the
end of your iptables rules:
```
*mangle
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:MINIUPNPD - [0:0]

-A POSTROUTING -o eth1 -j TTL --ttl-set 65

COMMIT
```
Replace the subnet with the one you use and the interface with your phone. And
then, so your router does the same, create the file `/stc/sysctl.d/11-ttl.conf`
with this line:
```
net.ipv4.ip_default_ttl=65
```
Note that TTL manipulation alone will not work with heavy-handed carriers that
use deep packet inspection (DPI). A VPN might help in this case by encrypting
your traffic, but they could just throttle that connection. This is why you
want an MVNO that has fewer fucks to give.

### Data Usage
If you did your due diligence and made sure your tethering privileges are
unlimited, you don't have to watch your usage like a hawk, exactly. That perk
comes with an expectation of high data usage. If you're limited to, say, 5Mbps,
you could flood that untampered connection 24/7 every month and likely still be
within the letter of the TOS. Which would add up to *well* over a terabyte of
traffic per month; and that's also pretty realistic with a whole household of
smartphones, consoles, and PCs constantly pulling updates and syncing with
cloud services. And their network engineers aren't stupid, they **know** people
will circumvent their limitations for unlearned scrubs, and they don't give a
shit as long as you don't cause those scrubs problems. They don't want to burn
their bonuses or weekends to spite the other 1% of the population who knows
what a TTL value is (which now includes you!).

### Be Nice to the Network
Regardless of your plan or how technically-okay your usage is, you want to be
nice about it. Don't be the one who abuses a good deal too hard and ruins it
for everyone else.

##### Schedule Your Downloads
You ideally want any bulky transfers to happen when demand is low. Set your
Winblows updates, download managers, and torrent clients to download after
midnight. Keep an eye on your consoles, too. You will probably get drastically
higher speeds at this time anyway, especially in rural areas. Even if you do
rack up an absurd total at the end of the month, most of it happening when the
airwaves are clear is obviously considerate and might cover your ass.

##### Use a VPN
Beyond hiding your activities from Big Brother and your carrier's traffic
shaping, this ensures that your traffic has the same route through your
carrier's network all of the time. That is much easier for them to optimize
around and passes off further routing to your VPN provider. These are covered
next.

### If You Have Limited/No Tethering
You might not be lucky. You might be limited by network compatibility, and/or
not get decent service with a more tethering-friendly carrier. If this is your
predicament, you can still use the internet somewhat normally. But you *need*
to stay under the radar; everything in these guides becomes just about
mandatory. You cannot cut corners, so go back and make sure.

No TTL mangling, you stick out like a sore thumb, and your carrier immediately
knows. No VPN, they see a phone hitting Microsoft and Nintendo game servers and
other shit it never should, and your carrier immediately knows. It's not even a
matter of avoiding throttling, or a data cap, you are just breaking your TOS.

You need to to watch your data usage like a hawk. No constant streaming on
multiple devices, no large downloads, nothing but standard browsing really. A
plan with no tethering comes with the obvious expectation that you're *only*
accessing their network from your phone. If you generate 200GB of traffic in a
month, you'e a very heavy user and probably watch a ton of YouTube. If you rack
up an entire terabyte, that might invite some questions about your use.

To go this route you will probably want to unlock your phone's bootloader and
flash a custom ROM, so the carrier can't just disable the tethering feature.
XDA might be able to help you with that.

[Previous: DIY Router](/guides/rural-networking/2-diy-router.html)<br/>
[Next: Use a VPN](/guides/rural-networking/4-tethering-vpn.html)

### Comments
