# UbuntuiSCSITarget
Future home of an Ubuntu iSCSI target bash script. For now... documentation on a manual installation and configuration.


# Ubuntu iSCSI Target documentation

## Hyper-V VM Notes:
1. Rmemeber to disable secure boot in order to install the OS

![Disable Secure Boot](https://github.com/redmondmj/UbuntuiSCSITarget/blob/master/images/secureBoot.PNG "Disable Secure Boot")

2. Add extra drives

![VM Disks](https://github.com/redmondmj/UbuntuiSCSITarget/blob/master/images/addDisk.PNG "Add disks to VM")


![VM Disks](https://github.com/redmondmj/UbuntuiSCSITarget/blob/master/images/Disks.PNG"Check disks to VM")

3. Set static IP (optional)
4. Create a Checkpoint!


## Installation

1. Get current: `sudo apt update`
2. (optional) `sudo apt upgrade`
3. Get connected: `sudo apt install openssh-server`
    * Now Connect via SSH!!!!
4. List available disks: `sudo lshw -class disk`
    * make note of your storage devices for your luns
5. Install the server: `sudo apt install tgt`
6. Verify: `sudo systemctl status tgt`

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
