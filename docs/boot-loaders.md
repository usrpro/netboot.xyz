# Boot as iPXE Linux Kernel

The `netboot.xyz.lkrn` file can be booted as a Linux kernel from the bootloader.  This can be useful for providing a diagnostic tool as part of the OS or even having a quick option to reprovision the server on the fly.

### Extlinux

Edit /boot/extlinux.conf and add a simple entry:

    LABEL ipxe-boot
          kernel /boot/ipxe.lkrn
          initrd /boot/ipxe-config.ipxe

The kernel is treated as a Linux kernel and the initrd is treated as the iPXE script that is run once the kernel has loaded.

### Grub2

Copy the kernel file:

    cp netboot.xyz.lkrn /boot/netboot.xyz.lkrn

Edit `/etc/grub.d/40-custom`:

    #!/bin/sh
    exec tail -n +3 $0
    # This file provides an easy way to add custom menu entries.  Simply type the
    # menu entries you want to add after this comment.  Be careful not to change
    # the 'exec tail' line above.
    menuentry "Netboot.xyz loader" {
        linux /netboot.xyz.lkrn
    }


