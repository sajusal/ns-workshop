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

## Configure SR-MPLS

Replace X in SID index with your router number

```bash
/configure router "Base" mpls-labels sr-labels start 21000
/configure router "Base" mpls-labels sr-labels end 22000
/configure router "Base" isis 0 advertise-router-capability as
/configure router "Base" isis 0 traffic-engineering true
/configure router "Base" isis 0 segment-routing admin-state enable
/configure router "Base" isis 0 segment-routing prefix-sid-range global
/configure router "Base" isis 0 interface "system" ipv4-node-sid index X
```

## Verify SR-MPLS

```bash
show router tunnel-table
```

```bash
tools dump router segment-routing tunnel
```

## Configure BGP

```bash
/configure router "Base" autonomous-system 64500
/configure router "Base" bgp group "edge" type internal
/configure router "Base" bgp group "edge" peer-as 64500
/configure router "Base" bgp neighbor "100.100.100.100" group "edge"
```

## Verify BGP status

```bash
show router bgp summary
```

```bash
show router bgp neighbor "100.100.100.100" advertised-routes ipv4
```

```bash
show router route-table
```






