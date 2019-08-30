# VBoxManage

$ cd '\Program Files\Oracle\VirtualBox'
$ .\VBoxManage.exe


VBoxManage list vms


VBoxManage export Ubuntu -o C:\Users\luis.lopes\Dropbox\mac\tut\vagrant\unbunto.ova --options manifest,nomacs

VBoxManage import C:\Users\luis.lopes\Dropbox\mac\tut\vagrant\test2.ova --vsys 0 --vmname ola

VBoxManage modifyvm test_1 --name teste2
VBoxManage modifyvm "Ubuntu" --groups "/TestGroup"


## Start VM in headless mode
VBoxManage startvm MyVM 
VBoxManage startvm MyVM --type headless
VBoxManage startvm MyVM --type gui

## Power off VM
VBoxManage controlvm MyVM poweroff
pause|resume|reset|poweroff|savestate|acpipowerbutton|acpisleepbutton


start a VMgroup ??

VBoxManage list -l vms | awk '/^Groups:/ { groups = $2; } /^UUID:/ { uuid = $2; if (groups == "/groupname") print uuid; }'

.\VBoxManage startvm -group /tt
#  decrease Virtual Disk Size
```
VBoxManage modifyvdi "D:\Users\luis\VirtualBox VMs\Ubuntu Zabbix Grafana\Appliance-disk002.vdi" compact
```

##  Increase Virtual Disk Size
### Increase the size of fixed sized disk in Virtualbox
 - https://www.youtube.com/watch?v=ikSIDI535L0
```bash
sudo dd if=/dev/sba of=/dev/sdb

df -kh
```
### Increase virtual machine disk size corrections and windows fix
 - https://www.youtube.com/watch?v=-eMq4KtlYUg

```bash
top
cat /proc/swaps
sudo blkid
sudo grep swap /etc/fstab
sudo vim /etc/fstab
```
- https://www.youtube.com/watch?v=r_UyKufXR3c

## Virtual Box : How to Increase Disk Size - Windows
- https://www.youtube.com/watch?v=7Aqx-VHv2_k
- https://www.youtube.com/watch?v=Ujd72kRMfFM 

## In VirtualBox
### Increase Virtual Disk Size (VMDK)
#### clone VMDK to VDI
VBoxManage clonehd "D:\Users\luis\VirtualBox VMs\Ubuntu Zabbix Grafana\Appliance-disk002.vmdk" "D:\Users\luis\VirtualBox VMs\Ubuntu Zabbix Grafana\Appliance-disk002.vdi" --format vdi
#### resize the VDI
VBoxManage modifymedium "D:\Users\luis\VirtualBox VMs\Ubuntu Zabbix Grafana\Appliance-disk002.vdi" --resize 16384
#### clone VDI to VMDK 
VBoxManage clonehd "D:\Users\luis\VirtualBox VMs\Ubuntu Zabbix Grafana\Appliance-disk002.vdi" "D:\Users\luis\VirtualBox VMs\Ubuntu Zabbix Grafana\Appliance-disk002.vmdk"  --format vmdk

#### Manually installing VBoxGuestAdditions [windows guest]
[host] # vboxmanage guestcontrol updateadditions "<vbox_name>" --source /usr/share/virtualbox/VBoxGuestAdditions.iso --verbose


https://www.youtube.com/watch?v=cDgUwWkvuIY
https://www.youtube.com/watch?v=QSpGaeHlkoE
https://www.youtube.com/watch?v=KW1ScgdCIfs
https://www.youtube.com/watch?v=hugEkh50Ynk
https://www.howtogeek.com/124622/how-to-enlarge-a-virtual-machines-disk-in-virtualbox-or-vmware/
https://www.howtogeek.com/howto/40702/how-to-manage-and-use-lvm-logical-volume-management-in-ubuntu/


#### Set the Path of Virtual Machine - https://devopsmates.com/oracle-virtual-box-installation-on-rhelcentos-7/

Validate the Installation

```
vboxmanage –version
```
 

vboxmanage is the CLI provided by the Virtual Box package.

Steps to Create a VM:

Set the Path of Virtual Machine

```
vboxmanage setproperty machinefolder /vm_store/virtual_machines
```
 

Create a VM Container and register it.

```
VBoxManage createvm --name "demovm" --register
```
 

Create a vDisk for the VM. This file will be presented to the VM as a virtual disk.

```
VBoxManage createvdi --filename /vm_store/virtual_machines/demovm/demovm-vdisk01.vdi --size 6000
```
 

In this example, disk size will be 6G and disk type will be vdi.

List OS types supported by installed Virtual Box software.

```
VBoxManage list ostypes
```
 

Configure the compute, networking and container operating system support.

```
VBoxManage modifyvm "demovm" --cpus 1 --memory 1024 --acpi on --boot1 dvd --nic1 bridged --bridgeadapter1 eth0 --cableconnected on --ostype RedHat_64
```
 

Create Storage IDE controller and attach to the VM.

```
VBoxManage storagectl "demovm" --name "SATA Controller" --add sata
```
 

Attached the vDisk and the ISO image for the operating system installation.

```
VBoxManage storageattach "demovm" --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium /vm_store/virtual_machines/demovm/demovm-vdisk01.vdi
```
```
VBoxManage storageattach "demovm" --storagectl "SATA Controller" --port 1 --device 0 --type dvddrive --medium /vm_store/CentOS-7-x86_64-DVD-1511.iso
```
Start VirtualBox VM from the command line

```
VBoxManage startvm "demovm" --type gui &
```
To display the information about Machine.

```
VBoxManage showvminfo “demovm”
```
To take a snapshot of the VM.

```
VBoxManage snapshot “demovm” take <snapshot_name>
```
Revert back to a particular snapshot

```
VBoxManage snapshot “demovm” restore <snapshot_name>
```
Power off the VM

```
VBoxManage controlvm “demovm” poweroff
```
Delete the VM

```
VBoxManage unregistervm “demovm” –delete
```
Pre-built VirtualBox VMs

If you want to use pre-built VM’s, can download those from Oracle Technology Site.

http://www.oracle.com/technetwork/community/developer-vm/index.html


 vboxmanage setproperty machinefolder /vm_store/virtual_machines

 # automation Virtualbox Unattended Guest Install
 - https://www.youtube.com/watch?v=wUQ1CNptnTI
 - https://github.com/HealisticEngineer/Powershell/blob/master/New-Virtualbox.ps1

 https://blogs.oracle.com/scoter/oracle-vm-virtualbox-52:-unattended-guest-os-install
 https://www.virtualbox.org/manual/ch08.html#vboxmanage-unattended
 - http://underpop.online.fr/v/virtualbox/vboxmanage-unattended.html
