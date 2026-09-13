# Why you need an IP KVM

*Every remote tool you have runs inside the operating system. The day you need one most is the day the operating system isn't there.*

## Why you need an IP KVM

You changed a network setting. The moment you pressed return you knew — the SSH
session did not disconnect, it froze. Reconnect: timeout. The machine is fine.
It is powered on, and it still answers ping. It just does not recognise you any
more. The line you need to put back is one line long, and it is forty
kilometres away.

It comes in other shapes. A machine reboots after a kernel update and stops on
a screen you cannot see. A client calls at two in the morning to say it will
not come on, and the thing you would connect to is the thing that has not
started.

Every remote tool you have makes the same three assumptions:

- the operating system has booted
- the network is configured and reachable
- its own service is running and accepting connections

SSH, RDP, VNC, TeamViewer, AnyDesk — all of them. Break one and you lose
access, and the day you most want access is the day one of them breaks. They
are programs, and a program needs something to run on. What you need is
something that does not run on the machine at all.

[The full comparison, tool by tool →](https://beacon-kvm.com/blogs/use-cases/ip-kvm-vs-remote-desktop)

## What an IP KVM is

An IP KVM is a fake monitor and a fake keyboard.

That is the whole idea. One cable goes into the machine's HDMI output, so the
device sees the picture the monitor would have shown. Another goes into a USB
port, and through it the device pretends to be a keyboard and mouse plugged
into the front of the case. Everything it captures and everything you type
travels over its own network connection — the IP in the name.

![To the machine it is a monitor and a keyboard, so it sees the BIOS too](https://cdn.shopify.com/s/files/1/0731/0557/1882/files/uc-device-bios.jpg?v=1789266408)

From the machine's point of view nothing unusual is attached. A screen, a
keyboard. It does not know they are being carried over a network, and it does
not need to. Which is why this reaches places software cannot:

- **Nothing is installed.** No agent, no service, no port to open, no account
  on the machine. There is nothing on it that can fail to start.
- **The operating system is irrelevant.** Linux, Windows, a BSD, a bootloader,
  a BIOS setup screen, a kernel panic — if it puts pixels on a screen, you see
  them. If it reads a keyboard, you can type at it.
- **The machine's network does not have to work.** The IP KVM has its own
  connection. The machine can be off the network entirely and you still see it.

Compare that with the three assumptions above. An IP KVM needs none of them.

## How an IP KVM solves it

Take the network setting you broke. Here is the same failure with an IP KVM
attached — a Beacon device, in this case, but the shape is the same whichever
one you use.

You open a browser and sign in. Every machine you have is listed, and you pick
the one that stopped answering.

![Every machine on your account, in one list](https://cdn.shopify.com/s/files/1/0731/0557/1882/files/uc-devices.png?v=1789266179)

The picture comes up. Not a remote desktop session — the actual screen output,
whatever is on it right now. In this case a login prompt, sitting there, fine,
waiting, on a machine that has been unreachable for ten minutes.

You log in. Not over the network: your keystrokes arrive over USB, exactly as
if you were standing at the machine with a keyboard in your hands. You edit the
interface config, put back the line you broke, bring the interface up. SSH
starts answering again. About two minutes, none of it spent driving.

The other two failures work the same way. Stopped at a boot menu: you see the
menu and you press the key. Will not power on: you see whether it posts at all,
which tells you whether this is a five-minute BIOS problem or a genuinely dead
power supply — and knowing which one before you get in the car is most of the
value.

## Common questions

### Does it work if the machine is completely switched off?

You will see that it is off, which is already more than you knew before.
Typing at it does nothing until it powers on, because a keyboard needs
something to type at. Getting it to power on is a separate wire: an IP KVM
that supports ATX control connects to the front-panel header and presses the
power button for you.

### What about IPMI, iDRAC or iLO?

Same idea, built into the motherboard, and if your machines have one you
should use it. It is a server feature. Desktops, mini PCs, workstations,
consumer motherboards and most homelab hardware do not have it, and an IP KVM
is how you add it to a machine that shipped without it.

### Do I need to open a port or run a VPN to reach it?

It depends on the device. Some listen on a port and expect you to forward
it or come in over a VPN. Beacon makes an outbound connection to a relay, so
it works behind NAT and needs nothing opened on the router at the far end.

### Can I get into the BIOS with it?

Yes, and this is the usual reason people buy one. The BIOS runs before any
operating system, so no software on the machine can show it to you. An IP KVM
sees it because it is reading the video output, the same as the monitor would.

## Where to start

Two ways in. The same software also runs on a Raspberry Pi 4B with a capture
card you supply yourself, and running it there is free, so you can have a
working IP KVM for the cost of the parts and an afternoon of assembly. Or you
can buy the device we make: the same software, on hardware that arrives
assembled, with remote access already working and no monthly fee attached
to it.

[How Beacon KVM compares with PiKVM, JetKVM and TinyPilot →](https://beacon-kvm.com/blogs/use-cases/ip-kvm-comparison)

---

Originally published at [beacon-kvm.com](https://beacon-kvm.com/blogs/use-cases/why-you-need-an-ip-kvm) · [Build your own on a Raspberry Pi](../README.md)
