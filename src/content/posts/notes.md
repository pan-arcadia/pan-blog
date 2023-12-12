---
title: 'Notes'
pubDate: 2023-12-12 10:00:00.0 -7
description: 'My daily notes.'
author: 'JH'
tags: ['notes', 'linux']
---

## How to use Vim with the system clipboard

The version of vim that came with Ubuntu 22.04 did not have access to the system clipboard.

We can see if Vim has system clipboard support by running the following command:

```shell
vim --version | grep clipboard
```

If we see `+clipboard` or `+xterm_clipboard`, then system clipboard support is enabled.

If not we can install `vim-gtk`:

```shell
sudp apt install vim-gtk3
```

Note: I've seen `vim-gtk` and `vim-gtk3`. Not sure what the difference is. I installed `vim-gtk3` and it had the system clipboard enabled.

Now that we have the system clipboard enabled, we can paste some text. Put Vim into INSERT mode. Paste from the clipboard with `Shift + Insert` or `Ctrl + Shift + V`.

### Reference

[How do I install vim-gnome on Ubuntu 19.10?](https://askubuntu.com/questions/1208159/how-do-i-install-vim-gnome-on-ubuntu-19-10) 

[How to Paste Clipboard Text in Vim](https://codingissimple.com/how-to-paste-clipboard-text-in-vim/)

## How to Manage Bluetooth Devices on Linux Using bluetoothctl

Bluetoothctl is an interactive and easy-to-use tool for controlling Bluetooth devices. It is the main utility for managing Bluetooth on Linux-based operating systems.

> Mwiza Kumwenda

### Checking Bluetooth Status

```shell
sudo systemctl status bluetooth
```

If the Bluetooth service is not active, we can enable it:

```shell
sudo systemctl enable bluetooth
sudo systemctl start bluetooth
```

### Scanning for Nearby Devices

```shell
bluetoothctl scan on
```

### Connecting to Your Device

We use the MAC address of the device we want to connect with. The address that was displayed using the `bluetoothctl scan on` command.

We can pair with our device:

```shell
bluetoothctl pair 2C:41:A1:28:7D:3F
```

We can connect with our device:

```shell
bluetoothctl connect 2C:41:A1:28:7D:3F
```

### Listing our Paired Devices

We can see a list of devices already paired with our system:

```shell
bluetoothctl paired-devices
```

We can also list devices that are withing Bluetooth range of our machine:

```shell
bluetoothctl devices
```

### Trusting Paired Devices

Trusting a device allows us to easily connect with them in the future:

```shell
bluetoothctl trust 2C:41:A1:28:7D:3F
```

We can also untrust a device:

```shell
bluetoothctl untrust 2C:41:A1:28:7D:3F
```

### Disconnecting Bluetooth Devices

We can unpair a Bluetooth device:

```shell
bluetoothctl remove 2C:41:A1:28:7D:3F
```

We can disconnect from a device:

```shell
bluetoothctl disconnect 2C:41:A1:28:7D:3F
```

We can also block a specific device from connecting to our machine:

```shell
bluetoothctl block 2C:41:A1:28:7D:3F
```

And we can unblock a device:

```shell
bluetoothctl unblock 2C:41:A1:28:7D:3F
```

### Using the Interactive Mode

We can use the interactive utility to enter all the above commands.

```shell
bluetoothctl
```

To exit the interactive mode, type the `exit` command.

### Reference

[# How to Manage Bluetooth Devices on Linux Using bluetoothctl]([How to Manage Bluetooth Devices on Linux Using bluetoothctl](https://www.makeuseof.com/manage-bluetooth-linux-with-bluetoothctl/))
