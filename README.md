# Introduction
  * The Kernel version 4.12.0-rc1 was based on Ubuntu mainline build to have a better experience.
  * [Mainline build](http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.12-rc1/)
  * Unlike UP board, this kernel should work for other CherryTrail tablets and laptops, because LattePanda focused on the Atmel MCU and developed it.
  * This repository could be cooperative. Any comments and suggestions will be appreciated.

# z8350 based platform

* Enivorment
  * Testing OS on LattePanda(4G/64G):
  * Ubuntu 16.04.2 64Bit LTS 
  * GCC version 5.4.0 20160609

* Patch:
  * WiFi (rtl8723bs directory and in Tree)
  * Bluetooth (rtl8723bs_bt directory)
  * Audio (ucm directory)
  * PWM (in Tree)

* BIOS:
  * South Bridge -> Chipset -> SCC Configuration
    * SCC SDIO Support -> PCI Mode

* If you want to build your own kernel step-by-step, there are steps as follows:
-------------------------------------------------------------------------------------------
  * 1. Install Ubuntu 16.04.2 ISO from Ubuntu official website, make sure that installation is only in UEFI boot mode.
  * 2. modify GRUB_CMDLINE_LINUX_DEFAULT="quiet splash intel_idle.max_cstate=1" to /etc/default/grub, it will prevent system freezing.
  * 3. In the terminal, sudo apt-get update
  * 4. sudo apt-get dist-upgrade
  * 5. sudo apt-get install git
  * 6. git clone this repository.
  * 7. cd in
  * 8. make mrproper
  * 9. make upboard_defconfig
  * 10. make -j4
  * 11. sudo make modules_install
  * 12. sudo make firmware_install
  * 13. sudo make headers_install
  * 14. sudo make install
  * 15. patch UCM configuration file to /usr/share/alsa/ucm/chtrt5645
  * 16. build rtl8723bs_bt dirver
  * 17. move binary to /usr/sbin
  * 18. add systemd service rtl8723bsbt.service
  * 19. link BT service for all users
  * 20. patch BT and WiFi firmware to /lib/firmware

  * p.s. 
  * If you see warnings as follows:
    * W: Possible missing firmware /lib/firmware/i915/kbl_dmc_ver1_01.bin for module i915
    * W: Possible missing firmware /lib/firmware/i915/kbl_guc_ver9_14.bin for module i915
    * W: Possible missing firmware /lib/firmware/i915/bxt_guc_ver8_7.bin for module i915

    * Download and install firmwares, but assume that CherryTrail is not involved in the firmwares.
    * [Intel firmwares](https://01.org/linuxgraphics/downloads/firmware)

  * 21. reboot and play. You could edit your grub menu to roll back original kernel.
-------------------------------------------------------------------------------------------

* If you want to install the kernel and apply all steps, there are steps as follows:
-------------------------------------------------------------------------------------------
  * z8350 directory: (split files)
  * Prebuilt Linux kernel, modules and steps by a DEB file, it is easy to install.
  * 1. merge the split files to get a DEB file, cd in package directory.
  * 2. cat lattepanda-64-mainline_4.12.0-rc1-1_amd64.deb.parta* > lattepanda-64-mainline_4.12.0-rc1-1_amd64.deb
  * 3. sudo dpkg -i lattepanda-64-mainline_4.12.0-rc1-1_amd64.deb
  * 4. reboot your LattePanda to take effect.
-------------------------------------------------------------------------------------------

# z8300 based platform

* Enivorment
  * Testing OS on LattePanda(4G/64G):
  * Ubuntu 16.04.2 64Bit LTS 
  * GCC version 5.4.0 20160609

* Patch:
  * (BT ID is BCM2E95)
  * WiFi (bcm43340 directory and in Tree)
  * Bluetooth (bcm34430_bt directory and in Tree)
  * Audio (ucm directory)
  * PWM (in Tree)

* If you want to build your own kernel step-by-step, there are steps as follows:
-------------------------------------------------------------------------------------------
  * 1. Install Ubuntu 16.04.2 ISO from Ubuntu official website, make sure that installation is only in UEFI boot mode.
  * 2. modify GRUB_CMDLINE_LINUX_DEFAULT="quiet splash intel_idle.max_cstate=1" to /etc/default/grub, it will prevent system freezing.
  * 3. In the terminal, sudo apt-get update
  * 4. sudo apt-get dist-upgrade
  * 5. sudo apt-get install git
  * 6. git clone this repository.
  * 7. cd in
  * 8. make mrproper
  * 9. make upboard_defconfig
  * 10. make -j4
  * 11. sudo make modules_install
  * 12. sudo make firmware_install
  * 13. sudo make headers_install
  * 14. sudo make install
  * 15. patch UCM configuration file to /usr/share/alsa/ucm/chtrt5645
  * 16. add systemd service bcm43340bt.service
  * 17. link BT service for all users
  * 18. patch BT and WiFi firmware to /lib/firmware

  * p.s. 
  * If you see warnings as follows:
    * W: Possible missing firmware /lib/firmware/i915/kbl_dmc_ver1_01.bin for module i915
    * W: Possible missing firmware /lib/firmware/i915/kbl_guc_ver9_14.bin for module i915
    * W: Possible missing firmware /lib/firmware/i915/bxt_guc_ver8_7.bin for module i915

    * Download and install firmwares, but assume that CherryTrail is not involved in the firmwares.
    * [Intel firmwares](https://01.org/linuxgraphics/downloads/firmware)

  * 19. reboot and play. You could edit your grub menu to roll back original kernel.
-------------------------------------------------------------------------------------------

* If you want to install the kernel and apply all steps, there are steps as follows:
-------------------------------------------------------------------------------------------
  * z8300 directory: (split files)
  * Prebuilt Linux kernel, modules and steps by a DEB file, it is easy to install.
  * 1. merge the split files to get a DEB file, cd in package directory.
  * 2. cat lattepanda-z8300-64-mainline_4.12.0-rc1-1_amd64.deb.parta* > lattepanda-z8300-64-mainline_4.12.0-rc1-1_amd64.deb
  * 3. sudo dpkg -i lattepanda-z8300-64-mainline_4.12.0-rc1-1_amd64.deb
  * 4. reboot your LattePanda to take effect.
-------------------------------------------------------------------------------------------

# For Debian 8 (Jessie)
  * Please refer to [Debian 8 installation](https://github.com/mopplayer/lattepanda-mainline-4.11/issues/1)
