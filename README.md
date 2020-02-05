# UbuntuiSCSITarget
future home of an Ubunti iSCSI target bash script.


# Ubuntu iSCSI Target documentation

## VM Notes:
Add extra drives
Set static IP (optional)
Checkpoint!


## Installation
sudo apt update
(optional) sudo apt upgrade

sudo apt install openssh-server

Connect via SSH!!!!

sudo lshw -class disk
* make note of your storage devices for your luns

sudo apt install tgt

systemctl status tgt

## Configure your LUN
sudo nano /etc/tgt/conf.d/iscsi.conf


<target iqn.2020-02.example.com:lun1>
    # Provided device as an iSCSI target
    backing-store /dev/sdb                            
    #initiator-address 172.16.144.100 
    #incominguser iscsi-user password
    #outgoinguser iscsi-target secretpass
</target>

systemctl restart tgt


## Connect!!!

Windows iscsi initiator

Inline-style: 
![alt text](https://github.com/redmondmj/UbuntuiSCSITarget/blob/master/images/iSCSIInitiator.PNG "Windows iSCSI Initiator")

discovery - IP

Connect