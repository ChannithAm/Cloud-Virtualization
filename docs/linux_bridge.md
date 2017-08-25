# មេរៀនណែនាំអំពី Linux bridge
------------------------------

## បញ្ជីអត្ថបទ
* [១.​ និយមន័យ](#intro)
* [២. ធាតុផ្សំរបស់linux bridge](#component)
* [៣. មុខងារSwitchមួយដែលបង្កើតដោយlinux bridge](#function)
* [៤. ដំឡើងឧបករណ៍គ្រប់គ្រង linuxbridge នៅលើubuntu 16.04](#install)
* [៥. Linux bridge command](#command)
  * [៥.១. ជាទូទៅ](#manpages)
  * [៥.២. Commandsសំខាន់ៗមួយចំនួន](#useful)
    * [៥.២.១. Bridge](#bridge)
    * [៥.២.២. Ports](#port)
    * [៥.២.៣. Ageing](#ageing)
    * [៥.២.៤. STP](#stp)
* [ឯកសាយោង](#ref)

--------------------------------
## <a name="intro">១.​ និយមន័យ</a>
- Linux-bridge ជា `soft-switch` ដែលជា មួយក្នុងចំនោមបីបច្ចេកវិទ្យាផ្ដល់switchនិមិត្តនៅក្នុងប្រពន្ធ័Linux (២ទៀតគឺ macvlan, OpenvSwitch)ជាមធ្យោបាយ `network virtualize`នៅក្នុងphysicalphysical machine។
- បើនិយាយអំពីភាពlogicវិញគឺ Linux bridge នឹងបង្កើតកូនswitchនិមិត្តមួយ ដើម្បីអោយបណ្ដារVM(virtual machine)អាចតភ្ជាប់ និងអាចទំនាក់ទំនងជាមួយគ្នា ក៏ដូចជាភ្ជាប់ដោយផ្ទាល់ទៅនឹងបណ្ដាញខាងក្រៅផងដែរ។
- Linux bridge ជា`kernel module`មួយ។

## <a name="component">២. ធាតុផ្សំរបស់linux bridge</a>
(https://camo.githubusercontent.com/3de8817e61ac39ed01b25ba615169155745191a9/687474703a2f2f692e696d6775722e636f6d2f786f62376c6a512e706e67)

ធាតុផ្សំរបស់linux​ bridgeមានដូចរូបខាងលើ។ ហើយខាងក្រោមនេះគឺជាសញ្ញាណមួយចំនួនទាក់ទងទៅនឹងlinux bridge៖
  * **Port**:​ ស្រដៀងគ្នានឹងportរបស់switchពិត
  * **Bridge**: ស្រដៀងគ្នានឹងswitch layer 2
  * **Tap**: ឫក៏ជាtap interface អាចយល់ថាជាinterfaceសំរាប់ភ្ជាប់VMទៅនឹងbridgeស្ថិតនៅក្នុងkernel។ Tap ដំនើរកានៅlayer 2 នៃទំរង់OSI។
  * **fd**: `forward data`-ផ្លាស់ប្ដូរទិន្ន័យពីVMដល់bridge

  
## <a name="function">៣. មុខងារSwitchមួយដែលបង្កើតដោយlinux bridge</a>
- STP: ជាមុខងារមួយបង្កាភាពច្រំដែល(loop)របស់packetនៅក្នុងswitch
- Vlan: ចែកswitch(បង្កើតដោយlinux bridge)បង្កើតជាvirtual LAN។ មុខងារសំខាន់ក្នុងការផ្ដាច់នៅចរាចរណ៍រវាងបណ្ដាVMនៅលើVLANខុសគ្នា នៃswitchតែមួយ។
- FDB: មុខងារបញ្ជូនបន្តpacketតាមរយៈdatabaseដើម្បីបង្កើតប្រសិទ្ធភាពរបស់switch។

## <a name="install">៤. ដំឡើងឧបករណ៍គ្រប់គ្រង linuxbridge នៅលើubuntu 16.04</a>

```
$sudo apt-get install bridge-utils
```

## <a name="command">៥. Linux bridge command</a>
--------------------------------
### <a name="manpages">៥.១. ជាទូទៅ</a>
>http://manpages.ubuntu.com/manpages/xenial/man8/brctl.8.html

### <a name="useful">៥.២. Commandsសំខាន់ៗមួយចំនួន</a>
#### <a name="bridge">៥.២.១. Bridge</a>
- Show all current virtual switch:
> brctl show

- Add, delete virtual switch:
> brctl addbr <brname>
> brctl delbr <brname>

#### <a name="port">៥.២.២. Ports</a>
- Show  information on the bridge
> brctl show <brname>

- Add, delete port:
> brctl addif <brname> <ifname>		# ifname: interface name of port <brname>
> brctl delif <brname> <ifname>

#### <a name="ageing">៥.២.៣. Ageing</a>
- Show forwarding table of bridge:
> brctl showmacs <brname>

- Set RTT:
> brctl setageing <brname> <time>

#### <a name="stp">៥.២.៤. STP</a>
- Show bridge stp info:
>brctl showstp <bridge>

- Turn {on|off}} spanning tree protocol:
> brctl stp <bridge> {on|off}

- Set bridge forward delay:
> brctl setfd <bridge> <time>

- Set bridge prioriy ដើម្បីជ្រើសរើស root bridge:
> brctl setbridgeprio <bridge> <prio>

- Set port prioriy ដើម្បីជ្រើសរើស root port:
> brctl setportprio <bridge> <port> <prio>

-----------------------------
To Do,
- learn about noVNC -Google Chrome
- Create bridge by command and xml
- Network mode

## <a name="ref">ឯកសាយោង</a>

[1] https://github.com/hocchudong/Linux-bridge

[2] https://wiki.linuxfoundation.org/networking/bridge

[3] https://github.com/hocchudong/thuctap012017/blob/master/XuanSon/Virtualization/Virtual%20Switch/Linux%20bridge/Linuxbridge_basic.md

[4] http://xmodulo.com/use-kvm-command-line-debian-ubuntu.html

[5] http://www.server-world.info/en/note?os=Ubuntu_14.04&p=kvm&f=1

https://www.youtube.com/watch?v=aN8lb2O-wHs
