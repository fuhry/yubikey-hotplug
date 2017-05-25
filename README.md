# `yubikey-hotplug`: Automatic screen lock/unlock for Yubikeys

This is a small script that allows the running desktop environment's screensaver to be locked/unlocked based on hotplug events of a Yubikey. It has the following features:

* Fast and responsive, triggered via a udev hook
* Confined to specific Yubikey serial numbers per-user
* No root access required for configuration
* Secure - workstation cannot be unlocked with a yubikey if it was unplugged while the PC was locked

## Dependencies

This utility depends on `yubikey-manager` which is available in the Arch Linux `community` repository.

## Setup

To configure `yubikey-hotplug`, all you need to do is write your Yubikey's serial number to a file in your home directory:

```
mkdir -p ~/.config/yubikey-hotplug
echo 1234567 > ~/.config/yubikey-hotplug/serials
```

If you don't know your Yubikey's serial number, use `ykman info` to get it. If `ykman` can't figure out what it is then this program will not work, as it uses `ykman` to query the Yubikey's serial number. Note that some very old Yubikeys do not have serial numbers.

## Security

Unlike other attributes, the serial number is completely burned into the Yubikey and no two will ever be the same. It is theoretically possible to make a fake device with the same hwid and API as a Yubikey. There is no challenge-response or other secret key based authentication that occurs when the system verifies the Yubikey's serial number. So keep this in mind, this utility is a convenience aid and not a replacement for proper workstation security.

The utility will check if the screensaver is locked when a Yubikey is unplugged. If it is, it will create a flag file (`~/.config/yubikey-hotplug/require-unlocked-plugin`) which signals that plugging the Yubikey back in should not unlock the workstation. The use case for this is perhaps you left your workstation unattended and forgot to take your Yubikey with you - this protects you from an attacker unplugging your Yubikey and immediately plugging it back in. **If you unplug your Yubikey while your workstation is locked, you must unlock it and then reconnect the Yubikey to automatically delete the flag file.**

## Limitations

The utility currently works only on MATE, an issue will be opened to track progress on support for other desktop environments.

## Author/License

Written by Dan Fuhry <dan@fuhry.com>.

MIT licensed; please see the [COPYING file](COPYING).
