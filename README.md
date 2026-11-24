# SR OS Workshop

## Topology

[!image](topo.png)

## Configure Ports

```bash
/configure port 1/1/c1 admin-state enable connector breakout c1-100g
/configure port 1/1/c1/1 admin-state enable
```

Compare and commit

## Configure Interface

Replace X in IP address with your router number

```bash
/configure router "Base" interface "to-core" port 1/1/c1/1
/configure router "Base" interface "to-core" ipv4 primary address 192.168.X.0 prefix-length 31
```

Compare and commit

## Configure System Loopback

Replace IP with the correct System loopback IP of your router based on the topology.

```bash
/configure router interface "system" ipv4 primary address X.X.X.X prefix-length 32
```

Compare and commit

## Verify Port and Interface status

```bash
show port
```

```bash
show router interface
```

Ping the core interface IP

Replace X in IP address with your router number

```bash
ping 192.168.X.1
```

## Configure ISIS

```bash
/configure router isis admin-state enable area-address 49.0000
/configure router "Base" isis 0 interface "system" passive true
/configure router "Base" isis 0 interface "system" interface-type point-to-point
/configure router "Base" isis 0 interface "to-core" interface-type point-to-point
```

Compare and commit

## Verify ISIS status

```bash
show router isis adjacency
```

```bash
show router isis database
```




