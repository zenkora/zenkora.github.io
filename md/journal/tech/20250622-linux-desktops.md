## Zenkora's Dark Moon - (2025.06.22) Best and Worst Linux Desktop Environments
In 2010, when I started using Linux, it had a *fuck ton* of options for desktop
environments and window managers. There were a million offshoot distros for
every conceivable setup. And most of them sucked balls and/or had no reason to
exist.

In 2025, Linux still has a *fuck ton* of options, and a million offshoot
distros with no legitimate reason to exist. And most of them kinda suck balls.
I'm not covering all the weird bespoke bullshit out there, mostly the DEs
you'll find in a mainstream distro's repositories.

### KDE Plasma
**Pros:** full Wayland support, no missing features, plenty of themes</br>
**Cons:** Not for toaster PCs </br>
**Rating:** 9.5/10

A decade ago, KDE was pretty but a little buggy. Now it's pretty and fully
functional. Since Plasma 5 it's been pretty much perfect out of the box; a
premium-looking blend of Apple's frosted-flat look and the familiar start
menu/taskbar layout; but you *can* switch it up however you want, and there are
plenty of nice themes, window decorations, etc easily accessible from its
included KDE store frontends. Just make sure you find the matching GTK theme to
go with it so everything is consistent.

Valve ships it on Steam Decks for a reason. Or probably dozens. Whatever, the
point is that KDE is great and I stan for it here.

![kde](/img/linux-desktops/kde.png)

### Sway/i3
**Pros:** extremely lightweight, minimalist, Wayland support (sway)</br>
**Cons:** not user-friendly at first </br>
**Rating:** 8/10

Sway, and its older Xorg-based cousin i3, are very fast and very light tiling
window managers, and share the same config syntax. They're not for everyone and
they do absolutely no hand-holding. But if you're willing to do a fair amount
of reading, and configure everything by hand, you can have a *very* intuitive,
personalized workspace that hardly requires you to reach for your mouse, and
uses next to no resources for itself.

Neither really pull a lot of dependencies besides X/Wayland themselves, so you
have the choice of preferring either GTK or Qt-based apps if you're trying to
keep your installation small.

If you'd like a simpler manual and included batteries, you're welcome to clone
[this repo](https://github.com/zenkora/sway_quickstart). It has everything you
need to get going in about thirty seconds post-install and then customize it
further yourself.

![sway](/img/linux-desktops/sway.png)

### MATE
**Pros:** lightweight, user-friendly, supports Wayland </br>
**Cons:** feels a little dated </br>
**Rating:** 8/10

MATE is a solid, conservative choice, whether your PC isn't bougie enough for
KDE or you want to maximize available resources on a more powerful machine. Or
maybe you just prefer GTK. It's basically Gnome 2 kept fresh in the modern age,
and it supports Wayland.

![mate](/img/linux-desktops/mate.png)

### XFCE
**Pros:** lightweight, themeable, configurable </br>
**Cons:** 2003 looking shit </br>
**Rating:** 5/10

If you have a shit PC, XFCE will be relatively nice to it. You can get it to
look decent
with a little effort and it won't eat all of your RAM.

![xfce](/img/linux-desktops/xfce.png)

### LXQt
**Pros:** same as LXDE below </br>
**Cons:** same as LXDE + a little harder to theme, slightly higher memory use </br>
**Rating:** 4/10

Imagine KDE, but its devs are all stuck with Intel Atom netbooks from 2010. You
get LXQt. It's like a slightly nicer cousin of LXDE, and as made obvious by the
name, it uses Qt instead of GTK.

![lxqt](/img/linux-desktops/lxqt.png)

### LXDE
**Pros:** lightweight, minimalist </br>
**Cons:** Y2K looking shit </br>
**Rating:** 3.5/10

If you have a *really* shit PC, LXDE might be your last option before resorting
to text-based programs on a TTY. You *can* theme it, kinda. But it looks like
shit without tons of effort and trial-and-error, and Openbox is really bare
bones shit.

![lxde](/img/linux-desktops/lxde.png)

### Gnome
**Pros:** supports Wayland I guess </br>
**Cons:** absurd VRAM usage, broken themes, intentionally missing features </br>
**Rating:** fucking garbage/10

Gnome is a steaming pile of shit with antiuser developers. I don't know why
it's so popular, or why it's shipped on the biggest distros. If you leave
everything default, and pretend to be retarded, it works okay I guess. But you
wanna theme it? Have fun finding one that still works, plus a matching shell
theme. Do you have tons of VRAM for your heaviest games? Not anymore you don't.
Accidentally closed your Steam or Discord window? Well, the neckbeard devs
don't believe in tray icons, so you can go fuck yourself. Oh, but here's a
stupid ass "Boxes" app and the KVM dependencies with it, because you *totally*
weren't gonna use VBox or VMware, were you?

![gnome](/img/linux-desktops/gnome.png)
