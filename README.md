qemu-0.14.1-patches-for-gns3
============================

Patches to Qemu v0.14.1 needed to work with GNS3

Older Qemu releases v0.11.0 or v0.14.1 are better suited for running Cisco ASA on GNS3 than newest Qemu versions.
However, Qemu releases before version 1.1 must be patched to work with GNS3.
Patches can be downloaded from the following site:
http://www.gns3.net/qemu/

This repository includes all necessary patches to Qemu v0.14.1 needed to work with GNS3.
They include patches from http://www.gns3.net/qemu/, as well as additional new patches:

0001-qemu-0.14.1-fix-build-errors.patch - new patch which fixes build errors (tested on Ubuntu 14.04 64bit)

0002-qemu-0.14.1-udp.patch - combines all patches from http://www.gns3.net/qemu/

0003-qemu-0.14.1-monitor-udp.patch - new patch for new versions of GNS3 (after v1.2.2) needed to control running Qemu VMs

Instructions how to use these patches for Qemu v0.14.1 on a Linux PC:

1 - Uninstall other Qemu versions if they are present on your PC, for example by simple file removal:

cd /usr/local/bin

sudo rm qemu*

2 - Download the latest Qemu development tree:

git clone git://git.qemu-project.org/qemu.git

cd qemu

3 - Switch to older Qemu version v0.14.1 (create a new branch "qemu0141" at tag "v0.14.1"):

git checkout -b qemu0141 v0.14.1

4 - Download the patches and copy them to the newly created "qemu" directory:
 
cp 0001-qemu-0.14.1-fix-build-errors.patch path/to/qemu

cp 0002-qemu-0.14.1-udp.patch path/to/qemu

cp 0003-qemu-0.14.1-monitor-udp.patch path/to/qemu

5 - Apply the patches in the right order:

patch -p1 -i 0001-qemu-0.14.1-fix-build-errors.patch

patch -p1 -i 0002-qemu-0.14.1-udp.patch

patch -p1 -i 0003-qemu-0.14.1-monitor-udp.patch

6 - Build Qemu following instructions on the site:

http://wiki.qemu.org/Hosts/Linux

For example, for the recommended out-of-tree builds:

cd qemu

mkdir -p bin/release/native

cd bin/release/native

../../../configure --target-list=i386-softmmu

make

7 - Install Qemu (by default, Qemu binaries will be installed to /usr/local/bin):

sudo make install

8 - When using ASA in GNS3 with Qemu 0.14.1, configure the ASA device as follows:

Configure -> Network -> Check the checkbox "Use the legacy networking mode"

Then press "Apply" and "OK"

