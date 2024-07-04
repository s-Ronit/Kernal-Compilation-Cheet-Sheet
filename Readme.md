Debian Based Linux Kernel Compilation  (Ubuntu/Debian/Kali/Rpi)

This repository contanins some useful command to play around the Debian based linux kernel.

Check current Kernel present in your system.
uname -r
Sample Output
6.5.0-27-generic

Check List Of Installed Kernel Present On Your Machine
dpkg --list | grep linux-image

Sample Output:-

Do not confused between installed kernel and using kernal even it if different it will work.
![image](https://github.com/s-Ronit/Kernal-Compilation-Cheet-Sheet/assets/144111150/f423b08f-3dd5-4a1c-8914-fca0960c092b)

Now You need to download the lates linux kernel or the kernel whichever you want to use or compile in your system.
1. click here or folow the link https://github.com/torvalds/linux/tags
2. Download the required kernel. ex:-6.5.0-27-generic
3. Select your architecture (if youre not sure, then most likely you have a amd64 machine)
4. Download all 4 .deb packages (you can also do this from the terminal as follows)
5. mkdir -p v6.5.0-27 && cd v6.5.0-27    change this version accordingly
wget 'https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.0.1/amd64/linux-headers-6.0.1-060001-generic_6.0.1-060001.202210120833_amd64.deb'
wget 'https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.0.1/amd64/linux-headers-6.0.1-060001_6.0.1-060001.202210120833_all.deb'
wget 'https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.0.1/amd64/linux-image-unsigned-6.0.1-060001-generic_6.0.1-060001.202210120833_amd64.deb'
wget 'https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.0.1/amd64/linux-modules-6.0.1-060001-generic_6.0.1-060001.202210120833_amd64.deb'

6. Install downloaded packages
7. IF NO OTHER .deb files are there in your folder simply run
 sudo dpkg -i *.deb
 # ELSE dpkg -i <insert all 4 file names seperated by space> 

 dpkg --list | grep 6.0.1

 8. reboot
 9. On grub screen select advanced options for ubuntu where you will get multiple options.
 10. select your desired kernel
