---
title: 'How to Manage Bluetooth Devices on Linux Using bluetoothctl'
pubDate: 2023-12-12 10:00:00.0 -7
description: 'Using bluetoothctl.'
author: 'JH'
tags: ['linux', 'bluetooth', 'bluetoothctl']
---

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
