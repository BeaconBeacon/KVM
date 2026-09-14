# A remote machine won't boot. Now what?

*The moment a machine stops booting is the moment every tool you use to reach it stops working. That is not a coincidence — they all live inside the thing that just failed.*

## First, work out which kind of dead it is

You cannot fix what you cannot see, but you can usually narrow it down by what
still responds.

| Symptom | What is probably true | Reachable remotely? |
|---|---|---|
| Pings, no SSH | OS is up, service or disk problem | Yes, with a KVM |
| No ping, fans spinning | Stuck in POST, bootloader, or filesystem check | Only with a KVM |
| No ping, no fans | Power supply, or the machine is off | No. Somebody has to go |
| Boots, then reboots | Overheating, bad update, failing disk | Yes, with a KVM |

The second and fourth rows are where most of the wasted trips happen. The
machine is fine — it is sitting at a prompt nobody can read.

## What a screen would tell you

Almost every non-booting machine is showing something on its HDMI output right
now:

- A GRUB menu waiting for a selection
- `No bootable device found`, because a USB stick was left plugged in
- A filesystem check that stopped and wants a root password
- A Windows recovery screen with a button to press
- A BIOS asking about a changed boot device
- A kernel panic with the line that caused it

Every one of those is fixed by looking at a screen and pressing a few keys.
None of them can be fixed over SSH, because SSH is not running.

## Reading that screen from where you are

An IP KVM captures the machine's HDMI output and emulates a USB keyboard and
mouse, so you get the screen and the keyboard in your browser. It is separate
hardware with its own network connection, so it does not care that the machine
it is watching has failed.

That covers:

1. Watching the whole boot, from POST onward
2. Choosing a different kernel or an older snapshot in the bootloader
3. Typing the root password at an emergency shell
4. Entering the BIOS to fix a boot order somebody changed
5. Seeing the panic message so you know what to prepare before anyone drives
   out there

Even when the answer turns out to be "this needs hands", knowing that in two
minutes rather than after a two-hour drive changes how the day goes — and you
arrive knowing which part to bring.

## What still needs somebody on site

### The machine is completely powered off. Can I turn it on?

Not with a KVM alone — it replaces the monitor and keyboard, not the power
button. A smart plug that cuts and restores mains power will usually cause a
machine to start if its BIOS is set to power on after a power loss. Set that
option while you are still standing in front of it.

### Nothing appears on screen at all, even at POST.

That is a hardware fault before the video output — power supply, RAM, CPU
or motherboard. No remote tool can help. The KVM is still useful here: it
proves the machine is producing no video, which rules out a whole class of
software causes before anyone travels.

### The disk is dead and it needs a fresh install.

You can drive an installer once it is running, but getting installation
media onto the machine needs either an image already on another disk or a
device that emulates a USB drive. Beacon does not emulate a USB drive today.

## Set this up before you need it

The uncomfortable part of remote recovery is that it has to be in place
already. Once the machine is down, it is too late to install anything on it —
which is exactly why the hardware sits outside it.

A KVM that has been plugged in for six months and never used is not waste. It
is the thing that turns one specific bad day into fifteen minutes.

---

Originally published at [beacon-kvm.com](https://beacon-kvm.com/blogs/use-cases/server-wont-boot-remote) · [All articles](README.md) · [Build your own on a Raspberry Pi](../README.md)
