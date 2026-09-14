# IP KVM vs remote desktop: when you need hardware

*These two things look similar in a browser window and are not remotely the same underneath. The difference only shows up on the day something breaks.*

## The one difference everything else follows from

Remote desktop software is a program running on the machine you are
controlling. An IP KVM is hardware plugged into that machine, pretending to be
a monitor and a keyboard.

So the question is never "which gives a nicer picture". It is: **when the
operating system is not running, is your remote access still there?**

| | Remote desktop | IP KVM |
|---|---|---|
| Installed on the target | Yes, an agent | Nothing |
| Works before the OS loads | No | Yes |
| BIOS and UEFI setup | No | Yes |
| Bootloader, recovery, safe mode | No | Yes |
| After a failed OS update | No | Yes |
| Machine with no network of its own | No | Yes |
| Copy and paste, file transfer | Yes | No |
| Multiple monitors | Yes | One HDMI output |
| Cost per machine | Often free | Hardware per machine |
| Picture quality for daily work | Better | Good enough |

## Use remote desktop when

- The machine is healthy and you are doing ordinary work on it
- You need to move files, share a clipboard, or print locally
- You are supporting a person who is sitting at the machine
- You have many machines and cannot put hardware on each

For day-to-day work, remote desktop is better and it is usually free. Nobody
should buy hardware to avoid installing RDP.

## Use an IP KVM when

- The machine is far enough away that a trip costs a morning
- It sometimes fails to boot, and you cannot predict when
- You need the BIOS: boot order, virtualisation, Secure Boot
- The machine has no network of its own, or its network is what you are fixing
- You are installing or reconfiguring the operating system itself
- Somebody else's network is involved and you cannot install anything on it

## The honest answer is usually both

Most people who own an IP KVM use remote desktop every day and the KVM twice a
year. That is the correct ratio, and it is not an argument against the KVM —
insurance you use constantly is not insurance.

The way to decide is to price one trip. If driving to the machine costs a
morning of your time, the hardware pays for itself the first time the machine
sits at a GRUB prompt.

## Common questions

### Can't I just use Wake-on-LAN and a scheduled task?

Those help with a machine that is off or that needs a routine job run. They
do not help with a machine that is on and stuck, which is the case that
actually strands you.

### What about IPMI, iDRAC or iLO?

Same idea, built into the motherboard, and if your machines have one you
should use it. Desktops, mini PCs, workstations and consumer motherboards
almost never do. That is the gap an external IP KVM fills.

### Does an IP KVM replace a VPN?

It depends on the KVM. Some need a port opened or a VPN to reach them.
Beacon makes an outbound connection and relays the session, so it works behind
CGNAT and needs nothing opened on your router.

### Will the machine know something is plugged into it?

It sees a monitor and a USB keyboard and mouse. It cannot tell them apart
from real ones, and nothing is installed on it.

---

Originally published at [beacon-kvm.com](https://beacon-kvm.com/blogs/use-cases/ip-kvm-vs-remote-desktop) · [All articles](README.md) · [Build your own on a Raspberry Pi](../README.md)
