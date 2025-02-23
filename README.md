# proxmox-memo

## Create template (with cloud init image)

Ref: https://www.youtube.com/watch?v=MJgIm03Jxdo

This sample create Ubuntu 22.04

- Create virtual machine

    - General Tab
    ![General Tab](pics/pic1.png)
        - VM ID = 900
        - Name = \<something\>-template

    - OS Tab
    ![OS Tab](pics/pic2.png)
        - Check = Do not use any media
    
    - System Tab
    ![System Tab](pics/pic3.png)
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

