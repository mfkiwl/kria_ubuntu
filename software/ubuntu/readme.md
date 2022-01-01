# Ubuntu on Kria Vision AI Development Kit
This kit is sold with a non-standard Kria module that has the QSPI flash set as the only boot device and write protected.  This means that the kit cannot be booted in the standard way. Luckily, Xilinx and Ubuntu provide a boot image that can just be copied to an SD card to boot full Ubuntu Desktop Linux.

## Prepare SD Card

Look here:

        https://www.xilinx.com/products/som/kria/kv260-vision-starter-kit/kv260-getting-started-ubuntu/setting-up-the-sd-card-image.html

Get the image:

        wget https://people.canonical.com/~platform/images/xilinx/kria/iot-kria-classic-desktop-2004-x03-20211110-98.img.xz

Get Balena Etcher (It looks legitimate):

        https://www.balena.io/etcher/

and write the image to your SD card.

## Connect and Boot

Connect the usb, ethernet and power cables. 

Open a terminal emulator.  I like putty.

    sudo putty

port = /dev/ttyUSB1, baud = 115200, 8-none-1


You will get a login prompt, username=ubuntu, password=ubuntu. It will force you to change your password to something strong. You can change it again later to something easier.

It is a good idea to create a user for yourself and give it sudoer privileges.

    adduser myuser
    usermod -aG sudo myuser

I like to ssh into the board. 

Using the terminal, find the ip address of the zcu104.

    ip address

    ssh myuser@<ip address>

You can update Ubuntu

    sudo apt update
    sudo apt upgrade

You can start installing things.

    sudo apt install man
    sudo apt install subversion
    sudo apt intall git

Configure the PL side of the Zynq with an FPGA design.

    git clone https://github.com/hdlguy/kria_ubuntu.git

    cp ~/github/kria_ubuntu/fpga/implement/results/top.bit.bin to /lib/firmware. 

    sudo su

    echo top.bit.bin > /sys/class/fpga_manager/fpga0/firmware

    exit

Good luck.



