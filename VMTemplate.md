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

    - Select Template VM > Hardware
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

    - Select template VM > Hardware > Unused Disk 0 > Edit > Check = Discard > Check = Advanced > Check = SSD emulation > Add
    <kbd>![](pics/pic5-1.png)</kbd>
    <kbd>![](pics/pic5-2.png)</kbd>
    <kbd>![](pics/pic5-3.png)</kbd>

    - Option > Boot Order
    <kbd>![](pics/pic5-4.png)</kbd>
    <kbd>![](pics/pic5-5.png)</kbd>

    - Start at boot = yes
    <kbd>![](pics/pic5-6.png)</kbd>

- Convert to template

    <kbd>![](pics/pic6-1.png)</kbd>

- Create VM from template (test)

    - Clone
    <kbd>![](pics/pic7-1.png)</kbd>

    - 
        - VM ID = 799
        - Mode = Full Clone
        - Name = ubuntu-test
    <kbd>![](pics/pic7-2.png)</kbd>

    - Console
    <kbd>![](pics/pic7-3.png)</kbd>
    