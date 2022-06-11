# OTUS7_GREP
Homework

В GUI Vinbox, на моменте выбора операционной системы, нажал e. Попал в меню изменения настроек загрузки системы.
Замечание: в этом меню я удалил записи "no_timer_chek console=tty0 console=ttyS0,115200n8 net.ifnames=0 biosdevname=0 elevator=noop crashkernel=auto LANG=en_US.UTF-8". В противном случае при добавлении строки init=/bin/sh - система вылетала в ошибку kernel panic, rd.break не срабатывал - система грузилась в обычном варианте.
После удаления этих записей в варианте с init=/bin/sh система показывала, что пароль изменен, но после этого ни под одним пользователем авторизоваться не получалось - слетала авторизация даже с пользователя vagrant
В варианте rw init=/sysroot/bin/sh ситуация такая же как с init=/bin/sh.

Вариант с rd.break сработал
Перемонтировал систему
moubt -o remount,rw / sysroot
chroot /sysroot
passwd root
touch /.autorelabel
После этого система загрузилась не до конца, переразметились все файлы. Система перезагрузилась, я зашел под root с новым паролем.

В целом, удобно. Удобней, чем сносить пароли на винде при помощи загрузочной флешки и замены cmd на sethc.exe)


Vagrantfile скопировал из урока 3 - LVM
Добавил в скрипт, устанавливающий ПО lvm и wget

Изменил название VolGroup00 на VolRoot
vgrename VolGroup00 VolRoot

Изменил параметры в /etc/fstab, /etc/default/grub, /boot/grub2/grub.cfg и перезагрузился
Вывод команды vgs верный:
[root@lvm ~]# vgs
  VG      #PV #LV #SN Attr   VSize   VFree
  VolRoot   1   2   0 wz--n- <38.97g    0

Создал файлы скриптов и загрузил их в свой гит.
Создал папку 01test и скачал скрипты туда
mkdir /usr/lib/dracut/modules.d/01test
wget https://raw.githubusercontent.com/Vozmen/OTUS7_GREP/main/module-setup.sh -O /usr/lib/dracut/modules.d/01test/module-setup.sh
wget https://raw.githubusercontent.com/Vozmen/OTUS7_GREP/main/test.sh -O /usr/lib/dracut/modules.d/01test/test.sh

Пересобрал образ initrd
dracut -f -v

Команда lsinitrd -m /boot/initramfs-$(uname -r).img | grep test дала вывод test
Отредактировал grub.cfg и перезагрузился
При загрузке увидел пингвинчика, запись приложена.

Скриптом установил проги, создал папку и скачал в неё скирпты, остальное руками