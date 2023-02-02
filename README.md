# Chip Tool Snap
[![chip-tool](https://snapcraft.io/chip-tool/badge.svg)](https://snapcraft.io/chip-tool)

Chip Tool is a Matter controller being developed as part of the [Connected Home IP project](https://github.com/project-chip/connectedhomeip.git).

The snap packaging makes it easy to run the Chip Tool on Linux distributions.

This snap has been tested on amd64/arm64 architectures for WiFi/Ethernet/DNS-SD/BLE commissioning and control. It has not been tested with the Thread protocol.

## Usage

### Setup

```bash
sudo snap install chip-tool
```

Connect the [`avahi-observe`](https://snapcraft.io/docs/avahi-observe-interface) interface to allow DNS-SD based discovery:
```bash
sudo snap connect chip-tool:avahi-observe
```

Connect the [`bluez`](https://snapcraft.io/docs/bluez-interface) interface for device discovery over Bluetooth Low Energy (BLE):
```bash
sudo snap connect chip-tool:bluez
```

### Commissioning
Discover and pair:
```bash
sudo chip-tool pairing onnetwork 110 20202021
```

Or, pair directly by giving the IP address:
```bash
sudo chip-tool pairing ethernet 110 20202021 3840 192.168.1.110 5543
```

where:

-   `110` is the node id being assigned to the app
-   `20202021` is the pin code set on the app
-   `3840` is the discriminator id
-   `192.168.1.110` is the IP address of the device running the app
-   `5540` the port for server that runs inside the app


### Control
Toggle:
```bash
sudo chip-tool onoff toggle 110 1
```

where:

-   `onoff` is the matter cluster name
-   `on`/`off`/`toggle` is the command name.
-   `110` is the node id of the app assigned during the commissioning
-   `1` is the endpoint of the configured device


## Build

Build locally for the architecture same as the host:
```bash
snapcraft -v
```

Build remotely for all supported architectures:
```
snapcraft remote-build
```

## Note on Cross build
for cross compiling this snap for arm64 target on amd64 build machine 
Use following command
snapcraft --build-for
