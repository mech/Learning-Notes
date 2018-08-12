# Docker Networking

* [CNM Design](https://github.com/docker/libnetwork/blob/master/docs/design.md)
* [Old design until Docker 1.6 before libnetwork - Worth a read too](https://docs.docker.com/v1.6/articles/networking/)

Container Network Model (CNM) is implemented by libnetwork.

From Docker 1.9, we can use `docker network` or user-defined networking.

Linux that run systemd like Ubuntu 16.04 use Predictable Network Interface Names (PNIN) like ens1 instead of eth0, etc.

The gateway will be the first available IP.

## Load Balancing

* [Introduction to modern network load balancing and proxying](https://blog.envoyproxy.io/introduction-to-modern-network-load-balancing-and-proxying-a57f6ff80236)

## Docker Internal Networking

Prior to Docker 1.9 and is not recommended.

Docker create an interface called `docker0`

```
▶ ip a show docker0

// Check port mapping and verify netfilter policies
▶ sudo iptables -t nat -L
```

The default `bridge` network is not recommended for production. There will be no **automatic service discovery** and can only use IP addresses. Discovery service is only enabled for user-defined bridge network.

Using the legacy `--link` flag is not recommended.

## Docker Networking

```
// Using default
▶ docker network create jobline-net

// Configure with options
▶ docker network create --driver bridge \
  --opt com.docker.network.bridge.host_binding_ipv4=58.x.x.x \
  --opt com.docker.network.bridge.name=jobline-bridge-0 \
  jobline-net

▶ docker network ls
▶ docker network inspect jobline-net

▶ docker run -d --net=jobline-net --name redis-db redis

// Or we can do it dynamically
▶ docker network connect jobline-net redis-db

// Remove container from the docker0 bridge and just use jobline-net
▶ docker network disconnect bridge redis-db

▶ sudo apt install bridge-utils
▶ brctl show
▶ ip link show
```

If you create user-defined network, you can't use `--link` anymore but you gain a DNS discovery natively which is better.

## Single-host Networking

* 802.1d bridge

Using bridge (a.k.a. virtual switch, vswitch) driver (`docker0`), containers can talk to each other easily on a single host machine.

## Multi-host Networking

* Since it is distributed, Docker needs a place to store information about the overlay network using Consul/etcd/ZooKeeper
* Need at least 3 cluster member for this key-value store for fault tolerance
* Need Linux 3.16 or greater
* Docker host need to open these ports: 7946 (Serf), 4789 (VXLAN), 8500 (Consul), or any key-value store you chose

Since Docker 1.12, acquiring technology from Socket Plane, Docker can use `overlay` driver to enable multi-host.

You can have 3 physical machines all using the same network subnet like 10.0.0.2, 10.0.0.8, 10.0.0.50, etc and each have their own different IP address like 192.168.0.5, 172.32.46.43, or 172.31.0.8 and all using the same overlay 10.0.0.0/24.

See [Overlay documentation](https://docs.docker.com/network/overlay-standalone.swarm/)

VXLAN tunnel (layer-2 broadcast domain) is the overlay network. Layer-2 adjacency.

* Level-2 broadcast domain - everyone get an IP address that can talk directly to each other without having to go through the router. The router still isolate different network, but the VXLAN tunnel make it seems like just one network.

## IPAM

Having Docker manage IP allocations through IPAM is a huge benefit.

## Security

Docker binds exposed ports on all interfaces (0.0.0.0) by default.

## DNS and Linking

* Docker has basic name resolution.
* `--icc=false` prevent containers on the same bridge from talking directly to each other. This forces them to talk to each other only through published ports.
* Linking provides a mechanism to override `--icc=false` rules
* Linking work in one direction
* Linking works differently when using user-defined networks
* `docker0` bridge has `--icc=true` by default

User-defined networks benefit from what's being named **embedded DNS**. It does not rely on `hosts` file or ENV variables.

```
▶ docker network create jobline-net
▶ docker run -d -P --name=web --net=jobline-net

// We can see that container connected to a user-defined network
// should use the embedded DNS server of 127.0.0.11
▶ docker exec -t web more /etc/resolv.conf
```

The name resolution for embedded DNS is bidirectional in contrast to links.

All the resolution is now occurring in the embedded DNS server and will not touch the `hosts` file.


