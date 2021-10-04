# Arch_installation
This codes is excuted  AFTER you partition using the DOS partition table MBR-(non -EFI) your hard-drive into three main partitions first partition MUST be the BOOT partition the second MUST be the ROOT partition and the third is your home partition I used cfdisk -utility for partitioning the hard-drive.
# install Archlinux

Steps of Arch install

ping google.com
timedatectl set-ntp true
timedate status
fdisk -l ---list the name of hard drive
use cfdisk or fdisk --to make sda1(ext4-boot-500M), ada2(swap-same size of pc ram) sda3(ext4-root)
Format the sda1 and sda3 to filesystem ext4
mkfs.etx4 /dev/sda1
mkfs.ext4 /dev/ada3
Make swap partition in sda2
mkswap /dev/sda2
swapon /dev/sda2
mount /dev/sda3 /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
nano /etc/pacman.d/mirrorlist --delete all non usa mirrors by ctl+k
Installing the linux-kernel
--------------------------
pacstrap /mnt base linux linux-firmware
genfstab -U /mnt >> /mnt/etc/fstab
arch-chroot /mnt
ln -sf /usr/share/zoneinfo/America/New_York /etc/localtime
hwclock --systohc
nano /etc/locale.gen --uncomment the line en_us.UTF-8
locale-gen
pacman -S nano vim sudo
nano/etc/locale.conf --type the following then save LANG=en_us.UTF-8
nano /etc/hostname  --type any host nam you likee, example:arefvbox
nano /etc/hosts --type exactly the following
127.0.0.1  localhost
::1        localhost
127.0.1.1 arefvbox.localdomain arefvbox
passwd   ---create root password
useradd -m newusername  ---adding standard user example:aref
we adding the user aref to the following groups by typing the following command:-
usermod -aG wheel,audio,video,lp,optical,storage aref
EDITOR=nano visudo  ---using nano instead visudo
uncomment the line # % wheel=ALL(All) ALL
Install grub and configure grub-install
---------------------------------------
pacman -S grub
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
installing network
-------------------
pacman -S networkmanager wpa_supplicant wireless_tools iw netctl
pacman -S dialog
systemctl NetworkManager
exit
umount -l /mnt
reboot
after log in succesfully as standard user
install xorg
sudo pacman -S xorg
lspci   ----to know your display card manufacture
intel-display-driver
sudo pacman -S xf86-video-intel
Amd-display-driver
sudo pacman -S xf86-video-amdgpu
Nvidia-display-driver
sudo pacman -S xf86-video-nouveau
Ati-display-driver
sudo pacman xf86-video-ati
unveral-display-diver
sudo pacman -S xf86-video-vesa
installing lxdm display-manager
sudo pacman -S lxde ---this will install the lxde-desktop and the lxdm-disply-manager

Enable the lxdm-display-manager at startup-vey-important-step:
-------------------------------------------------------------
sudo systemctl enable lxdm
reboot-done

