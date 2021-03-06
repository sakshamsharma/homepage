<?php 
$markdown = <<<content

Running Windows inside Arch (and never having to leave Arch again)
========================

I am a die-hard Linux user, and yet, I used to have to boot up my Windows at times. I loathed that, I had to leave all my work, I missed the concept of workspaces, I missed the terminal.\n
At one point, I used to be an expert about Windows related troubles, and now I hardly ever open it. If you are thinking of doing that too, I'll list some reasons I have about not removing it altogether.

1. Visual Studio: Yes this is probably the only IDE I use (For Windows Phone App Dev for code.fun.do finals). The IDE is good enough, and, I pretty much don't have a choice.
2. Gaming: Well, I manage the occasional Counter Strike game with friends on my Linux itself, with Wine. But for games like GTA 5, you don't have any choice but to boot up Windows.
3. Proper phone support: It's possibly just me, but I have troubles with MTP for my android phone. Can be fixed.

Anyhow, here's about how to never have to boot out of Linux again: Wine + VirtualBox !\n

###Wine
This lets me run Counter Strike, small exe programs meant for small tasks, and the big boy Office 2010 right in my Linux. Agreed I don't use it so often, but it feels great to have this functionality.\n

###VirtualBox
The cure to the main trouble I had: Visual Studio. Run Windows inside your Linux. Boot up is faster (as this Windows just has things my Linux doesn't have, i.e. Visual Studio), and I get workspaces ! (I keep Windows on one workspace, and the rest of the work on another). Oh and works quite fast (although you need a good PC to be able to say this).\n
Without further ado, I'll show you how to get the same experience:\n

##Installing a Windows guest inside Arch Linux host
You would first have to check whether your processor supports Virtualization. Do it by TODO
You need to have Virtualization enabled in your BIOS (it wasn't in my case). To check this, do a `lsmod | grep kvm`. You should see a 'kvm' and a 'kvm_intel' or 'kvm_amd' modules there. If not, enable the setting in BIOS, the module should load then (assuming it was already installed, which it is in the default Linux kernel).

Here's a list of packages you need to install:

1. virtualbox
2. virtualbox-guest-utils
3. virtualbox-guest-modules
4. virtualbox-guest-dkms
5. virtualbox-host-dkms
6. virtualbox-host-modules
7. virtualbox-guest-iso
8. vboxguest-hook (AUR)

You might already have qt4, that would provide you with a GUI for VirtualBox too.\n

Now to add your user to the necessary groups:
`sudo gpasswd -a <user> vboxusers`\n
Make SURE you logout and login again after this command to make this take effect.\n

Now run this: `sudo dkms install vboxguest/4.3.28` (version as of 6/6/2015).\n

Also, you have to add the entry "vboxguest" to the array "HOOKS" inside /etc/mkinitcpio.conf\n

Now to loading necessary modules and services.
Here are the command I run the first time I have to open vbox after a fresh boot:

1. sudo modprobe vboxdrv vboxnetadp vboxnetflt vboxpci vboxvideo
2. VBoxClient-all
3. sudo systemctl start vboxservice

This should be all. Now Open up virtualbox, and create a new machine. I gave mine 4 GB RAM out of 8 and 3 processors out of 8. Next allocate harddisk space. I kept it on my home drive, 30 GB (its almost full now, with Visual Studio + Windows Phone taking up almost half of it).\n
Now if you have a DVD drive, insert a DVD of Windows 8 and then start the machine. It should boot from the drive (you must enable the drive access from the menu below).



content;
?>
