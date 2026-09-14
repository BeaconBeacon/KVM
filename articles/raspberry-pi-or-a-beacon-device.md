# A Raspberry Pi KVM, or a Beacon device

*Two ways to have a Beacon KVM, and the software is the same in both. What differs is everything the hardware decides.*

## Two ways to have one

**The Raspberry Pi build** is our software on a Raspberry Pi 4B you supply and
assemble yourself. It is free, and it is the whole software, not a cut-down
version.

**A Beacon Device** is the KVM hardware we make and sell: the same software on
a board built for it, assembled, with the capture card fitted and the cables in
the box.

Where they differ:

## It works the moment you plug it in

No board to source, no capture card to choose, no socket to get right, no
operating system to write to a card, no wiring to a GPIO header, no multimeter.

A Beacon device arrives assembled, with the capture card already in the correct
socket and the cables in the box. Four cables, scan the code on the label, and
it is on your account. Nothing on the way there asks you to know Linux, and
nothing on the way there can be wired backwards.

Building one on a Pi asks more of you. You choose the parts. You power the
board from its GPIO header, because its USB-C port is busy being the keyboard.
And you check the polarity before you connect it, because reversed it destroys
the board. That is a fair trade if you enjoy this sort of thing — and a poor
one if you were hoping to be finished before dinner.

## The picture is better

The device is built around a video processor chosen for this job, and it is
tuned for what a KVM screen actually is: mostly still, with text that has to
stay readable.

In use that means a higher frame rate, a sharper picture, a pointer that keeps
up with your hand, and less bandwidth for the same result. A Raspberry Pi does
all of it, just not as well, and it needs considerably more bandwidth to get
close.

On your own network you may not notice. Tethered to a phone in a car park, or
sharing an uplink with an office, it is the difference between working and
waiting.

## Somebody answers

A device is ours. A fault in it is ours to find, and we can change its firmware
to fix it. That is part of what the price buys.

The Pi build runs on a board we did not make, with a capture card we did not
choose, on a network we cannot see. We help where we can, and remote access on
a Pi is explicitly not something we promise.

## What is the same

Everything else, and that is deliberate:

- The same software, not a cut-down version
- Firmware setup, boot menus and recovery screens — it works below the
  operating system either way
- LAN and remote access, with nothing opened on your router
- Sharing a machine by link, full control or view only
- SSH in the browser
- The same console and the same account, with a Pi and a device side by side

Which means trying the Pi first is never wasted. Nothing has to be moved,
re-learned or re-bound if you buy a device afterwards.

## Common questions

### Is the Raspberry Pi version limited on purpose?

No. Every feature is there, and the console treats it as an ordinary device.
The differences come from the board: an older video encoder, a lower frame rate
ceiling, and more bandwidth for the same picture.

### What does building one actually cost?

A Pi 4B, a 1080p USB capture card, a card for the operating system, and a
5.1 V supply with a lead to the GPIO header. Prices move, but it lands under
half the price of a device — and the difference is an evening of your time.

### Will a Raspberry Pi 5 work?

No. The 5 has no hardware H.264 encoder at all. A 4B is the one to use.

### Can I move from a Pi to a device later?

Yes. Add the device to the same account and it appears next to the Pi. Both
can stay if you want them to.

### Is remote access on a Pi usable?

On a good connection, yes, and it is what most people try first. It is not
something we promise, because the bandwidth it needs depends on a board we did
not build and a network we cannot see.

---

Originally published at [beacon-kvm.com](https://beacon-kvm.com/blogs/use-cases/raspberry-pi-or-a-beacon-device) · [All articles](README.md) · [Build your own on a Raspberry Pi](../README.md)
