## Elden Guides - Use a VPN
If you're using any cellular connection, whether your usage is technically
allowed or not, you should get a VPN. Cell carriers have always been the worst
enemies of net neutrality, and short of paying them piles of money, that's
about all you can do to get it back. They *especially* love to throttle the
shit out of video streams to keep the resolution low, so they can sell those
pixels back to you as an addon.

### Avoid Shitty VPNs
Just go with Mullvad or Proton. Mullvad is like $5 and has multiple servers in
each city. Most of the VPNs you see ads for are massively overpriced, and lots
only have one server per city.

### 1. OpenVPN vs WireGuard
Lots of providers will give you a choice between several protocols. Lots of
them are pieces of shit only supported OOB by Windows for corporate VPNs. The
two in the section title, OpenVPN and WireGuard, are the only two that matter.
Which one you should choose depends on what kind of hardware you have.

#### WireGuard
WireGuard is a newer, peer-to-peer VPN protocol. It runs as a kernel module (on
Linux at least), supports multithreading, and uses crypto ciphers that are
meant to be efficient on machines without hardware acceleration. It also uses
a lower MTU, which may cause you some outbound packet fragmentation, but
probably not enough to matter.

Package: `wireguard-tools`

#### OpenVPN
OpenVPN is the older of the two and runs as a process in userspace. It supports
a few different crypto ciphers, with AES often being supported in hardware by
lots of Intel/AMD CPUs made after about 2010. Check the flags in
`/proc/cpuinfo` to see if your CPU supports this.

In my experience it can be quite a bit faster, more reliable, and more
responsive than WireGuard, especially on the right hardware and with realtime
priority.

Package: `openvpn` or `openvpn-client`

### 2. Realtime Priority (Optional)
If you use OpenVPN (and especially if you have hardware crypto) this will help
you tremendously. Your VPN process will preempt absolutely everything else on
the computer and handle that layer with as close to zero delay as it can.
1. Install an `rt` kernel from your distro repositories and boot into it
2. Run `chrt -d -p $(pidof openvpn)`

### 3. VPN Configuration
Copy your VPN config to the appropriate directory. That will be
`/etc/openvpn/client` or `/etc/wireguard`. You will then want to to enable the
service with `systemctl enable <vpn-service>@<config>`.

Open your firewall rules and add a rule for your VPN interface, in the `nat`
table, above your other interfaces. If you have a static, public IP, you will
want to use a source NAT rule:
```
-A POSTROUTING -s 10.0.0.0/24 -o <vpn_if> -j SNAT --to-source <ip>
```
Otherwise, if you receive a private address or you are at all unsure, use a
masquerade rule:
```
-A POSTROUTING -s 10.0.0.0/24 -o <vpn_if> -j MASQUERADE
```

You will then want to install and configure `miniupnpd` if you game, and have a
public address. It's pretty easy, and because we predefined the `MINIUPNPD`
chains in your iptables rules earlier it should just work.

### 4. Secure Your Shit
You should probably go and disable password auth in your SSHd config and use
a key. And make sure things like Samba aren't being exposed. Unless you paid
extra for a public IP, you have CGNAT hiding you from the public internet, but
it's still best to not blindly trust that no bad actors can ping you.

Also, this isn't a Walmart router. You get updates and logfiles, and should
shell back in periodically to check on things and update.

[Previous: Tethering Considerations](/guides/rural-networking/3-tethering.html)

### Comments
