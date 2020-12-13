
# Table of Contents

1. [Install Arch](#org6beafd4)
    1. [Define keymaps:](#org25b9e4f)
    2. [Internet conection](#orgcba797c)
    3. [Update clock](#org7fc94c9)
    4. [Partition disks:](#orgf25512e)
    5. [Installation:](#org11216fa)
    6. [Configure the system:](#orgb2b3bfe)
    7. [Finish:](#org9f7ca20)
2. [Post Instalation](#org6c45a34)
    1. [sudo localectl set-x11-keymap latam](#org2aea4a6)
    2. [NetworkManager setup:](#orga538d2d)
    3. [Install:](#org3983cac)
    4. [Install graphic drivers:](#org2dd1009)
    5. [Install xorg:](#org2b007fb)
    6. [Install a display manager or xorg-init to start xorg](#orgd97e25f)
    7. [Install AUR:](#org9e9a4fd)
    8. [Clone dotfiles:](#org2888b5f)
    9. [Audio:](#orge5742f5)
    10. [Printer:](#org65e75b7)
3. [Links:](#orgff3faeb)
    1. [Installation:](#org7c2b67a)
    2. [Xorg:](#org63d8dbf)
    3. [Lightdm:](#org1bbfd89)
    4. [Printer:](#org8730836)

# Introduction

The elements <u>*marked with italic and underline is where you need to change stuff*</u>

# Install Arch

## Define keymaps

- List aviable keymaps:
ls /usr/share/kbd/keymaps/**/*.map.gz | less

- Select keymaps:
loadkeys <u>*la-latin1*</u>

## Internet conection

- Wlan:  
  - Check if wlan isn't down:  
    - rfkill list
    - rfkill unblock <u>*device*</u>
  - Connect to wifi:  
    - iwctl (interactive promt)  
      - device list
      - station <u>*device*</u> scan
      - station <u>*device*</u> get-networks
      - station <u>*device*</u> connect <u>*SSID*</u>
      - CTR-d (to exit)

    > Use USB tethering for first installation if wifi driver don't work

## Update clock

- timedatectl set-ntp true

## Partition disks

- List disks:  
  - fdisk -l
- Partition disk:  
    create a primary partition of 550M for EFI and give 'EFI System' type  
    creae a primary partition of 2G for swap and give 'Linux swap' type  
    create a primary partition of desire size for /root  
  - fdisk <u>*device*</u>
    > Use m for help

- format partitions:  
  - mkfs.fat -F32 <u>*partition*</u> for EFI
  - mkswap <u>*partition*</u> for swap partition
  - mkfs.ext4 <u>*partition*</u> for root partition
- Mount partitions:  
  - mount <u>*partition*</u> /mnt for /root
  - swapon <u>*partition*</u> for swap

## Installation

- Install escential packages:  
  - pacstrap /mnt base linux linux-firmware  
    > here you can add more packages appendig to pacstrap with a space of difference

## Configure the system

- Generate Fstab:  
  - genfstab -U /mnt >> /mnt/etc/fstab
- chroot (change root)  
  - arch-chroot /mnt
  > Here you will enter the new installed system
- set time zone:  
  - ln -sf /usr/share/zoneinfo/<u>*REGION</u>/<u>*CITY*</u> /etc/localtime  
    > To get REGION and CITY list with `ls` the previous folders
  - hwclock -systohc
- Localization:  
  - edit /etc/locale.gen and uncomment the locales needed
  - locale-gen
  - create /etc/locale.conf and set:  
    - LANG=<u>*LANG*</u>  
        > where <u>*LANG*</u> is the first column of the uncomment line in the previous step
  - make keyboard layout persistent creating /etc/vconsole.conf:  
    - KEYMAP=<u>*LAYOUT*</u>
        > where <u>*LAYOUT*</u> is the layout selected
- Network configuration:  
  - Create /etc/hostname  

    ```Text
        myhostname
    ```

    > where <u>*myhostname*</u> is the actual hostname

  - edit /etc/host and add the following lines  

    ```Text
    127.0.0.1    localhost
    ::1          localhost
    127.0.1.1    myhostname.localdomain myhostname  
    ```

    > Where myhostname is the hostname define in the previous step
    > If a static ip address is used the use that instead of 127.0.1.1
- Change root password:  
  - passwd
- Add user:  
  - Create user:
    useradd -m <u>*username*</u>
  - Change user password:
    passwd <u>*username*</u>
  - Assing basic group to user:
    usermod -aG wheel,audio,video,optical,storage <u>*username*</u>
  - Install sudo and add the user:  
    - pacman -S sudo
    - EDITOR=<u>*EDITOR*</u> visudo  
        > where <u>*EDITOR*</u> is the text editor of your choice
    - uncomment "%wheel ALL=(ALL) ALL"
- Install grub boot manager:  
  - pacman -S grub
  - if you're using an UEFI system
    - pacman -S efibootmgr dosfstools os-prober mtools
    - mkdir /boot/EFI
    - mount <u>EFI_PARTITION*</u> /boot/EFI
    - grub-install -taget=x86_64-efi -bootloader-id=grub_uefi -recheck
  - grub-mkconfig -o /boot/grub/grub.cfg
- Networking:  
  - An easy and widely used program to setup internet connection is network manager
  pacman -S networkmanager
  systemctl enable NetworkManager
  > Pay attention to the capital letters.

## Finish

- Exit chroot:
    exit
- Umount the root partition
    umount /mnt
    > use -l if shows "target is busy"
- Finish installation and enter the system:
    reboot
    > Don't forget to remove the installation media!

# Post Instalation

- Set lenguaje:
 sudo localectl set-x11-keymap <u>*latam*</u>


## NetworkManager setup

- For WiFi connections:
  - nmcli device wifi list
  - nmcli decive wifi connect <u>*SSID*</u> password <u>*PASSWORD*</u>  
    > In case the network is hidden just add "hidden" at the end

<a id="org3983cac"></a>

## Basic software needed

Here are some software that every linux machine need, with a couple of option in no particular order.

- Terminal emulator
  - gnome-terminal
- Text Editor  
  - vim
  - nano
- Web Browser  
  - firefox
- Desktop Environment or Window Manager:  
  - i3
  - i3-gasp

## Install graphic drivers

- for Intel:  
  - Install xf86-video-intel with pacman
  - by a comment in youtube do this instead:  
    > open/create  /etc/X11/xorg.conf.d/20-intel.conf
    > and type:
    >
    > ```Text
    > Section "Device"
    >   Identifier  "Intel Graphics"
    >   Driver      "modesetting"
    > EndSection
    > ```
    >
    > now restart the pc.
    > to check if settings are applied, type: inxi -G
    > and look for driver: modesetting
    > one more note: you can use  --needed to avoid reinstalling the existing pkgs in a group:
    > pacman -S base-devel --needed

    >i actually didn't need this but i wanted to leave it here just in case.

## Install graphical environment

sudo pacman -S xorg

## Install a display manager or xorg-init to start xorg

A display manager will let you choose witch Desktop environment or Window Manager to launch at login time.

- for xinit:  

  > Important! I didn't try this personally yet.

  - Install xinit:
  sudo pacman -S xorg-init
  - Copy the default configuration:
  cp *etc/X11/xinit/xinitrc ~*.xinitrc
  - edit .xinitrc file:  
    - delete evething after fi
    - add the program to execute on start of X  
    - Add the DE or WM like: exec <u>*DE / WM*</u>
      > For software that you need to run onm the background just type the name and give '&' at the end
  - reboot
  - starx  
    > this is only to test if everething is ok
  - On ~/.bash_profile append:
  `[[ $(fgconsole 2>dev/null) == 1]] && exec startx -- vt1`

- Install Lighdm:  
  A window manager and xorg need to be installed beforehand
  - Install lightdm and a greeter of preference ([check the Arch Wiki](https://wiki.archlinux.org/index.php/LightDM#Greeter) for some greeter options):
  sudo pacman -S lightdm lightdm-gtk-greeter  
  
  - edit /etc/lightdm/lightdm.conf  uncomment and edit `greetar-session=lightdm-gtk-greeter` with the greeter you choose. 
    > You need to edit the one under [Seat:*], the first lines are examples.
    > The list of greeters is on /usr/share/xgreeters directory
  - test configuration:  
    lightdm -test-mode -debug
  - enable lightdm as service:
    sudo systemctl enable lightdm

## Multi Monitor Setup

Xorg can handle the monitor detection and setup for you, but if you want a special setup you have to do some configuration.

For this there are 2 options: execute a xrandr command on login or have a xorg.conf file. I find best combine both so i can have the right configuration when lightdm launch, but if you use xinit execute a xrandr command from your WM or DE is recomendable.

> Usually DE can handle this in their configuration.
> If you're using a WM and want a graphical application to see the configuration arandr is a good option.

- Setup:
  - Create /etc/X11/xorg.conf.d/10-monitor.conf and add:

    ```Text
      Section "Monitor"
        Identifier "HDMI1"
        Option "Primary" "true"
      EndSection

      Section "Monitor"
        Identifier "eDP1"
        Option "RightOf" "HDMI1"
      EndSection
    ```

  - [Modify lightdm config:](https://wiki.archlinux.org/index.php/LightDM#LightDM_displaying_in_wrong_monitor)
    - If you're using gtk greeter:
    Edit /etc/lightdm/lightdm-gtk-greeter.conf
    > Not personally tested!

    ```Text
    [greeter]
    active-monitor=0
    ```

    - Else:
    Edit /etc/lightdm/lightdm.conf

    ```Text
    display-setup-script=xrandr --output OUTPUT --primary
    ```

    > Replace OUTPUT with the desire monitor, you can check this with xrandr -q command

  - Handle changes in monitors:
    If you're using a laptop and change frequently the number of monitors you're using, you can install autorandr and save layouts, when you connect/disconnect outputs arandr will change xorg config automatically with a saved layout (you can even trigger some custom script when the outputs change!).

## Install AUR

The Arch User Repository (AUR) is a community-driven repository for Arch users. ([Arch Wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository)), it's not mandatory but it's useful to have.

- Install some packages needed:
  sudo pacman -S base-devel git
- Clone the yay repository:
  git clone <https://aur.archlinux.org/yay-git.git>
- Compile yay:
  cd yay-git
  makepkg -si

## Audio

- If audio don't work well try this (in this order):  
  1. pulseaudio -start
  2. set this config in /etc/pulse/daemon.conf  

      ```Text
      flat-volumes = no
      deferred-volume-safety-margin-usec = 1
      ```

## Printer

To print something the cups service is needed.

- Download the right drivers:  
  - splix: drivers for Samsung.
  - hplip: drivers for HP.
  - gutenprint: drivers for Canon, Epson, Lexmark, Sony y Olympus.
  - cups-pdf: drivers for PDF printer.
- add user to lpadmin group  
  sudo usermod -aG lpadmin <u>*user*</u>
- Edit /etc/cups/cups-files.conf and add the user to systemGroup

  ```Text
  SystemGroup sys root wheel lpadmin
  ```

- Start cups service and enable it  
  sudo systemctl enable org.cups.cupsd.service -now
- Reboot to be sure everthing loads up
- Open system-config-printer and set up the printer

## Power Settings

[ArchWiki](https://wiki.archlinux.org/index.php/Power_management) [Arch Cheetsheet](https://archcheatsheet.com/environment/power-management.html)

# Links

## Installation

- <https://www.youtube.com/watch?v=PQgyW10xD8s&list=WL&index=5&t=1486s>

## Xorg

- <https://www.youtube.com/watch?v=pouX5VvX0_Q&list=WL&index=6&t=249s>

## Lightdm

- <https://linoxide.com/linux-how-to/install-lightdm-arch-linux/>
- <https://mundo-tips.com/como-configurar-lightdm-en-arch-linux/>

## Printer

- <http://aurumlinux.com/instalar-una-impresora-en-arch-linux/>
- <https://gorauskas.org/linux/arch/ArchPrintingSetup>
