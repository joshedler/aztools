# aztools
Tools (e.g. scripts) for working with Azure VMs

# Prepare a generic Linux VM

[Preping a VM for Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/upload-vhd#option-1-upload-a-vhd)

Don't forget to setup the VM Kernel to be ready for Azure!


1. Edit the "modules" file located in `/etc/initramfs-tools` using this command:
    * `sudo vi /etc/initramfs-tools/modules`
2. Add the following lines:
    ```
    hv_vmbus
    hv_storvsc
    hv_blkvsc
    hv_netvsc
    ```
3. Save and exit.
4. Run the following commands to re-initialize the “modules” file:
    * `sudo update-initramfs –u`
5. Reboot the virtual machine by executing the below command in Shell:
    * `sudo shutdown -r now`


# Convert a VMware VMDK disk and convert it to Azure VHD

```
$ ~/dev/aztools/az-vmdx-convert -i Kali-Linux-2019.3-vmware-amd64.vmdk -o Kali-Linux-2019.3-amd64

qemu-img:              /usr/bin/qemu-img
jq:                    /usr/bin/jq


-rw-r--r-- 1 josh josh 81G Oct 11 13:32 Kali-Linux-2019.3-amd64.raw
RAW file Kali-Linux-2019.3-amd64.raw exists; it will be re-used as-is unless manually deleted.
Press [Enter] to continue or [Ctrl]-C to abort: 

Raw disk current size:  81G
Raw disk target size:   81G

Raw file appears to have been resized to 81G.

-rw-r--r-- 1 josh josh 81G Oct 11 13:37 Kali-Linux-2019.3-amd64.vhd
VHD file Kali-Linux-2019.3-amd64.vhd exists; it will be re-used as-is unless manually deleted.
Press [Enter] to continue or [Ctrl]-C to abort: 

VHD file Kali-Linux-2019.3-amd64.vhd is ready to upload to Azure.
```
