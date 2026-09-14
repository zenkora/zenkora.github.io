## Elden Journal - (2024.03.14) Review: VPSDime

### The Beginning
About four months ago, I decided to start up a Windows VPS with these guys on
quarterly billing. $60 for three months with four nice Xeon vcores, 8GB of RAM
and 100GB of SSD space. Plenty enough for my needs, though enough shit was
explicitly banned or heavily restricted by the ToS that there wasn't much left
I was even allowed do with that shit besides my web and email. It didn't say
anything about my BeamNG server, but at this point I hope it was bannable and
they're extremely pissed about it.

The first sign of something fucky was when I started lusrmgr.msc and went to
make myself a user. The provider had an account with admin privileges baked
into their image. Well, I'm not doing anything unethical with my server, but I
don't want a backdoor like that in one I'm paying for. Deleted that shit and
continued on learning to admin a Windows server and setting it up.

### The Fuckening
This VPS dutifully ran my website, email, primary DNS, and BeamNG servers for
the aforementioned four months. And then sometime in the last few days that I
haven't checked on it shit went WAY south.

I fired up my new MBA, downloaded Microsoft's RDP app, and tried to log in with
my user to check up on it and run the updates. Got kicked off because the
account was locked. Huh, weird. So I tried to log in as the admin user, which
I'm pretty fucking sure I disabled. Instead of an invalid credentials error I
got the same message: the account is locked because someone tried to log into
it too many times. *Really* weird. So I headed onto the provider's client site,
hoping to use a web VNC client. They apparently replaced that with a useless
emergency console at some point, in the time that I haven't needed to visit
this site. Whatever. I clicked it and was greeted with the Windows login
screen. And **sure as fuck** the administrator account was *somehow* re-enabled
along with *two* auto-named accounts starting with "VPSDIME-". And this console
didn't seem to support keyboard input, so with that and no way to RDP in I
considered it dead. I will not be renewing that bullshit. I don't know if it
would have worked in another browser, but at this point I didn't care. These
motherfuckers went apeshit on my server and locked every account before
apparently using their host powers to get in anyway, because I didn't want them
just casually logging into my shit.

### The Verdict
Go with VPSDime if you want a provider who apparently wants to snoop through
your shit and will use the software equivalent of a battering ram to do it. If
you don't, because you're a dissident journalist or just someone who values
what shreds of privacy remain in this world, use literally any other provider.
I have never had anything like this happen to me before.
