# Docker Networking

* [Design](https://github.com/docker/libnetwork/blob/master/docs/design.md)

Container Network Model (CNM) is implemented by libnetwork.

## Single-host

Using bridge (a.k.a. virtual switch, vswitch) driver (`docker0`), containers can talk to each other.

## Multi-host

Since Docker 1.12, acquiring technology from Socket Plane, Docker can use overlay driver to enable multi-host.

You can have 3 physical machines all using the same network subnet like 10.0.0.2, 10.0.0.8, 10.0.0.50, etc and each have their own different IP address like 192.168.0.5, 172.32.46.43, or 172.31.0.8 and all using the same overlay 10.0.0.0/24.

VXLAN tunnel (layer-2 broadcast domain) is the overlay network. Layer-2 adjacency.

## IPAM



