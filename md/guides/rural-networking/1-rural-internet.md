## Elden Guides - Rural Internet Options
If you live in rural America, you are a second-class internet citizen. And if
you're not technologically inclined, you are kind of fucked. But that's what
this entire section of guides is really for: to help you get un-fucked.

You probably dream of a nice, symmetrical-gigabit fiber connection going right
to your house, with a public IP you can host games and servers on to your
heart's content. But you're in the sticks, so that's not gonna happen. You have
few options and they all know it.

### Option 1: Satellite Internet
You're probably deeply familiar with satellite internet. It might even fill you
with a deep sense of dread and perhaps even be the reason for your chronic
depression. You pay out the ass to get 700ms ping and data caps that weren't
even acceptable for a cell plan from a decade ago. Then, once you're out of
data, you're throttled to about 125Kbps. Which is like low-end DSL but with
satellite latency.

### Option 2: DSL
You might live in a place that still offers DSL over phone lines. This is
slightly better and more stable than satellite service, but is still a complete
pile of shit for what you pay. You will probably be given a bargain bin router
with a builtin DSL modem, and it's a whole pain in the ass to use your own
hardware. DSL is best left to die and disappear like satellite.

### Option 3: Starlink
Elon Musk's satellite internet company stepped in a while back to kill the two
above. And it's alright. But it comes with its own problems.

The equipment is expensive as hell and the monthly cost of service is steep.
You *will* sometimes get such amazing speeds that you could redownload your
entire Steam library in an hour. But as soon as there's a cloud in the sky it
will go to hell. Your IP address will change often, getting you blocked by
uptight asshole services like Hulu. Also your latency, and the locations sites
believe you to be in, can vary depending on which base station your Starlink
satellite decides to use. You could be in Texas and have your traffic routed
through Chicago. It's decent enough if you have money to burn and torrent a
lot, I guess.

### Option 4: Cellular "Home Internet"
Many rural areas can get a pretty strong LTE or 5G connection. Carriers have
caught on to this in recent years and started offering legit home broadband.
But, of course, they don't offer this everywhere for one unknowable reason or
another. It can also be more expensive than a cell line. And you're still
subject to things cell carriers do like throttling your video streams to 480p,
blocking torrents, etc. You may also have a hard data cap that, while high,
still exists in the terms.

They will loan you a proprietary modem/router combo that may or may not let you
throw it in bridge mode. This is less than ideal, but certainly a less shitty
option if you just need to get going. And it will most likely still work in bad
weather.

### Option 5: Tethered Phome
If you don't want to pay out the ass, or don't have any other good options
where you live, you can use a tethered phone. And if you roll your own router
as detailed in the next guide it will accommodate this nicely. Tethering to
Androids is natively supported by the Linux kernel, and iPhones work pretty
well once you install `libimobiledevice` and `usbmuxd`.

### Option 6: LTE/5G Modem
It is possible to get a data line on a sim card, put this into an internal or
external modem installed in your DIY router, and use that. There are some out
there that will work natively on Linux. The drawbacks are that these do not
work very seamlessly without a full desktop environment running. Configuring
them is also kind of a pain in the ass, and may require unmaintained software
to switch modes and such. To flip mine from QMI to MBIM mode, I had to boot up
Ubuntu 14.04 in a VM.

I don't cover these as they are painful to use and I honestly forgot how to
anyway. You will have to scour the web like I did, sorry.

#### Picking a Carrier
So you went with option 5 because it's the least deleterious to your wallet or
your sanity. Now it all comes down to your choices of carrier and plan. You may
or may not want to shop for a new carrier, for you or for a dedicated tethering
device if you have one. You want three things out of it:
1. A strong, consistent signal
2. No hard data cap
3. Unlimited tethering, even if speed-limited

That last part is **extremely** important and you need to be sure before you
buy. Speed caps are easy enough to work around (and that's covered later), but
you don't want to be kicked off the network for abuse when you rack up hundreds
of GB of data usage.

Carriers that offer unlimited tethering are also likely to be VPN-friendly, as
WFH customers often rely on them to access company resources.

#### Rooted Androids Are Your Friend
If you can't get a plan that legitimately allows tethering, you will almost
100% need an Android capable of running a custom ROM. iOS and lots of stock
Androids will bend right over, spread their cheeks and disable your native
tethering function if the carrier asks them to with OTA provisioning.

The process of unlocking a bootloader and flashing a ROM varies by device.
Google it.

[Next: DIY Router](/guides/rural-networking/2-diy-router.html)

### Comments
