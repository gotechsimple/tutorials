# Creating an Ubuntu 20.04 Server VM on Virtualbox

### Prerequisites

* Virtualbox 6.x is installed

### Installation

1. Download Ubuntu 20.04 ISO
```bash
$ curl -O https://releases.ubuntu.com/20.04.4/ubuntu-20.04.4-live-server-amd64.iso
```

2. Start Virtualbox

3. Click **New**

4. *Name and operating system*
   * **Name** - Enter a name for the virtual machine (VM).  Note: this is *not* the hostname, but the name Virtualbox will refer to it as.
   * **Machine Folder** - The path where the VM files will be created.
   * **Type** - The general operating system type.  Select **Linux**.
   * **Version** - The vendor of the operating syste.  Select **Ubuntu (64-bit)**.
   * Click **Continue**

5. *Memory size*
   * Select the amount of memory you want to give the VM.  You are capped by the amount of physical memory that is on your host system.  Virtualbox will recommend a value given the oeprating system type and version.  For this exercise use the recommended value of **1024**.
   * Click **Continue**

6. *Hard disk*
   * You are presented with three different options for a hard disk.  The first option, *Do not add a virtual hard disk*, will do as it says - it will *not* add a hard disk to this VM instance.  The second option, *Create a virtual hard disk now*, will allow you to customize a hard disk for the VM instance.  The third option, *Use an existing virtual hard disk file*, will allow you to attach an existing hard disk file to this VM.  In *most* instances you will choose the second option.  For this exercise choose the second option.
   * Click **Create**

7. *Hard disk file type*
   * Select the first option, *VDI (VirtualBox Disk Image)*
   * Click **Continue**

8. *Storage on physical hard disk*
   * You are now asked to choose a storage method for the hard disk file.  The first option, *Dynamically alocated*, will create a small file which will grow over time as more storage is used by the VM - up to the maximum size you give the hard disk (this will be the next step).  The second option, *Fixed size*, will instantly create a hard disk file on the host system with the size you tell it in the next step.  It is generally a good idea to select the first option, unless you have a valid reason for preallocating the entire hard disk.  For this exercis choose the first option.
   * Click **Continue**

9. *File location and size*
    * Leave the location of the hard disk file untouched.
    * For the size of the hard disk, move the slider all the way to the right (2.00 TB).  This is the maximum size allowed by Virtualbox.  Initially, the hard disk file size will be very small, but can grow up to a maximum of 2 TB or the current available room of the host storage - whichever is smaller.
    * Click **Create**

10. Make sure the VM is selected in the left panel, and then click **Settings**

11. *General*, *System*, *Display*, *Audio*, *Network*, *Ports*, *Shared Folders*, and *User Interface*
    * No changes are needed at this time.

12. *Storage*
    * Under *Storage Devices*, select *Empty* under *Controller: IDE*
    * Under *Attributes*, click the CD-ROM icon next to the entry for *Optical Drive*
    * Click *Choose/Create a Virtual Optical Disk*
    * Click *Add*
    * Locate and Choose the Ubuntu 20.04 Server ISO you downloaded earlier

13. Click **OK** to apply the settings.

14. Click **Start** to start the VM and begin the installation of Ubuntu 20.04 server.

During the installation, accept all of the default choices.  Use *test* as the username and hostname.  Use a valid password for the password.  Also, make sure to have it install *OpenSSH server* when it asks.  At the end of the installation, select *Reboot now* and then press *Enter* to remove the ISO from the CD-ROM drive.  Once the VM is restarted, you should be able to log into it using the aforementioned *test* user account.  If the UI for the VM is small, select *View > Scaled Mode" to enlarge.

### Enabling SSH to the Virtual Machine

SSH will allow the user to log into the VM from the host system as well as copy files to/from the host and VM.  Enabling SSH requires the user set up port fowarding.  To enable SSH, do the following:

1. Make sure the VM is selected in the Virtualbox list of VM's.

2. Click **Settings**

3. Click **Network**

4. Click **Adapter 1**, if it is not already opened.

5. Under **Advanced**, click the **Port Forwarding** button.

6. Click the green "+" to add a new rule.  For the new rule, enter the following:
   * Name: SSH
   * Protocol: TCP
   * Host IP: 127.0.0.1
   * Host Port: 2200
   * Guest IP: (leave blank)
   * Guest Port: 22

7. Click **OK** to exit the *Port Forwarding* dialog, and the click **OK** to apply the settings.

The SSH rule you just created uses port 2200 on your host system (which should be available).  This port can be any unused port on your host system above 1024.  We gave it 2200 as it closely resembles the standard SSH port of 22 to alleviate confusion.  In another tutorial, we will launch multiple VM's and as such we will need to create different host ports for SSH access since using 2200 for both would cause a collision.  The host IP of 127.0.0.1 is the standard IP address for the local host (in this case your host machine).  The guest IP is not needed, but can be filled in using the supplied IP address Virtualbox gives the VM for the NAT adapter.  Lastly, the guest port of 22 is the standard port the SSH listens on.

With the VM running, you should now be able to SSH to the VM from your local (host) system by doing the following:
```bash
$ ssh -p 2200 test@127.0.0.1
```

### Enabling a Shared Folder


