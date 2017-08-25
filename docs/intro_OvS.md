# អត្ថបទស្ដីអំពី**Open vSwitch**
--------------------------------

## មាតិការ

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
**OVS ជំនាន់ថ្មីsupportsមុខងារដូចខាងក្រោម៖**
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

## <a name="ref">ឯកសារយោង</a>
[1] http://openvswitch.org/slides/ppf.pdf

[2] http://docs.openvswitch.org/en/latest/
