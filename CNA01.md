## Installing FusionComputeCNA01

Here’s how I set up FusionCompute CNA01:

1. **First, I installed VMware Workstation** and created a virtual machine with Ubuntu 24.
2. **I installed and configured Ubuntu** on the VM:
    - Booted from my USB flash drive and followed the installation wizard.
    - Picked English (US) for the keyboard layout.
    - Chose either Normal or Minimal installation, depending on my needs.
    - Selected to install Ubuntu alongside Windows when needed.
    - Set the time zone to Shanghai and created my user account.
    - Finished the installation, restarted the VM, and removed the USB drive when prompted.
3. **I upgraded Ubuntu** by running `sudo apt update` and `sudo apt upgrade` in the Terminal.
4. **Checked CPU virtualization support** with `egrep -c '(svm|vmx)' /proc/cpuinfo` to make sure virtualization was enabled in BIOS.
5. **Installed KVM and related packages** using `sudo apt install qemu qemu-kvm libvirt-bin bridge-utils virt-manager`, then rebooted.
6. **Configured networking**:
    - Used `virt-manager` to create a bridged network interface.
    - Set a static IP for the bridged NIC (like 192.168.100.1 for PC1).
    - Made sure the bridge starts on boot and picked the right physical NIC.
7. **Set up storage** in `virt-manager` by adding the FusionCompute ISO files under the Storage tab.
8. **Created and configured the FusionCompute CNA01 VM**:
    - Made a new VM and selected the FusionCompute CNA ISO.
    - Set at least 4096 MB RAM (I recommend 7168 MB), 3 CPUs, and a 200 GB disk (QCOW2 format).
    - Set the CPU model to `host-passthrough`.
    - Used VirtIO for the disk bus and set the NIC to bridged with device model `e1000`.
    - Assigned a static IP (like 192.168.100.11), set the gateway, and named the host `CNA01`.
    - Finished the installation and checked network connectivity.
9. **(Optional) Set up VRM and more CNA nodes**:
    - Repeated the VM creation steps for VRM (set memory to 3072 MB, CPUs to 4, disk name to VRM, IP to 192.168.100.20, hostname to VRM).
    - For extra CNA nodes (like CNA02), used unique disk names, VM names, IPs, and hostnames.
10. **Set up NFS shared storage**:
     - Installed NFS server with `sudo apt install nfs-kernel-server`.
     - Created and exported a shared directory for FusionCompute.
     - Restarted and enabled the NFS server.
11. **Accessed FusionCompute**:
     - Logged in via browser using the VRM IP address.
     - Used the default credentials (admin / IaaS@PORTAL-CLOUD8!) and followed the product documentation for further setup and testing.


![kvm](https://github.com/user-attachments/assets/ba315d75-7e33-40a6-87d8-d5ecdbffc450)