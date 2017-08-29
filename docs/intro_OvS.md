# អត្ថបទស្ដីអំពី**Open vSwitch**
--------------------------------

## មាតិការ
* [១. ជាទូទៅ](#intro)
  * [១.១. Open vSwitchជាអ្វី?](#sub-intro)
  * [១.២. មុខងារ](#feature)
  * [១.៣. ធាតុផ្សំនៃOpen vSwitch](#architec)
* [២.​ ដំឡើង Open vSwitch](#install)
* [៣. Commands សំខាន់ៗមួយចំនួន](#command)
  * [៣.១. Switch](#switch)
  * [៣.២. Ports](#port)
  * [៣.៣. STP](#stp)
* [៤.​ ឯកសារយោង](#ref)
--------------------------------

## <a name="intro">១. ជាទូទៅ</a>
### <a name="sub-intro">១.១. Open vSwitchជាអ្វី?</a>
![OpenvSwitch](http://openvswitch.org/assets/featured-image.jpg)
- Open vSwitch ជា Soft-switchមួយ (មួយក្នុងចំនោម៣បច្ចេកវិទ្យា៖ Open vSwitch, macvlan & Linux bridge) ជាដំណោះស្រាយនិមិត្តកម្មបណ្ដាញនៅខាងក្នុងphysical machine ដោយsoftware។
- Open vSwitch (ជួនកាលគេសរសេរកាត់ថា OVS) ជាOpen software ផ្ដល់អជ្ញាបណ្ណដោយ![Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)។
- OVS supports multiple Linux-based virtualization technologies រួមមាន៖ Xen/XenServer, KVM, & VirtualBox។
- OVSត្រូវបានសរសេរដោយភាសា'C' ហើយមានភាពងាយស្រួលក្នុងការផ្លាស់ប្ដូរ(easily ported to other environments)
- OVSអាចដំណើរការនៅលើ Linux-based, FreeBSD, Windows, non-POSIX embedded Systems,...

### <a name="feature">១.២. មុខងារ</a>
OVS ជំនាន់ថ្មីsupportsមុខងារដូចខាងក្រោម៖
  * Standard 802.1Q VLAN model with trunking and access ports
  * NIC bonding with or without LACP on upstream switch
  * NetFlow, sFlow(R), and mirroring for increased visibility
  * QoS
  * Geneve, GRE, VXLAN, STT, LISP tunneling
  802.1aq connectivity fault management
  * Openflow 1.0 plus numerous extensions
  * Transactional configuration database with C and Python bindings
  * High-performance forwarding using a Linux kernel module


### <a name="architec">១.៣. ធាតុផ្សំនៃOpen vSwitch</a>
![OVS architecture](/images/architecture.jpg)
* Control Plane(user mode):
  * **ovs-vswitchd** -មានតួនាទីជា​ 1 daemon​ switch ប្រតិបត្តិបញ្ជូនបន្ត(switch) រួមជាមួយmoduleនៅក្នុងLinux kernel សំរាប់flow-based switching
  * **ovsdb-server** -ជាdatabase serverដែលសំរាប់ovs-vswitchdផ្ទុកswitch configurations

* Kernel Mode:
  * Kernel module រួមជាមួយ`ovs-vswitchd`សំរាប់packet switching។​ It also does a Fast path switching.

* Command Line Interface:
  * **ovs-dpctl** -ជាឧបករណ៍(tool)សំរាប់configuring the switch kernel module
  * **ovs-vsctl** -ប្រើសំរាប់configure the switch, i.e it is use to push configs to OVSDB.
  * **ovs-appctl** -ប្រើសំរាប់បញ្ជូនcommandsទៅovs-vswithd.
  * **ovs-ofctl** -ប្រើសំរាប់បញ្ជូនcommandsទៅopenflow module.

## <a name="install">២.​ ដំឡើង Open vSwitch</a>
សំរាប់ Debian:
> sudo apt-get install -y openvswitch-switch openvswitch-common

[!ឫក៏អាចមើលតាមការណែនាំនេះ](http://docs.openvswitch.org/en/latest/intro/install/)

## <a name="command">៣. Commands សំខាន់ៗមួយចំនួន</a>
យោងទៅតាម http://manpages.ubuntu.com/manpages/xenial/man8/ovs-vsctl.8.html
### <a name="switch">៣.១. Switch</a>

```
ចំនាំថា អ្នកត្រូវតែមានសិទ្ទជា super user ទើបអាចដំនើរការcommandsទាំងនេះ!
```

- បង្ហាញ virtual switchបច្ចប្បន្ន
```
ovs-vsctl show
```

or
```
ovs-vsctl list-br
```

- ថែម ឫលុបVirtual switch
```
ovs-vsctl add-br <switch-name>

ovs-vsctl del-br <switch-name>
```

### <a name="port">៣.២. Ports</a>
- រាយពត័មានអំពីបណ្ដាportនៅលើ vswitch:
```
ovs-vsctl list-ports <swith-name>
```

- ថែម ឫលុបport
```
ovs-vsctl add-port <br-name> <ifname>

ovs-vsctl del-port <br-name> <ifname>
```

- Set ប្រភេទអោយport:
```
ovs-vsctl set interface <interface_name> type=<type_name>
```

type_name: internal, vxlan, gre, etc.


- Set VLAN អោយport
```
ovs-vsctl set port <ifname> tag=<vlan-id>
```

- ថែម port និងset អោយport
```
ovs-vsctl add-port <br-name> <ifname> tag=<vlan-id> -- set interface <ifname> type=<type_name>
```

- បង្ហាញចេញឈ្មោះរបស់vswitchដែលមានport
```
ovs-vsctl port-to-br <port_name>
```

### <a name="stp">៣.៣. STP</a>
- Turn {on|off} STP protocol:
```
ovs-vsctl set Bridge <vswitch> stp_enable=<{true|false}>
```

- បង្កើតbridge prioriy ដើម្បីជ្រើសរើសroot bridge
```
ovs-vsctl set Bridge <vswitch> other_config:stp-priority=<prio>
```

- Example:
> ovs-vsctl set Bridge br0 other_config:stp-priority=0x7800

- បង្កើតport priority ដើម្បីជ្រើសរើសroot port
```
ovs-vsctl set Port <vswitch> other_config:stp-path-cost=<prio>
```

## <a name="ref">៤.​ ឯកសារយោង</a>
[1] http://openvswitch.org/slides/ppf.pdf

[2] http://docs.openvswitch.org/en/latest/

[3] http://networkstatic.net/openflow-openvswitch-lab/

[4] https://www.slideshare.net/yongkikim106/understanding-open-vswitch

[5] https://www.youtube.com/watch?v=rYW7kQRyUvA

[6] https://opennetworkingblog.blogspot.in/2016/06/openvswitch-introduction.html?view=classic
