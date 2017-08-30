# Open vSwitch Lab

## <a name="require">១. ឧបករណ៍ដែលត្រូវមាន</a>

នៅក្នុងLabនេះ យើងត្រូវមានឧបករណ៍ដូចជា៖
- 1 PC/Desktop ដំណើរការប្រពន្ធប្រតិបត្តិការLinux និងបានinstall Open vSwitch
- នៅលើកុំព្យូទ័រនេះមានដំឡើងVirtualbox ហើយក្នុងនោះមានដំឡើងម៉ាសុីននិមិត្ត២ស្រាប់ផងដែរ

## <a name="process">២. ដំណើរការ</a>

* បង្កើតvSwitch មានឈ្មោះថា `br0`
> ovs-vsctl add-br br0

  * បង្ហាញ៖
> ovs-vsctl show

* Turn up this port
> ifconfig br0 up

  * ពិនិត្យមើល
> ifconfig
  * បើសិនលុយវិញប្រើcommandខាងក្រោម
> ovs-vsctl del-br br0

មកដល់ត្រឹមនេះយើងមានដ្យាក្រាមដូចរូបខាងក្រោមនេះ
![ovs1](/images/ovs_lab1.jpg)

* ភ្ជាប់bridgeនេះទៅនឹងinterface eth0នៃphysical machine
> ovs-vsctl add-port br0 eth0
  * ពិនិត្យមើលលទ្ធផង
> ovs-vsctl show

មកដល់ពេលនេះphysical machine មិនអាចមានទំនាក់ទំនងទៅInternetខាងក្រៅបានទេ។​ 

![ovs2](/images/ovs_lab2.jpg)

  * ដើម្បីដោះស្រាយបញ្ហានេះ យើងត្រូវធ្វើដូចខាងក្រោម៖
> ifconfig eth0 0	# ដើម្បីលុបIPពីinterface eth0

បន្ទាប់មកទៀត
> dhclient br0 	# ដើម្បីasign IP​ ដោយdhcpទៅbr0

> ifconfig		# យើងនឹងឃើញថាbr0ទទួលបានIP

> route -n 		# ពិនិត្យមើលrouting table

ពេលនេះយើងអាច `ping google.com` បានហើយ។
* មកដល់ដំណាក់កាលនេះយើងបង្កើតtap 2 សំរាប់ភ្ជាប់ទៅនឹងVM
> ip tuntap add mode tap vport1
> ip tuntap add mode tap vport2
> ifconfig vport1 up
> ifconfig vport2 up

  * ពិនិត្យមើល
> ifconfig

  * ភ្ជាប់ vport1 & vport2 ទៅនឹងbr0
> ovs-vsctl add-port br0 vport1 -- add-port br0 vport2

> ovs-vsctl show

  * នៅលើVirtualBox ចុចលើVM1 ហើយចុចលើsetting -> Network​ -> Adapter x -> Enable Network Adapter -> Advance to: Bridged Adapter -> name: vport1។
  * ធ្វើដូចគ្នានៅលើVM2 ដោយខុសត្រង់name: vport2។
![ovs lab](/images/ovsLab.jpg)
  * សាកល្បងpingមើល(នៅលើVMនិយមួយៗ) យើងសង្កេតឃើញថាpingបានធម្មតា
  * ពិនិត្យមើលបន្ថែម
> ovs-vsctl fdb/show br0

> ovs-ofctl show br0
