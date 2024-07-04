# Debian Based Linux Kernel Compilation  (Ubuntu/Debian/Kali/Rpi)

This repository contanis some useful command to play around the Debian based linux kernel.

## Check current Kernal.
Check current kernel version.
   ```
   uname -r
   ```
Sample output
   ```bash
   6.5.0-27-generic
   ```
## List of Installed Kernel Present On Your Machine
   Debian Based Systems(Ubantu/Debian/Kali/Rpi)
   ```bash
   dpkg --list | grep linux-image
   ```
Sample Output:-

Do not confused between installed kernel and using kernal it can be different.

![image](https://github.com/s-Ronit/Kernal-Compilation-Cheet-Sheet/assets/144111150/f423b08f-3dd5-4a1c-8914-fca0960c092b)

## Now You need to download the latest linux kernel.
   Note:- Must download the same kernel whose header present in your system otherwise you may face difficulties at some point.
   ![image](https://github.com/s-Ronit/Kernal-Compilation-Cheet-Sheet/assets/144111150/dd2f1005-86d7-4a60-aca4-bfa3c745607d)
Follow the below steps:-
1. click [here](https://kernel.ubuntu.com/mainline/) to get all the linux kernel.
2. Download the latest kernel (6.0.1 in my case)
3. Select your architecture (if youre not sure, then most likely you have a amd64 machine)
4. Download all 4 .deb packages (you can also do this from the terminal as follows)
   ```bash
   mkdir -p v6.0.1 && cd v6.0.1
   wget 'https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.0.1/amd64/linux-headers-6.0.1-060001-generic_6.0.1-060001.202210120833_amd64.deb'
   wget 'https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.0.1/amd64/linux-headers-6.0.1-060001_6.0.1-060001.202210120833_all.deb'
   wget 'https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.0.1/amd64/linux-image-unsigned-6.0.1-060001-generic_6.0.1-060001.202210120833_amd64.deb'
   wget 'https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.0.1/amd64/linux-modules-6.0.1-060001-generic_6.0.1-060001.202210120833_amd64.deb'
   ```
5. Install the downloaded packages.
   ```bash
    # IF NO OTHER .deb files are there in your folder simply run
    sudo dpkg -i *.deb
    # ELSE dpkg -i <insert all 4 file names seperated by space> 
   ```
6. Confirm the installation by checking the list
   ```bash
    dpkg --list | grep 6.0.1
   ```

 7. reboot
 8. On grub screen you will see advance option in ubuntu where you will get multiple installed linux kernel options.
 9. select your desired kernel.
     
## Compiling Linux Kernel
This method has been adapted from [kernel compile notes](https://askubuntu.com/questions/718381/how-to-compile-and-install-custom-mainline-kernel/718662#718662) with few aditions based on personal experience.

1. Download the desired kernel from [here](https://github.com/torvalds/linux/tags)
   Note:- kernel version should match header version otherwise can you may face difficulties.
2. Move to the downloaded directory/folder.(In my case it is in the home directory of my system).
3. Unpack the tar ball
   ```bash
   #change the folder name with yours
   tar xvf linux-6.5.xz
   ```
4. Update System and Install Necessary Pacakage.
   ```bash
   sudo apt-get update
   sudo apt-get dist-upgrade
   sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison
   ```
5. Configure The Kernel
   ```bash
      cd linux-6.5
      # Copy existing configuration from current kernel
      cp /boot/config-$(uname -r) .config
   
      # (OPTIONAL) edit config using GUI menu
      make menuconfig
   
      # Ubuntu config file has full debugging. 
      # Makes an enormous kernel and takes twice as long to compile
      # (OPTIONAL) We can disable debug_info
      scripts/config --disable DEBUG_INFO
      
      # We also need to override certificate checking
      scripts/config --disable SYSTEM_TRUSTED_KEYS
      scripts/config --disable SYSTEM_REVOCATION_KEYS
   ```
6. Now Build Kernel and Modules.(here you can face some errors described in next step)
   ```bash
   # -j option specifies number of parallel jobs you want the process to use
   # nproc shows number of procesing units available
   # time records the time taken to compile it took me 95minutes
   time make -j $(nproc)
   
   # Install necessary modules
   time sudo make modules_install
   
   # Install Kernel
   sudo make install
   ```
7. On running command "sudo make install" you might face error.
   **error!!, Memetest86+ needs a 16-bit boot, that is not available on EFI, exiting.** (ignore it)
    ![image](https://github.com/s-Ronit/Kernal-Compilation-Cheet-Sheet/assets/144111150/e9ca3bb7-2201-4565-8237-f6e37188dc64)
8. install grub 
    ```bash
    #it should be installed still install it for safe side or you can ignore
    sudo grub-install
    ```
9. Update init frames
    ```bash
    sudo update-initramfs -c -k 6.0.7
    ```
10. Update grub
    ```bash
    sudo update-grub
    ```
12. Check weather grub loader is giving you advance options or not.if you are not getting grub advance options reboot the system you will get. 
    **image is just for representation. you will get your compiled kernel name.**
    
     ![ubuntu-recovery-mode2](https://github.com/s-Ronit/Kernal-Compilation-Cheet-Sheet/assets/144111150/2a7fbfc5-791e-45bd-b62e-d8b6a93f75c4)


13. Done !!

##   Modprobe
modprobe - Add and remove (enable/disable) modules from the Linux Kernel Syntax
   ```bash
   # enable
   modprobe <module_name>
   # disable
   modprobe -r <module_name>
   ```
## List of of active modules
   ```
   lsmod
   ```
