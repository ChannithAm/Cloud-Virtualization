# ស្វែងយល់អំពីនិមិត្តកម្ម Hypervisor
--------------------------------------------

## មាតិការ
* [1. និយមន័យ](#def)
* [2. ចំណែកថ្នាក់](#class)
  * [1.1. Type-1, Native or Bare-Metal hypervisors](#type1)
  * [1.2. Type-2 or Hosted hypervisors](#type2)
* [3. References](#ref)

*****************************************
## <a name = "def"> 1. និយមន័យ </a>
**Hypervisor** មានឈ្មោះហៅមួយទៀតថា Virtual Machine Monitor (VMM) ជាពាក្យដែលសំដៅទៅលើ Software, firmware ឫក៏ Hardware ដែលប្រើសំរាប់បង្កើត និងដំណើរការម៉ាសុីននិមិត្ត VM(Virutal Mchines)។
```
- កុំព្យូទ័រដែល`Hypervisor`​ដំណើរការម៉ាសុីននិមិត្តមួយ ឫច្រើនហៅថា `Host Machine`
- VM និមួយហៅថា `Guest Machine`
```

## <a name = "class"> 2. ចំណែកថ្នាក់ </a>
Hypervisor ត្រូវបានបែងចែកជាពីរ
- Type-1, Native or Bare-Metal hypervisors
- Type-2 or Hosted hypervisors

![Type of hypervisor](/images/hypervisor.jpg)


### <a name = "type1">1.1. Type-1, Native or Bare-Metal hypervisors</a>

ជាប្រភេទHypervisorដំណើរការដោយផ្ទាល់នៅលើHardwareរបស់Host Machine ដើម្បីcontrol the hardware និងគ្រប់គ្រងGuest OS។ វាមានសិទ្ធិក្នុងការបញ្ជា Host Hardware ដូច្នេះទិន្នផល និងសមត្ថភាពការពារសុវត្តិភាពល្អជាង។

Hypervisorដំបូងគេឋិតនៅក្រុមនេះត្រូវបានអភិវឌ្ឍន៍ដោយក្រុមហ៊ុនIBMនៅឆ្នាំ១៩៦០រួមមាន៖ SIMMON, CP/CMS OS។

Hypervisor ពេលបច្ចប្បន្នដែលកំពុងពេញនិយមមានដូចជា៖ Xen, Oracle VM Server for SPARC, Oracle VM Server fo X86, Microsoft Hyper-V និង VMware ESX/ESXi។

### <a name = "type2">1.2. Type-2 or Hosted hypervisors</a>

ជាប្រភេទHypervisorត្រូវបានដំឡើង និងដំណើរការនៅលើប្រពន្ធប្រតិបត្តិការ(OS) ដូចជាSoftwareធម្មតាដទៃទៀត ទើបត្រូវបានហៅថា Hosted hypervisor។ ប្រភេទនេះយកធនធាន ដែលប្រពន្ធប្រតិបត្តិការផ្ដល់អោយដើម្បីគ្រប់គ្រង និងបែងចែកធនធានទាំងនេះ។

Hypervisorនៅក្នុងក្រុមនេះមានដូចជា៖ VMware Workstation, VMware Player, VirtualBo, Parallels Desktop for Mac និង QEMU។

ទោះបីជាយ៉ាងណាក៏ដោយ បណ្ដារប្រភេទដែលឋិតនៅក្រុមទីពីរនេះ វាមានមួយចំនួនដំណើរការស្រដៀងគ្នាទៅនឹងក្រុមទីមួយ។ ជាក់ស្ដែង Linux's Kernel-based Virtual Machine (KVM) និង FreeBSD's bhyve។ ពីរVMMនេះជា `kernel module` និងពួកវាមានសម្ថភាពផ្លាស់ប្ដូរប្រពន្ធប្រតិបត្តិការរបស់Host Machineក្លាយទៅជា Hypervisor Type-1 និងដំណើរការស្រដៀង Typer-1។ ប៉ុន្តែដោយសារ `KVM` និង`bhyve` ត្រូវបានbuild ផ្អែកទៅលើ `Distro`ខុសគ្នារបស់Linux (ឧទាហរណ៍៖ `bhyve` ត្រូវបានbuildលើ FreeBSD ដែលជា ១​ Linux Distro។ ចំនែកឯ `KVM` គឺដំឡើងដោយផ្ទាល់នៅលើ Linux Distroមួយណាក៏បាន) ដូច្នេះពួកគេនៅតែចាត់ជា Hypervisor type-2។

ចំពោះគុណសម្បត្តិ និងគុណវិបត្តិរបស់(VMM)​ ទាំងពីរប្រភេទនេះ បើតាមIBM គឺType-1 មានប្រសិទ្ធភាពខ្ពស់ (higher perfomance), availablity, and security than Type-2 hypervisor។

## <a name = "ref">3. References </a>
---------------------------------
[1] https://viblo.asia/p/tan-man-ao-hoa-ai-cung-biet-nhung-cu-the-no-la-gi-Do754NV3ZM6



