# Creating an Ubuntu 20.04 Server VM on Virtualbox

1. Prerequisites

* Virtualbox 6.x

2. Download Ubuntu 20.04 ISO
```bash
$ curl -O https://releases.ubuntu.com/20.04.4/ubuntu-20.04.4-live-server-amd64.iso
```

3. Start Virtualbox
4. Click **New**
5. *Name and operating system*
   * **Name** - Enter a name for the virtual machine (VM).  Note: this is *not* the hostname, but the name Virtualbox will refer to it as.
   * **Machine Folder** - The path where the VM files will be created.
   * **Type** - The general operating system type.  Select **Linux**.
   * **Version** - The vendor of the operating syste.  Select **Ubuntu (64-bit)**.
   * Click **Continue**
6. *Memory size*
   * Select the amount of memory you want to give the VM.  You are capped by the amount of physical memory that is on your host system.  Virtualbox will recommend a value given the oeprating system type and version.  For this exercise use the recommended value of **1024**.
   * Click **Continue**
7. *Hard disk*
   * You are presented with three different options for a hard disk.  The first option, *Do not add a virtual hard disk*, will do as it says - it will *not* add a hard disk to this VM instance.  The second option, *Create a virtual hard disk now*, will allow you to customize a hard disk for the VM instance.  The third option, *Use an existing virtual hard disk file*, will allow you to attach an existing hard disk file to this VM.  In *most* instances you will choose the second option.  For this exercise choose the second option.
   * Click **Create**
8. *Hard disk file type*
   * Select the first option, *VDI (VirtualBox Disk Image)*
   * Click **Continue**
9. *Storage on physical hard disk*
   * You are now asked to choose a storage method for the hard disk file.  The first option, *Dynamically alocated*, will create a small file which will grow over time as more storage is used by the VM - up to the maximum size you give the hard disk (this will be the next step).  The second option, *Fixed size*, will instantly create a hard disk file on the host system with the size you tell it in the next step.  It is generally a good idea to select the first option, unless you have a valid reason for preallocating the entire hard disk.  For this exercis choose the first option.
   * Click **Continue**
10. *File location and size*
    * Leave the location of the hard disk file untouched.
    * For the size of the hard disk, move the slider all the way to the right (2.00 TB).  This is the maximum size allowed by Virtualbox.  Initially, the hard disk file size will be very small, but can grow up to a maximum of 2 TB or the current available room of the host storage - whichever is smaller.
    * Click **Create**


