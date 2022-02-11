# UbuntuiSCSITarget
Future home of an Ubuntu iSCSI target bash script. For now... documentation on a manual installation and configuration.
This documentation assumes a few things:

* You have a Windows Host with network acccess to guest VM
* You can install Ubuntu Server on the guest VM
* IP: 172.16.144.100 (replace with your own)
* Username: itstudent (replace with your own)

# Ubuntu iSCSI Target documentation

## Hyper-V VM Notes:
1. Generation 2 VM is reccomended.
2. Your VM will need internet access to install required packages.
3. Remember to disable secure boot in order to install the OS

![Disable Secure Boot](https://github.com/redmondmj/UbuntuiSCSITarget/blob/master/images/secureBoot.PNG "Disable Secure Boot")

2. Add extra drives

![VM Disks](https://github.com/redmondmj/UbuntuiSCSITarget/blob/master/images/addDisk.PNG "Add disks to VM")


![VM Disks](https://github.com/redmondmj/UbuntuiSCSITarget/blob/master/images/Disks.PNG "Check disks to VM")

3. Set static IP (optional)
4. Create a Checkpoint!


## Installation
NOTE: OS Installation is not covered. Default installation will suffice. Network Config is up to you, you can set a static IP (if you know one that will work) or just use DHCP(if available). If offered, choose to install packages for OpenSSH (just convenient, you can skip step 3).

1. Get current: `sudo apt update`
2. (optional) `sudo apt upgrade`
3. Get connected: `sudo apt install openssh-server`
    * Now Connect via SSH!!!!
    * Check your IP ```ip a```
    * From Windows HOST use Putty or Powershell ``` ssh itstudent@172.16.144.100 ```
4. List available disks: `sudo lshw -class disk`
    * make note of your storage devices for your luns
5. Install the server: `sudo apt install tgt`
6. Verify: `sudo systemctl status tgt`
7. To start (if needed): `sudo systemctl start tgt`

## Configure your LUN
1. `sudo nano /etc/tgt/conf.d/iscsi.conf`
```
<target iqn.2020-02.example.com:lun1>
    # Provided device as an iSCSI target
    backing-store /dev/sdb                            
    #initiator-address 172.16.144.100 
    #incominguser iscsi-user password
    #outgoinguser iscsi-target secretpass
</target>
```
2. Restart the service: `sudo systemctl restart tgt`
3. Verify your config: `sudo tgtadm --mode target --op show`


## Connect!!!

1. Run Windows iSCSI initiator

![Initiator](https://github.com/redmondmj/UbuntuiSCSITarget/blob/master/images/iSCSIInitiator.PNG "Windows iSCSI Initiator")

2. Enter the discovery - IP

3. Connect to your LUN!

4. Manage Your new Storage with Disk Management:

![Disk](https://github.com/redmondmj/UbuntuiSCSITarget/blob/master/images/diskManagement.PNG "Disk Management")
