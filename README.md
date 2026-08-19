# Beacon KVM on a Raspberry Pi

[Beacon](https://www.beacon-kvm.com) is an IP KVM: the screen, keyboard and
mouse of any computer, in a browser, at BIOS level. Nothing is installed on the
machine you control.

This repository is the trial build for a **Raspberry Pi 4B** — the same
software, on a board you already own — and where to report problems with it.

> **This is a trial.** Remote access on a Pi is not something we make any
> promises about. On your own network it is fine. The console labels these
> devices *Raspberry Pi (trial)*.

## The hardware version

A Beacon device is the same software on a board built for it: assembled, with
the capture card fitted and the cables in the box, and remote access we do
stand behind.

[beacon-kvm.com](https://www.beacon-kvm.com)

## What you need

| | |
|---|---|
| **Raspberry Pi 4B** | Not a Pi 5 |
| **A USB HDMI capture card** | 1080p, UVC. Goes in a **blue** USB 3 socket |
| **A USB-C data cable** | Pi to the machine you control |
| **A network cable** | Or 5 GHz Wi-Fi |
| **A 5.1 V 3 A supply for the GPIO header** | Not the USB-C port |
| **64-bit Raspberry Pi OS** | Bookworm |

## Install

Power the Pi from the GPIO header: 5 V to pin 4, ground to pin 6. Leave the
USB-C port free.

> ⚠️ **Check the polarity first.** Measure the supply: red to pin 4, black to
> pin 6. Reversed, it destroys the board.

Then:

```bash
curl -LO https://github.com/BeaconBeacon/KVM/releases/latest/download/beacon-pi.tar.gz
tar xzf beacon-pi.tar.gz
cd beacon-pi
sudo ./install.sh
```

Power off, pull the plug, plug it back in:

```bash
sudo poweroff
```

Connect four cables, each starting at the Pi:

| Cable | On the Pi | At the other end |
|---|---|---|
| **HDMI** | The capture card | The machine's video output |
| **USB-C** | The USB-C port | Any USB socket on that same machine |
| **Ethernet** | The Ethernet socket | Your router or switch |
| **Power** | GPIO pins 4 and 6 | A 5.1 V 3 A supply |

The installer prints a serial and a link:

```
Serial : BCN-PI-XXXXXXXXXXXX
Bind it: https://beacon-kvm.com/b/BCN-PI-XXXXXXXXXXXX
```

Open the link, sign in, click **Add to my account**.

Full instructions: <https://doc.beacon-kvm.com/raspberry-pi.html>

## What is in the package

The `beacon-kvm` binary, built for arm64, and these scripts. Read them before
running them.

| | |
|---|---|
| `install.sh` | Installs the binary, the services and the config |
| `setup-hid-gadget-pi.sh` | Makes the USB-C port a keyboard and mouse |
| `hid-selftest.sh` | Types and moves the pointer, to prove HID works |
| `beacon-kvm-pi.service` | The client |
| `beacon-hid-pi.service` | Runs the gadget script at boot, and retries |

## If something is wrong

```bash
sudo journalctl -u beacon-kvm-pi -n 50 --no-pager
```

| What you see | What to do |
|---|---|
| Black screen, session connected | Move the HDMI cable to the capture card. The Pi's own HDMI socket is an output |
| Around 10fps | Move the capture card to a blue USB 3 socket |
| `no USB device controller` | Put `dtoverlay=dwc2,dr_mode=peripheral` under `[all]` in `/boot/firmware/config.txt`, then power off and on |
| Keyboard or mouse does nothing | Run `sudo hid-selftest.sh` |
| LAN KVM jumping between 60 and 20fps | Use a cable, or 5 GHz Wi-Fi |
| Random reboots | Power the Pi from the GPIO header, not from the target's USB port |

## Report a problem

[Open an issue](https://github.com/BeaconBeacon/KVM/issues/new/choose). Include
the output of:

```bash
sudo journalctl -u beacon-kvm-pi -n 100 --no-pager
```

Questions that are not bugs: <support@beacon-kvm.com>

## Links

| | |
|---|---|
| Website | <https://www.beacon-kvm.com> |
| Docs | <https://doc.beacon-kvm.com> |
| Console | <https://console.beacon-kvm.com> |
