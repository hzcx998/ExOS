# ExOS

ExOS extends the [MIT exokernel](https://pdos.csail.mit.edu/archive/exo/) by removing the necessity to relink. Removing this process will allow consumers with no advanced computer knowledge better access to the OS. To achive this, the executable is scanned to identify system calls. Once they are identified, the native OS system calls are replaced with the appropriate ExOS userland system calls (from the LibOS). This replacement process is known as "live relinking".

***Before Working on ExOS, you should have a strong knowledge of the MIT Exokernel.***
 
## Goals

* Working OS  
* LibOSes for all 3 major OSes  
    * Windows  
    * Linux  
    * Mac OS X  
* Live relinking to allow unmodified programs to be run

## Short term work
* Garrett - in driver_bundle branch
	- [x] Define driver bundle format
	- [x] read grub (multiboot) module format
	- [ ] parse driver bundle
	- [ ] load drivers from bundle
	- [ ] init drivers
	- [ ] enumerate devices 
	
## Long term work
* Load files from floppy drives
* Some basic file systems support
* libC
	* probably from NewLib
* Decide on a format for the libOS
* live relinking or something
* Linux libOS
* Windows libOS
	* Possibly based on [ReactOS](https://www.reactos.org/)
* Mac OS X libOS

## Major systems to support
- [x] PCI - workingish
- [ ] PCI Express
- [ ] USB
- [ ] Text Graphics
- [ ] Regular Graphics
- [ ] Sound
- [ ] Ethernet
- [ ] WIFi
- [ ] SATA
- [ ] IDE
- [ ] SCSI (maybe probably)
- [ ] SAS
- [ ] M.2

## Helping out

### Contacting us
* [slack](https://join.slack.com/t/exos-dev/shared_invite/enQtMjI2OTE2NjYzOTU4LTJhZTIyOTNkYmY2MjcxN2RjZTUzZjhkYTAzZTNlOThkODZkZmE5ODI3ODA0MjBlNDY3Mjg3OWNjODQ0ZGM3NDU)
* Email
	* Garrett: garrett@garrettbattaglia.com
	* Oskari: xxc3ncoredxx@gmail.com (the typo is intentional)

### But, what can ***I*** do???
The best thing you can do is write code. If you know a system like the ones listed above, write a driver for it. If there's a bug that catches your fancy try and patch it. 

If you can't code theres still stuff for you. If you can write our readme or wiki might intrest you. You can run this and test it out. If you have an issue open a bug. 

## Building

### Precompilation steps

1. Build a GCC cross compiler
    * Must be GCC as I use some attributes that are only in GCC.
    * Must be for i686-elf.
    * See [os dev wiki](http://wiki.osdev.org/GCC_Cross-Compiler#Preparing_for_the_build) for more information.
2. Get a bootable medium
    * I'm using a 3.5" floppy but you can use a USB flashdrive or even a CD/DVD.
        * You can also use an emulator such as [Bochs](http://wiki.osdev.org/Bochs) or [QEMU](http://wiki.osdev.org/Qemu) to boot from a disk image.
    * If you're contributing ***please test on real hardware*** not just an emulator.
3. Set up a ***multiboot compliant*** bootloader
    * I'm using [grub legacy](http://wiki.osdev.org/GRUB_Legacy) as my bootloader but you can use whatever as long as it's ***multiboot compliant***. 
    * I'm not 100% sure that all of them work the more I look into it. I will try grub and see.
    * A new branch has been started to move to multiboot2 and modern grub. be prepared to change. 
4. Test the bootloader installation
    * Just boot to the bootloader's menu screen to make sure it works.
    
## Compilation

If everything went well in the precompilation stage, running `make all` should work. If you encounter issues at this stage, file an issue with the "bulding" tag (please include the build logs).
