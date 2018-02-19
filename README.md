# Docker :: Cisco Packet Tracer

Author: Loan Lassalle
---

## Cisco Packet Tracer

Packet Tracer is a cross-platform visual simulation tool designed by Cisco Systems that allows users to create network topologies and imitate modern computer networks. The software allows users to simulate the configuration of Cisco routers and switches using a simulated command line interface. Packet Tracer makes use of a drag and drop user interface, allowing users to add and remove simulated network devices as they see fit. The software is mainly focused towards Certified Cisco Network Associate Academy students as an educational tool for helping them learn fundamental CCNA concepts.

## Prerequisites

 * macOS High Sierra 10.13.3 or later
 * XQuartz 2.7.11 or later
 * Docker for Mac 17.12.0 or later

## How to use

### XQuartz

Fisrt of all, you need to run `XQuartz` application.

```sh
open -a XQuartz
```

In the XQuartz preferences, go to the `Security` tab and make sure you’ve got `Allow connections from network clients` ticked.

<p align="center">
  <img src="images/xquartz_preferences.png" width="500" height="363" alt="XQuartz - Allow connections from network clients"/>
</p>

Afer that, you need to run `xhost` and allow connections from your local machine.

```sh
xhost + $(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}')
```

### Docker

You can now run Cisco Packet Tracer container.

```sh
docker run \
    --env DISPLAY=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}'):0 \
    --detach \
    --name cisco-packet-tracer \
    --privileged \
    --rm \
    --volume /tmp/.X11-unix/:/tmp/.X11-unix/ \
    --volume $HOME/.packettracer:/root/pt \
    avend0black/cisco-packet-tracer
```