# proxmox-memo

## Create template (with cloud init image)

Ref: https://www.youtube.com/watch?v=MJgIm03Jxdo

This sample create Ubuntu 22.04

- Create virtual machine

    - General Tab
    <kbd>![General Tab](pics/pic1.png)</kbd>
        - VM ID = 900
        - Name = \<something\>-template

    - OS Tab
    <kbd>![OS Tab](pics/pic2.png)</kbd>
        - Check = Do not use any media
    
    - System Tab
    <kbd>![System Tab](pics/pic3.png)|</kbd>
        - Check = Qemu Agent
    
    - Disks Tab
    <kbd>![Disks Tab](pics/pic4-1.png)</kbd>
    <kbd>![Disks Tab](pics/pic4-2.png)</kbd>
        - Delete disk

    - CPU Tab
    <kbd>![CPU Tab](pics/pic5.png)</kbd>

    - Memory Tab
    <kbd>![Memory Tab](pics/pic6.png)</kbd>
        - Memory (MiB) = 1024

    - Network Tab
    <kbd>![Network Tab](pics/pic7.png)</kbd>

    - Confirm Tab
    <kbd>![Confirm Tab](pics/pic8.png)</kbd>

- Add cloud init to VM

    - Select template > Hardware
    <kbd>![](pics/pic2-1.png)</kbd>

    - Add > CloudInit Drive
    <kbd>![](pics/pic2-2.png)</kbd>

    - Storage = local-lvm
    <kbd>![](pics/pic2-3.png)</kbd>

- CloudInit setting

    - Cloud-Init 
        - user = \<username\>
        - password = \<password\>
        - network > DHCP
        - SSH public key = \<copy paste\>
        <kbd>![](pics/pic3-1.png)</kbd>

- Proxmox console

    ```
    # wget https://cloud-images.ubuntu.com/minimal/releases/jammy/release/ubuntu-22.04-minimal-cloudimg-amd64.img
    ```
    Ref: https://cloud-images.ubuntu.com/minimal/releases/jammy/release/

    ```
    # qm set 900 --serial0 socket --vga serial0
    ```
    900 is proxmox template VM id 

    ```
    # mv ubuntu-22.04-minimal-clouding-amd64.img ubuntu-22.04.qcow2
    # qemu-img resize ubuntu-22.04.qcow2 32G
    # qm importdisk 900 ubuntu-22.04.qcow2 local-lvm
    ```

- Set template


