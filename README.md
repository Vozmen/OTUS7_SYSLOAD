# OTUS7_GREP
Homework

� GUI Vinbox, �� ������� ������ ������������ �������, ����� e. ����� � ���� ��������� �������� �������� �������.
���������: � ���� ���� � ������ ������ "no_timer_chek console=tty0 console=ttyS0,115200n8 net.ifnames=0 biosdevname=0 elevator=noop crashkernel=auto LANG=en_US.UTF-8". � ��������� ������ ��� ���������� ������ init=/bin/sh - ������� �������� � ������ kernel panic, rd.break �� ���������� - ������� ��������� � ������� ��������.
����� �������� ���� ������� � �������� � init=/bin/sh ������� ����������, ��� ������ �������, �� ����� ����� �� ��� ����� ������������� �������������� �� ���������� - ������� ����������� ���� � ������������ vagrant
� �������� rw init=/sysroot/bin/sh �������� ����� �� ��� � init=/bin/sh.

������� � rd.break ��������
�������������� �������
moubt -o remount,rw / sysroot
chroot /sysroot
passwd root
touch /.autorelabel
����� ����� ������� ����������� �� �� �����, ��������������� ��� �����. ������� ���������������, � ����� ��� root � ����� �������.

� �����, ������. �������, ��� ������� ������ �� ����� ��� ������ ����������� ������ � ������ cmd �� sethc.exe)


Vagrantfile ���������� �� ����� 3 - LVM
������� � ������, ��������������� �� lvm � wget

������� �������� VolGroup00 �� VolRoot
vgrename VolGroup00 VolRoot

������� ��������� � /etc/fstab, /etc/default/grub, /boot/grub2/grub.cfg � ��������������
����� ������� vgs ������:
[root@lvm ~]# vgs
  VG      #PV #LV #SN Attr   VSize   VFree
  VolRoot   1   2   0 wz--n- <38.97g    0

������ ����� �������� � �������� �� � ���� ���.
������ ����� 01test � ������ ������� ����
mkdir /usr/lib/dracut/modules.d/01test
wget https://raw.githubusercontent.com/Vozmen/OTUS7_GREP/main/module-setup.sh -O /usr/lib/dracut/modules.d/01test/module-setup.sh
wget https://raw.githubusercontent.com/Vozmen/OTUS7_GREP/main/test.sh -O /usr/lib/dracut/modules.d/01test/test.sh

���������� ����� initrd
dracut -f -v

������� lsinitrd -m /boot/initramfs-$(uname -r).img | grep test ���� ����� test
�������������� grub.cfg � ��������������
��� �������� ������ �����������, ������ ���������.

�������� ��������� �����, ������ ����� � ������ � �� �������, ��������� ������