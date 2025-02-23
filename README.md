# proxmox-memo

## Create template (with cloud init image)

Ref: https://www.youtube.com/watch?v=MJgIm03Jxdo

This sample create Ubuntu 22.04

- Create virtual machine

    - General Tab
    ![General Tab](pics/pic1.png)
    <img src= "pics/pic1.png" alt="General Tab" style="border: 2px solid grey;">
        - VM ID = 900
        - Name = \<something\>-template

    - OS Tab
    <kbd>![OS Tab](pics/pic2.png)</kbd>
        - Check = Do not use any media
    
    - System Tab
    |![System Tab](pics/pic3.png)|
    -
        - Check = Qemu Agent
    
    - Disks Tab
    ![Disks Tab](pics/pic4-1.png)
    ![Disks Tab](pics/pic4-2.png)
        - Delete disk

    - CPU Tab
    ![CPU Tab](pics/pic5.png)

    - Memory Tab
    ![Memory Tab](pics/pic6.png)
        - Memory (MiB) = 1024

    - Network Tab
    ![Network Tab](pics/pic7.png)

    - Confirm Tab
    ![Confirm Tab](pics/pic8.png)

- Add cloud init to VM

    - Select template > Hardware
    ![](pics/pic2-1.png)

    - Add > CloudInit Drive
    ![](pics/pic2-2.png)

    - Storage = local-lvm
    ![](pics/pic2-3.png)

- CloudInit setting

    - Cloud-Init 
        - user = \<username\>
        - password = \<password\>
        - network > DHCP
        - SSH public key = \<copy paste\>
        ![](pics/pic3-1.png)

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

