# Open vSwitch Lab

Get stated with Open vSwitch, flows and OpenFlow contrllers
-------------------------------------------------------------

## Pre-reqs

Linux system with OVS installed.

## Setup

Use this script to add a bridge with for testing. The interfaces are moved into IP namespaces to isolate them from main namespace and from each other.

```
#!/bin/bash

ovs-vsctl --version

if [ $# -ne 2 ]; then
    echo "usage: $0 port_num ovs_br"
    exit 1
fi

set -xe

port=p$1
ns=ns$1
br=$2
mac=00:00:00:00:00:0$1
ip=10.0.0.${1}/24

# add bridge
ovs-vsctl --may-exist add-br $br

# add port
ovs-vsctl add-port $br $port

# port type
ovs-vsctl set Interface $port type=internal

# Create name spaces
ip netns add $ns

#  Add the peer interface to the corresponding namespaces
ip link set $port netns $ns

# Setup IP {vpeer}
ip netns exec $ns ip link set $port address $mac
ip netns exec $ns ip address add $ip dev $port
ip netns exec $ns sysctl -w net.ipv6.conf.${port}.dsable_ipv6=1
ip netns exec $ns ip link set $port up

```

#### Call script like:

```
# sh ovs-add-port.sh 1 br0
# sh ovs-add-port.sh 2 br0
```
Then the bridge should look like:

```
6e903398-18c1-4e66-8047-06f659be015f
    Bridge "br0"
        Port "p1"
            Interface "p1"
                type: internal
        Port "p2"
            Interface "p2"
                type: internal
        Port "br0"
            Interface "br0"
                type: internal
    ovs_version: "2.5.4"

```

## Test 1 - the normal flow

### Test Connectivity:

```
# ip netns exec ns1 ping -c1 10.0.0.2
```

### Show flows

```
# ovs-ofctl dump-flows br0
```

```
NXST_FLOW reply (xid=0x4):
 cookie=0x0, duration=296.584s, table=0, n_packets=0, n_bytes=0, idle_age=296, priority=0 actions=NORMAL
 
 ```
This flow gets created by default when you create a bridge. The **normal flow** causes the bridge to behave like a simple MAC learning switch. It applies to all ports because no `in_port` was specified and that is ike a wildcard for all ports.

### Show the mac table

```
# ovs-appctl fdb/show br0

```


## Reference

[1] https://gist.github.com/djoreilly/1cf74c684cf03da06ea6