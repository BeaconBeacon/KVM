# How to access a computer's BIOS remotely

*Every remote access tool you already have runs inside the operating system. The BIOS runs before there is an operating system — which is why none of them can get you there.*

## Why remote desktop can't do it

RDP, VNC, TeamViewer, AnyDesk and SSH are all programs. They start after the
operating system starts, and they send you a picture that the operating system
draws.

Press Delete or F2 during boot and none of that exists yet. There is no
network stack, no service to accept your connection, and nothing running that
could send an image anywhere. The machine is drawing to its HDMI output and
listening to a USB keyboard, and that is all it is doing.

So the only way in is to be that monitor and that keyboard.

## What an IP KVM does instead

An IP KVM is a small piece of hardware that sits between you and the machine:

1. It takes the machine's HDMI output and encodes that video.
2. It plugs into a USB port and pretends to be a keyboard and a mouse.
3. It streams the video to your browser and sends your keystrokes back.

The machine cannot tell the difference. To it, a monitor is plugged in and
somebody is typing. It does not know the keyboard is three thousand kilometres
away, and it needs no software, no driver and no configuration to make this
work.

Because none of it depends on the operating system, it keeps working in the
BIOS, in a bootloader, at a Windows recovery screen, and while the machine is
restarting.

## Getting into the BIOS, step by step

1. Connect to the machine in your browser.
2. Restart it — from inside the OS, or with the physical power button if
   somebody is there.
3. Hold Delete or F2 as it comes back up, exactly as you would locally. The
   key goes over the same USB connection a real keyboard would use.
4. The POST screen and then the BIOS appear in the browser window.

The keys that matter are the ones sent early, so start holding the key before
the screen lights up rather than after.

## What you can do once you are in there

- Change the boot order
- Turn virtualisation extensions on
- Enable or disable Secure Boot
- Set or clear a supervisor password
- Read the machine's temperatures and fan behaviour
- Recover a machine that boots to the wrong disk

## What it still cannot do

Be honest with yourself about the limits before you buy anything.

### Can an IP KVM turn a machine on that is fully powered off?

Not by itself. It gives you the screen and the keyboard, not the power
button. If the machine is off, pair the KVM with a smart plug, or with the
motherboard's own Wake-on-LAN if that is enabled in its BIOS.

### Can I reinstall an operating system through it?

You can drive an installer that is already booting, because that is just a
screen and a keyboard. Getting the installer onto the machine in the first
place needs either an image already on a disk, or a device that can emulate a
USB drive. Beacon does not emulate a USB drive today.

### Does the machine need a network connection?

No. The KVM has its own network connection. The machine being controlled
can have no network at all — that is often exactly why you are connecting.

### Does it work with a laptop?

Only if the laptop can output video over HDMI while its lid is open or its
internal display is off, which most can. The KVM sees whatever the HDMI port
sends.

## Server hardware sometimes has this built in

If you are working with rack servers, check for IPMI, iDRAC, iLO or an
equivalent baseboard controller before buying anything. Those are IP KVMs
built into the motherboard, and they are excellent.

Desktops, mini PCs, workstations and consumer motherboards almost never have
one. That is the gap an external IP KVM fills.

---

Originally published at [beacon-kvm.com](https://beacon-kvm.com/blogs/use-cases/access-bios-remotely) · [All articles](README.md) · [Build your own on a Raspberry Pi](../README.md)
