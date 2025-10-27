Pavel Sibirenko
# 1 месяц
## 1 урок
**Домашнее задание** <ins>"Обновление ядра системы"</ins>

Цель: научиться обновлять ядро в ОС Linux;

🎯**Задание
1.Запустите ВМ c Ubuntu.
2.Обновите ядро ОС на новейшую стабильную версию из mainline-репозитория.
3.Оформите отчет в README-файле в GitHub-репозитории.**
<details>
<summary> = Теория = </summary>
- Репозитории Ubuntu
- В Ubuntu всё программное обеспечение делится на четыре секции, называемые компонентами,
 чтобы отразить разницу в лицензии и уровне доступной поддержки.
- Пакеты распределяются по компонентам таким образом:
- Main – свободное ПО, официально поддерживаемое компанией Canonical. 
- Restricted – проприетарное ПО (в основном — драйверы устройств), официально поддерживаемое компанией Canonical. 
- Universe – свободное ПО, официально не поддерживаемое компанией Canonical (но поддерживаемое сообществом пользователей). 
- Multiverse – проприетарное ПО, не поддерживаемое компанией Canonical. 
 
- Существует четыре основных репозитория Ubuntu.
- $release1) – это пакеты на момент выхода релиза. 
- $release-security – пакеты критических обновлений безопасности. 
- $release-updates – пакеты обновления системы (т.е. более поздние версии ПО, вышедшие уже после релиза). 
- $release-backports – бэкпорты более новых версий некоторого ПО, которое доступно только в нестабильных версиях Ubuntu. 
- partner – репозиторий содержищий ПО компаний-партнеров Canonical.
  
- Кроме официальных, существует множество репозиториев от авторов программ и от тех, кто не поленился собрать из исходников пакет и поделиться им с другими. Launchpad предлагает создавать PPA-репозитории — Personal Package Archive, обычно небольшой репозиторий, в который его хозяин складывает исходники, а пользователи на выходе получают уже готовый deb-пакет.
- Подключение репозитория
- Репозитории Ubuntu содержат большое количество программ, однако существуют программы, отсутствующие в репозиториях Ubuntu, и возможно, Вы хотели бы их использовать. Существует много сторонних репозиториев, подключив которые Вы получите доступ к дополнительному ПО. Сделать это можно как при помощи графического интерфейса, так и в консоли.
- Некоторые репозитории помимо нужных Вам пакетов могут содержать экспериментальные сборки различного системного ПО, в том числе и ядер linux. Т.к. версия этих экспериментальных пакетов как правило выше, чем установленная у Вас, Менеджер обновлений может попытаться «обновить» систему с этих репозиториев, что в свою очередь может повредить Вашу систему. Поэтому внимательно читайте описание подключаемого репозитория и информацию в Менеджере обновлений.

- Что такое mainline-ядро

- Ubuntu по умолчанию использует ядра, которые поддерживаются Canonical (обычно LTS + security-patches).
- Иногда нужно поставить новое ядро (например, для поддержки нового «железа» или драйверов).
- Для этого есть отдельный репозиторий Ubuntu Mainline Kernel — там выкладываются пакеты с «чистыми» ядрами от kernel.org, собранные под Ubuntu.
 
- Есть два способа обновить ядро: вручную или через утилиту mainline.

- **1. Ручная установка**
- Перейди на официальный репозиторий:  https://kernel.ubuntu.com/mainline/
- Выбери нужную версию (например, v6.12.41/).
- Скачайте .deb пакеты для своей архитектуры (обычно amd64):
- linux-headers-...all.deb
- linux-headers-...amd64.deb
- linux-image-unsigned-...amd64.deb
- linux-modules-...amd64.deb
  
- Установите их:

- sudo dpkg -i *.deb
  
- После перезагрузки система загрузится с новым ядром.

- **2. С помощью утилиты mainline (удобнее)**
- Есть GUI/CLI-программа для управления mainline-ядрами.

- Установка:

- sudo add-apt-repository ppa:cappelikan/ppa
- sudo apt update
- sudo apt install mainline
   
Запуск:

- mainline --list   # список доступных ядер
- mainline --install 6.10.5   # установка ядра

- **Важно**
- Mainline-ядра не поддерживаются Canonical официально, их используют «на свой риск».
- Если что-то пойдет не так, всегда  загрузиться со старого ядра (оно остаётся в меню GRUB).*
</details>

**Выполнение домашнего задания:**
- spg@ol-alp-ubuntu1:~$ uname -r
- 6.8.0-79-generic
- spg@ol-alp-ubuntu1:~$ cat /proc/version
- Linux version 6.8.0-79-generic (buildd@lcy02-amd64-049) (x86_64-linux-gnu-gcc-13 (Ubuntu 13.3.0-6ubuntu2~24.04) 13.3.0, GNU ld (GNU Binutils for Ubuntu) 2.42) #79-Ubuntu SMP PREEMPT_DYNAMIC Tue Aug 12 14:42:46 UTC 2025
- spg@ol-alp-ubuntu1:~$ sudo add-apt-repository ppa:cappelikan/ppa
- spg@ol-alp-ubuntu1:~$ sudo su
- root@ol-alp-ubuntu1:/home/spg#
- apt update
- Scanning linux images...

- Running kernel seems to be up-to-date.
- mainline --list
- mainline 1.4.13
- Notice: "--list" has been renamed to "list"
- Updating Kernels...
- -----------------------
- Available Kernels...
- -----------------------
- 6.16.4
- 6.16.3
- 6.16.2
- 6.16.1
- 6.16
- 6.15.11
-  ...
- mainline --install 6.10.5
- mainline 1.4.13
Notice: "--install" has been renamed to "install"
Updating Kernels...
Downloading 6.10.5
Installing 6.10.5
sh: 1: pkexec: not found
- spg@ol-alp-ubuntu1:~$ sudo apt update
- sudo apt install policykit-1
- sudo su
- mainline --install 6.10.5
- ...update-initramfs:
-  Generating /boot/initrd.img-6.10.5-061005-generic...
- reboot
- spg@ol-alp-ubuntu1:~$ uname -r
- 6.10.5-061005-generic

## 2 Урок
**Домашнее задание**
<ins>Работа с mdadm</ins>

**Цель:** научиться использовать утилиту для управления программными RAID-массивами в Linux;

🎯**Задание
Запустите ВМ c Ubuntu.
 Добавьте в виртуальную машину несколько дисков
•	Соберите RAID-0/1/5/10 на выбор
•	Сломайте и почините RAID
•	Создайте GPT таблицу, пять разделов и смонтируйте их в системе.**

<details>
<summary> = Теория = </summary>
  mdadm — это утилита в Linux для работы с программными RAID-массивами (software RAID). Она позволяет создавать, управлять и проверять RAID на уровне ОС, без аппаратного контроллера.

🔹 Основные возможности mdadm
	•	Создание RAID-массивов (0, 1, 4, 5, 6, 10 и др.).
	•	Добавление/удаление дисков.
	•	Восстановление массива после сбоя.
	•	Мониторинг состояния RAID.
	•	Сборка массива при загрузке системы.
 
🔹 Основные команды
1. Проверить доступные массивы
- cat /proc/mdstat
2. Создать массив (например RAID1 из 2 дисков)
  - sudo mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc
  - /dev/md0 — имя RAID-массива
  - --level=1 — тип RAID (зеркалирование)
  - --raid-devices=2 — количество дисков
/dev/sdb /dev/sdc — сами диски
3. Проверить состояние массива
- sudo mdadm --detail /dev/md0
4. Добавить новый диск в массив
- sudo mdadm --add /dev/md0 /dev/sdd
5. Удалить диск из массива
  - sudo mdadm --remove /dev/md0 /dev/sdb
6. Остановить массив
- sudo mdadm --stop /dev/md0
  
🔹 Автосборка при загрузке
Чтобы RAID автоматически собирался после перезагрузки:
- sudo mdadm --detail --scan >> /etc/mdadm/mdadm.conf
  
⚠️ Важно:
	•	Перед использованием очисти диски от старых RAID-метаданных:
- sudo mdadm --zero-superblock /dev/sdX
- **Используй только новые/пустые диски, иначе потеряешь данные.**
- Для постоянного хранения данных массив нужно ещё отформатировать и смонтировать (например в ext4).

**Как сделать автосборку RAID после перезагрузки (mdadm)**
	1.	Проверить, что RAID работает сейчас  
- cat /proc/mdstat
- Ты должен увидеть свой массив, например:
- md0 : active raid1 sdb1[0] sdc1[1]
	2.	Убедиться, что mdadm.conf содержит описание массива
- Сохраняем конфиг RAID:
- sudo mdadm --detail --scan >> /etc/mdadm/mdadm.conf
- Проверь содержимое:
- cat /etc/mdadm/mdadm.conf
- Там должна быть строка вроде:
- ARRAY /dev/md0 metadata=1.2 name=server:0 UUID=xxxxxxxx:yyyyyyyy:zzzzzzzz
	3. Обновить initramfs (чтобы система собирала RAID при загрузке)
- Для Debian/Ubuntu:
- sudo update-initramfs -u
- Для CentOS/RHEL:
- sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
	4. Добавить запись в fstab (если массив монтируется)
- Узнай UUID раздела:
- sudo blkid /dev/md0
- Допустим, UUID=1111-2222
- Тогда добавь в /etc/fstab строку:
- UUID=1111-2222   /mnt/raid   ext4   defaults   0   0
- (замени ext4 на твою файловую систему и /mnt/raid на точку монтирования).
	5. Проверка
- Перезагрузи сервер.
- Выполни:
- cat /proc/mdstat
- RAID должен собраться автоматически.
- Убедись, что файловая система смонтирована:
- df -h
- ⚡ Важные моменты
- Если один диск выйдет из строя, массив всё равно поднимется, но в degraded-состоянии.
- Чтобы система присылала уведомления об ошибках, в mdadm.conf  настроить email-оповещения:  
</details>

**Выполнение домашнего задания:**

- Добавлено 2 диска по 25ГБ.
- Перезагружена машина
- **root@ol-alp-ubuntu1:/home/spg#fdisk -l**
- **Disk /dev/sda: 30 GiB**, 32212254720 bytes, 62914560 sectors
- Disk model: Virtual disk
- Units: sectors of 1 * 512 = 512 bytes
- Sector size (logical/physical): 512 bytes / 512 bytes
- I/O size (minimum/optimal): 512 bytes / 512 bytes
- Disklabel type: gpt
- Disk identifier: 8D9F226A-26B4-4BCB-B1D9-1A25308F5904

 -Device       Start      End  Sectors Size Type
 -/dev/sda1     2048     4095     2048   1M BIOS boot
 -/dev/sda2     4096  4198399  4194304   2G Linux filesystem
 -/dev/sda3  4198400 62912511 58714112  28G Linux filesystem


- **Disk /dev/sdb: 25 GiB**, 26843545600 bytes, 52428800 sectors
- Disk model: Virtual disk
- Units: sectors of 1 * 512 = 512 bytes
 -Sector size (logical/physical): 512 bytes / 512 bytes
 -I/O size (minimum/optimal): 512 bytes / 512 bytes


- **Disk /dev/sdc: 25 GiB**, 26843545600 bytes, 52428800 sectors
- Disk model: Virtual disk
- Units: sectors of 1 * 512 = 512 bytes
- Sector size (logical/physical): 512 bytes / 512 bytes
- I/O size (minimum/optimal): 512 bytes / 512 bytes

- **root@ol-alp-ubuntu1:/home/spg# mdadm --zero-superblock --force /dev/sd{b,c}** # обнуляем супербюлоки
- mdadm: Unrecognised md component device - /dev/sdb
- mdadm: Unrecognised md component device - /dev/sdc

- **root@ol-alp-ubuntu1:/home/spg# mdadm --create --verbose /dev/md0 -l 1 -n 2 /dev/sd{b,c}** # Создаем RAID1 из двух наших дисков
- mdadm: Note: this array has metadata at the start and
-    may not be suitable as a boot device.  If you plan to
-    store '/boot' on this device please ensure that
-    your boot-loader understands md/v1.x metadata, or use
-    --metadata=0.90
- mdadm: size set to 26196992K
- Continue creating array? y
- mdadm: Defaulting to version 1.2 metadata
- mdadm: **array /dev/md0 started**.
- **root@ol-alp-ubuntu1:/home/spg# cat /proc/mdstat** # проверка RAID
- Personalities : [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
- md0 : active raid1 sdc[1] sdb[0]
- 26196992 blocks super 1.2 [2/2] [UU]
- [===================>.]  resync = 96.9% (25406848/26196992) finish=0.0min speed=206724K/sec
-
- unused devices: <none>
- **root@ol-alp-ubuntu1:/home/spg# mdadm -D /dev/md0**
- /dev/md0:
- Version : 1.2
- Creation Time : Mon Sep  8 12:30:54 2025
- Raid Level : raid1
- Array Size : 26196992 (24.98 GiB 26.83 GB)
- Used Dev Size : 26196992 (24.98 GiB 26.83 GB)
- Raid Devices : 2
- Total Devices : 2
- Persistence : Superblock is persistent
- Update Time : Mon Sep  8 12:33:04 2025
- State : clean
- Active Devices : 2
- Working Devices : 2
- Failed Devices : 0
- Spare Devices : 0
- Consistency Policy : resync
- Name : ol-alp-ubuntu1:0  (local to host ol-alp-ubuntu1)
- UUID : fb759b8b:cfc4115e:f806dd32:0d7e6930
- Events : 17
- Number   Major   Minor   RaidDevice State
- 	0       8       16        0      active sync   /dev/sdb
- 	1       8       32        1      active sync   /dev/sdc
- **root@ol-alp-ubuntu1:/home/spg# mdadm /dev/md0 --fail /dev/sdc** # "ломаем" диск 1 в RAID-е md0
- mdadm: set /dev/sdc faulty in /dev/md0
- **root@ol-alp-ubuntu1:/home/spg#mdadm -D /dev/md0** # проверяем
- Number   Major   Minor   RaidDevice State
- 0       8       16        0      active sync   /dev/sdb
- 0        0        1      removed
- 1       8       32        -      faulty   /dev/sdc
- **root@ol-alp-ubuntu1:/home/spg# mdadm /dev/md0 --remove /dev/sdc** # удаляем "сломанный диск" из массива md0
- mdadm: hot removed /dev/sdc from /dev/md0
- "заменили" диск на новый (**Нужно ли быть уверенным, что на новом нет никакой информации, чтобы не повредить данные на md0?**)
- **root@ol-alp-ubuntu1:/home/spg# mdadm /dev/md0 --add /dev/sdc** # добавляем "новый исправный" диск в наш массив
mdadm: added /dev/sdc
- **root@ol-alp-ubuntu1:/home/spg# cat /proc/mdstat** # Процесс rebuild-а
- Personalities : [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
- md0 : active raid1 sdc[2] sdb[0]
- 26196992 blocks super 1.2 **[2/1] [U_]**
- [=======>.............]  recovery = **36.8%** (9652352/26196992) finish=1.3min speed=206294K/sec
- **root@ol-alp-ubuntu1:/home/spg# cat /proc/mdstat**
- Personalities : [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
- md0 : active raid1 sdc[2] sdb[0]
- 26196992 blocks super 1.2 **[2/1] [U_]**
- [=============>.......]  recovery = **68.3%** (17907840/26196992) finish=0.6min speed=200041K/sec
- unused devices: <none>
- **root@ol-alp-ubuntu1:/home/spg# cat /proc/mdstat**
- Personalities : [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
- md0 : active raid1 sdc[2] sdb[0]
- 26196992 blocks super 1.2 **[2/2] [UU]** # Готово!
- unused devices: <none>
- parted -s /dev/md0 mklabel gpt

  
- **root@ol-alp-ubuntu1:/home/spg# fdisk /dev/md0**

- Welcome to fdisk (util-linux 2.39.3).
- Changes will remain in memory only, until you decide to write them.
- Be careful before using the write command.

- Command (m for help): **p** # показать таблицу разделов
- Disk /dev/md0: 24.98 GiB, 26825719808 bytes, 52393984 sectors
- Units: sectors of 1 * 512 = 512 bytes
- Sector size (logical/physical): 512 bytes / 512 bytes
- I/O size (minimum/optimal): 512 bytes / 512 bytes
- Disklabel type: gpt
- Disk identifier: 590C44E9-EC0D-4A26-BC53-E5775ACF2E02 

- Device     Start      End  Sectors Size Type
- /dev/md0p1  2048 10479615 10477568   5G Linux filesystem

- Command (m for help): **d** # удаляем раздел md0p1
- Selected partition 1
- Partition 1 has been deleted.

- Command (m for help): **p** # проверяем
- Disk /dev/md0: 24.98 GiB, 26825719808 bytes, 52393984 sectors
- Units: sectors of 1 * 512 = 512 bytes
- Sector size (logical/physical): 512 bytes / 512 bytes
- I/O size (minimum/optimal): 512 bytes / 512 bytes
- Disklabel type: gpt
- Disk identifier: 590C44E9-EC0D-4A26-BC53-E5775ACF2E02

- Command (m for help): **quit**

- **root@ol-alp-ubuntu1:/home/spg# parted -s /dev/md0 mklabel gpt** #создает новую таблицу разделов GPT
- **root@ol-alp-ubuntu1:/home/spg# parted /dev/md0 mkpart primary ext4 0% 20%**
- **root@ol-alp-ubuntu1:/home/spg# parted /dev/md0 mkpart primary ext4 20% 40%**
- **root@ol-alp-ubuntu1:/home/spg# parted /dev/md0 mkpart primary ext4 40% 60%**
- **root@ol-alp-ubuntu1:/home/spg# parted /dev/md0 mkpart primary ext4 60% 80%**
- **root@ol-alp-ubuntu1:/home/spg# parted /dev/md0 mkpart primary ext4 80% 1000%**



- Information: You may need to update /etc/fstab.

- **root@ol-alp-ubuntu1:/home/spg# parted /dev/md0** # проверяем

- GNU Parted 3.6
- Using /dev/md0
- Welcome to GNU Parted! Type 'help' to view a list of commands.
- (parted) mklabel gpt
- Warning: The existing disk label on /dev/md0 will be destroyed and all data on this disk will be lost. Do you
- want to continue?
- Yes/No? **Y**
- (parted) **print**
- Model: Linux Software RAID Array (md)
- Disk /dev/md0: 26.8GB
- Sector size (logical/physical): 512B/512B
- Partition Table: gpt
- Disk Flags:

- Number  Start  End  Size  File system  Name  Flags

- (parted) **mkpart primary ext4 0% 20%**
- (parted) **mkpart primary ext4 20% 40%**
- (parted) **mkpart primary ext4 40% 60%**
- (parted) **mkpart primary ext4 60% 80%**
- (parted) **mkpart primary ext4 80% 100%**
- (parted) **print**
- Model: Linux Software RAID Array (md)
- Disk /dev/md0: 26.8GB
- Sector size (logical/physical): 512B/512B
- Partition Table: gpt
- Disk Flags:

- Number  Start   End     Size    File system  Name     Flags
- 1      1049kB  5366MB  5365MB  ext4         primary
- 2      5366MB  10.7GB  5365MB  ext4         primary
- 3      10.7GB  16.1GB  5366MB  ext4         primary
- 4      16.1GB  21.5GB  5365MB  ext4         primary
- 5      21.5GB  26.8GB  5365MB  ext4         primary

- (parted) **quit**
- Information: You may need to update /etc/fstab.

- **root@ol-alp-ubuntu1:/home/spg# for i in $(seq 1 5); do sudo mkfs.ext4 /dev/md0p$i; done** # форматируем разделы в ext4
- mke2fs 1.47.0 (5-Feb-2023)
- Creating filesystem with 1309696 4k blocks and 327680 inodes
- Filesystem UUID: 92eca3f1-12d7-49ce-be6a-733e609bb7d7
- Superblock backups stored on blocks:
- 32768, 98304, 163840, 229376, 294912, 819200, 884736

- Allocating group tables: done
- Writing inode tables: done
- Creating journal (16384 blocks): done
- Writing superblocks and filesystem accounting information: done

- mke2fs 1.47.0 (5-Feb-2023)
- Creating filesystem with 1309696 4k blocks and 327680 inodes
- Filesystem UUID: 6f5c3479-02a4-4ed2-a7aa-026f09ccef68
- Superblock backups stored on blocks:
- 32768, 98304, 163840, 229376, 294912, 819200, 884736

- Allocating group tables: done
- Writing inode tables: done
- Creating journal (16384 blocks): done
- Writing superblocks and filesystem accounting information: done
 
- mke2fs 1.47.0 (5-Feb-2023)
- Creating filesystem with 1309952 4k blocks and 327680 inodes
- Filesystem UUID: 5c870d58-bc00-444b-a417-c5c5d1282f7b
- Superblock backups stored on blocks:
- 32768, 98304, 163840, 229376, 294912, 819200, 884736

- Allocating group tables: done
- Writing inode tables: done
- Creating journal (16384 blocks): done
- Writing superblocks and filesystem accounting information: done
- **root@ol-alp-ubuntu1:/home/spg# vi /etc/fstab** # монтирование при загрузке ОС
- dev/disk/by-uuid/92eca3f1-12d7-49ce-be6a-733e609bb7d7 /mnt/raid/part1 ext4 defaults 0 0
- /dev/disk/by-uuid/6f5c3479-02a4-4ed2-a7aa-026f09ccef68 /mnt/raid/part2 ext4 defaults 0 0
- /dev/disk/by-uuid/5c870d58-bc00-444b-a417-c5c5d1282f7b /mnt/raid/part3 ext4 defaults 0 0
- /dev/disk/by-uuid/f93c1908-34a8-46af-90d5-16822484d597 /mnt/raid/part4 ext4 defaults 0 0
- /dev/disk/by-uuid/353739df-06c1-4c27-bd64-e42ee243599c /mnt/raid/part5 ext4 defaults 0 0

- **root@ol-alp-ubuntu1:/home/spg# reboot** # перегружаем ОС и проверяем
- **spg@ol-alp-ubuntu1:~$ df -k**
- Filesystem                        1K-blocks    Used Available Use% Mounted on
- tmpfs                                201536    1188    200348   1% /run
- /dev/mapper/ubuntu--vg-ubuntu--lv  14339080 5001468   8587432  37% /
- tmpfs                               1007672       0   1007672   0% /dev/shm
- tmpfs                                  5120       0      5120   0% /run/lock
- **/dev/md127p3**                       5071520      24   4793124   1% /mnt/raid/part3
- **/dev/md127p4**                        5070496      24   4792152   1% /mnt/raid/part4
- **/dev/md127p1**                        5070496      24   4792152   1% /mnt/raid/part1
- **/dev/md127p2**                        5070496      24   4792152   1% /mnt/raid/part2
- **/dev/md127p5**                        5070496      24   4792152   1% /mnt/raid/part5
- /dev/sda2                           1992552  101928   1769384   6% /boot
- tmpfs                                201532      16    201516   1% /run/user/1000
  
- **root@ol-alp-ubuntu1:/# ls -hal /mnt/raid**
- total 28K
- drwxr-xr-x 7 root root 4.0K Sep  8 13:31 .
- drwxr-xr-x 3 root root 4.0K Sep  8 13:31 ..
- drwxr-xr-x 4 root root 4.0K Sep  9 11:40 part1
- drwxr-xr-x 3 root root 4.0K Sep  8 13:19 part2
- drwxr-xr-x 3 root root 4.0K Sep  8 13:19 part3
- drwxr-xr-x 3 root root 4.0K Sep  8 13:19 part4
- drwxr-xr-x 3 root root 4.0K Sep  8 13:19 part5

  
## 3 и 4 Урок

**Домашнее задание**
<ins>Работа с LVM</ins>

**Цель:** Научиться создавать и управлять логическими томами в LVM;

🎯**Задание**
1. Настроите LVM в Ubuntu 24.04 Server
2. Создайте Physical Volume, Volume Group и Logical Volume
3. Отформатируйте и смонтируйте файловую систему
4. Расширьте файловую систему за счёт нового диска
5. Выполните resize
6. Проверьте корректность работы**

<details>
<summary> = Теория = </summary>
- LVM (Logical Volume Manager) в Linux — это прослойка между «железными» дисками и файловой системой. Она позволяет удобно управлять дисками:
- объединять, делить, увеличивать и перемещать тома «на лету».

🧩 Основные элементы LVM
- 	1	Physical Volume (PV) — физический носитель (например, /dev/sdb, /dev/sdc), подготовленный для LVM.
- 	2	Volume Group (VG) — группа томов. Это как «пул» памяти, в который складываются PV.
- 	3	Logical Volume (LV) — логический том (раздел внутри VG). На него накатывается файловая система, и монтируется в систему.

🔧 Пример работы с LVM (Ubuntu)
- 	1 Подготовить диски под LVM
- Допустим, у тебя есть два пустых диска /dev/sdb и /dev/sdc:
- sudo pvcreate /dev/sdb /dev/sdc
- 2 Создать группу томов
- sudo vgcreate vg_data /dev/sdb /dev/sdc
- Теперь у тебя есть VG с именем vg_data
- 3 Создать логический том
- Например, том размером 50 ГБ:
- sudo lvcreate -L 50G -n lv_storage vg_data
- Или занять всё доступное пространство:
- sudo lvcreate -l 100%FREE -n lv_storage vg_data
- 4 Создать файловую систему
- sudo mkfs.ext4 /dev/vg_data/lv_storage
- 5 Смонтировать в каталог
- sudo mkdir /mnt/storage
- sudo mount /dev/vg_data/lv_storage /mnt/storage
  🔄 Полезные операции с LVM
- 	•	Посмотреть PV, VG и LV:
- sudo pvs
- sudo vgs
- sudo lvs
- Увеличить том (и файловую систему):
- sudo lvextend -L +10G /dev/vg_data/lv_storage
- sudo resize2fs /dev/vg_data/lv_storage
- Уменьшить том (опасно, нужно сначала уменьшить ФС):
- sudo resize2fs /dev/vg_data/lv_storage 20G
- sudo lvreduce -L 20G /dev/vg_data/lv_storage
- Удалить логический том:
- sudo umount /mnt/storage
- sudo lvremove /dev/vg_data/lv_storage
- Удалить группу томов:
- sudo vgremove vg_data
- Удалить физический том:
- sudo pvremove /dev/sdb
- 
- ⚡ Плюсы LVM
- •	Масштабируемость ( увеличивать/уменьшать тома).
- •	Гибкость (несколько дисков объединяются в одно пространство).
- •	Snapshots (снимки томов для бэкапов).
- •	Удобное управление ( переносить данные между дисками).





 
</details>


**Выполнение домашнего задания:**

- Добавлено 2 диска по 25ГБ (cтало 5 дисков: 1 - система, 2 - raid, 2 - новые
- Перезагружена машина
- **root@ol-alp-ubuntu1:~# lsblk**
- NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINTS
- sda                         8:0    0   30G  0 disk
- ├─sda1                      8:1    0    1M  0 part
- ├─sda2                      8:2    0    2G  0 part  /boot
- └─sda3                      8:3    0   28G  0 part
-   └─ubuntu--vg-ubuntu--lv 252:0    0   14G  0 lvm   /
- sdb                         8:16   0   25G  0 disk
- └─md127                     9:127  0   25G  0 raid1
-   ├─md127p1               259:0    0    5G  0 part  /mnt/raid/part1
-   ├─md127p2               259:1    0    5G  0 part  /mnt/raid/part2
-   ├─md127p3               259:2    0    5G  0 part  /mnt/raid/part3
-   ├─md127p4               259:3    0    5G  0 part  /mnt/raid/part4
-   └─md127p5               259:4    0    5G  0 part  /mnt/raid/part5
- sdc                         8:32   0   25G  0 disk
- └─md127                     9:127  0   25G  0 raid1
-   ├─md127p1               259:0    0    5G  0 part  /mnt/raid/part1
-   ├─md127p2               259:1    0    5G  0 part  /mnt/raid/part2
-   ├─md127p3               259:2    0    5G  0 part  /mnt/raid/part3
-   ├─md127p4               259:3    0    5G  0 part  /mnt/raid/part4
-   └─md127p5               259:4    0    5G  0 part  /mnt/raid/part5
- sdd                         8:48   0   25G  0 disk
- sde                         8:64   0   25G  0 disk
- sr0                        11:0    1  3.1G  0 rom
- **root@ol-alp-ubuntu1:~# cat /proc/mdstat** # посмотрим на наш массив, его нужно разобрать для домашнего задания (нужно 4 диска)
- Personalities : [raid1] [raid0] [raid6] [raid5] [raid4] [raid10]
- md127 : active raid1 sdb[0] sdc[2]
- root@ol-alp-ubuntu1:~# umount /dev/md127p1
- root@ol-alp-ubuntu1:~# umount /dev/md127p2
- root@ol-alp-ubuntu1:~# umount /dev/md127p3
- root@ol-alp-ubuntu1:~# umount /dev/md127p4
- root@ol-alp-ubuntu1:~# umount /dev/md127p5
- **root@ol-alp-ubuntu1:~# umount /dev/md127**
- umount: /dev/md127: not mounted.
- **root@ol-alp-ubuntu1:~# mdadm --stop /dev/md127**
- mdadm: stopped /dev/md127
- **root@ol-alp-ubuntu1:~# lsblk**
- NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
- sda                         8:0    0   30G  0 disk
- ├─sda1                      8:1    0    1M  0 part
- ├─sda2                      8:2    0    2G  0 part /boot
- └─sda3                      8:3    0   28G  0 part
-   └─ubuntu--vg-ubuntu--lv 252:0    0   14G  0 lvm  /
- **sdb                         8:16   0   25G  0 disk**
- **sdc                         8:32   0   25G  0 disk**
- **sdd                         8:48   0   25G  0 disk**
- **sde                         8:64   0   25G  0 disk**
- sr0                        11:0    1  3.1G  0 rom
- **# теперь у нас 4 свободных диска для ДЗ**
- **root@ol-alp-ubuntu1:~# lvmdiskscan**
-  /dev/sda2 [       2.00 GiB]
-  /dev/sda3 [     <28.00 GiB] LVM physical volume
-  /dev/sdd  [      25.00 GiB]
-  /dev/sde  [      25.00 GiB]
-  2 disks
-  1 partition
-  0 LVM physical volume whole disks
-  1 LVM physical volume
-  **# нет 2-х дисков (не подготовлены для LVM (PV), т.к. размечены под ext4**
- **root@ol-alp-ubuntu1:~# wipefs -a /dev/sdb** # удаляем старую разметку (сотрет данные)
- /dev/sdb: 4 bytes were erased at offset 0x00001000 (linux_raid_member): fc 4e 2b a9
- **root@ol-alp-ubuntu1:~# wipefs -a /dev/sdc** # удаляем старую разметку (сотрет данные)
- /dev/sdc: 4 bytes were erased at offset 0x00001000 (linux_raid_member): fc 4e 2b a9
- **root@ol-alp-ubuntu1:~# lvmdiskscan** # проверяем
-  /dev/sda2 [       2.00 GiB]
-  /dev/sda3 [     <28.00 GiB] LVM physical volume
-  **/dev/sdb  [      25.00 GiB]**
-  **/dev/sdc  [      25.00 GiB]**
-  **/dev/sdd  [      25.00 GiB]**
-  **/dev/sde  [      25.00 GiB]**
-  4 disks
-  1 partition
-  0 LVM physical volume whole disks
-  1 LVM physical volume
-  **root@ol-alp-ubuntu1:~# pvcreate /dev/sdb** # разметим диск для будущего использования LVM - создадим PV
-  Physical volume "/dev/sdb" successfully created
-  **root@ol-alp-ubuntu1:~# vgcreate otus /dev/sdb** # создаем первый уровень абстракции - VG
-  Volume group "otus" successfully created
-  **root@ol-alp-ubuntu1:~# lvcreate -l+80%FREE -n test otus** # создаем Logical Volume (LV)
-  Logical volume "test" created.
-  **root@ol-alp-ubuntu1:~# vgdisplay otus**
-  --- Volume group ---
-  VG Name               otus
-  System ID
-  Format                lvm2
-  Metadata Areas        1
-  Metadata Sequence No  2
-  VG Access             read/write
-  VG Status             resizable
-  MAX LV                0
-  Cur LV                1
-  Open LV               0
-  Max PV                0
-  Cur PV                1
-  Act PV                1
-  VG Size               <25.00 GiB
-  PE Size               4.00 MiB
-  Total PE              6399
-  Alloc PE / Size       5119 / <20.00 GiB
-  Free  PE / Size       1280 / 5.00 GiB
-  VG UUID               jCugMC-ZHcJ-muKG-FqI5-XiQr-aACB-Us9wMV
-  **root@ol-alp-ubuntu1:~# vgdisplay -v otus | grep 'PV Name'**
-  PV Name               /dev/sdb
-  **root@ol-alp-ubuntu1:~# lvdisplay /dev/otus/test**
-  --- Logical volume ---
-  LV Path                /dev/otus/test
-  LV Name                test
-  VG Name                otus
-  LV UUID                0B0NKg-ICGz-PyZM-SlqY-qg9j-pEgW-Izl0XI
-  LV Write Access        read/write
-  LV Creation host, time ol-alp-ubuntu1, 2025-09-12 06:17:06 +0000
-  LV Status              available
-  open                 0
-  LV Size                <20.00 GiB
-  Current LE             5119
-  Segments               1
-  Allocation             inherit
-  Read ahead sectors     auto
-  - currently set to     256
-  Block device           252:1
- **root@ol-alp-ubuntu1:~# vgs**
-  VG        #PV #LV #SN Attr   VSize   VFree
-  otus        1   1   0 wz--n- <25.00g  5.00g
-  ubuntu-vg   1   1   0 wz--n- <28.00g 14.00g
- **root@ol-alp-ubuntu1:~# lvs**
-  LV        VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
-  test      otus      -wi-a----- <20.00g
-  ubuntu-lv ubuntu-vg -wi-ao---- <14.00g
- **root@ol-alp-ubuntu1:~# lvcreate -L100M -n small otus** # создать еще один LV из свободного места. На этот раз создадим не экстентами, а абсолютным значением в мегабайтах:
-  Logical volume "small" created.
-  **root@ol-alp-ubuntu1:~# lvs**
-  LV        VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
-  small     otus      -wi-a----- 100.00m
-  test      otus      -wi-a----- <20.00g
-  ubuntu-lv ubuntu-vg -wi-ao---- <14.00g
- **root@ol-alp-ubuntu1:~# mkfs.ext4 /dev/otus/test** # Создаем на LV файловую систему и смонтируем его
- mke2fs 1.47.0 (5-Feb-2023)
- Creating filesystem with 5241856 4k blocks and 1310720 inodes
- Filesystem UUID: e962ea62-1dcc-4f03-be63-d15e556065a2
- Superblock backups stored on blocks:
- 32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
- 4096000
-
- Allocating group tables: done
- Writing inode tables: done
- Creating journal (32768 blocks): done
- Writing superblocks and filesystem accounting information: done
- **root@ol-alp-ubuntu1:~# mkdir /data**
- **root@ol-alp-ubuntu1:~# mount /dev/otus/test /data/**
- **root@ol-alp-ubuntu1:~# mount | grep /data**
- /dev/mapper/otus-test on /data type ext4 (rw,relatime
- # Расширение LVM
- Допустим, перед нами встала проблема нехватки свободного места в директории /data. Мы можем расширить файловую систему на LV /dev/otus/test за - счет нового блочного устройства /dev/sdc.
- **root@ol-alp-ubuntu1:~# pvcreate /dev/sdc**
- Physical volume "/dev/sdc" successfully created.
- **root@ol-alp-ubuntu1:~# vgextend otus /dev/sdc** # расширяем VG otus диском sdc
- Volume group "otus" successfully extended
- **root@ol-alp-ubuntu1:~# vgdisplay -v otus | grep 'PV Name'** # проверка
- PV Name               /dev/sdb
- PV Name               /dev/sdc
- **root@ol-alp-ubuntu1:~# vgs**
- VG        #PV #LV #SN Attr   VSize   VFree
- otus        2   2   0 wz--n-  49.99g <29.90g
- ubuntu-vg   1   1   0 wz--n- <28.00g  14.00g
- **root@ol-alp-ubuntu1:~# dd if=/dev/zero of=/data/test.log bs=1M  count=80000 status=progress** # займем все место на диске
- 20094910464 bytes (20 GB, 19 GiB) copied, 16 s, 1.3 GB/s
- dd: error writing '/data/test.log': **No space left on device** # занято 100% дискового пространства
- 19967+0 records in
- 19966+0 records out
- 20936445952 bytes (21 GB, 19 GiB) copied, 16.7435 s, 1.3 GB/s
- **root@ol-alp-ubuntu1:~# df -Th /data/**
- Filesystem            Type  Size  Used Avail Use% Mounted on
- /dev/mapper/otus-test ext4   20G   20G     0 100% /data
- **root@ol-alp-ubuntu1:~# lvextend -l+80%FREE /dev/otus/test** # Увеличиваем LV за счет части (80%) появившегося свободного места.
- Size of logical volume otus/test changed from <20.00 GiB (5119 extents) **to <43.92 GiB** (11243 extents).
- Logical volume otus/test successfully resized.
- **root@ol-alp-ubuntu1:~# lvs /dev/otus/test**
- LV   VG   Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
- test otus -wi-ao---- <43.92g
- **root@ol-alp-ubuntu1:~# df -Th /data** # файловая система в размере пока не изменилась
- Filesystem            Type  Size  Used Avail Use% Mounted on
- /dev/mapper/otus-test ext4   20G   20G     0 100% /data
- **root@ol-alp-ubuntu1:~# resize2fs /dev/otus/test**
- resize2fs 1.47.0 (5-Feb-2023)
- Filesystem at /dev/otus/test is mounted on /data; on-line resizing required
- old_desc_blocks = 3, new_desc_blocks = 6
- The filesystem on /dev/otus/test is now 11512832 (4k) blocks long.
- **root@ol-alp-ubuntu1:~# df -Th /data** # проверяем место
- Filesystem            Type  Size  Used Avail Use% Mounted on
- /dev/mapper/otus-test ext4   44G   20G   22G  48% /data
- # Допустим Вы забыли оставить место на снапшоты.  уменьшить существующий LV с помощью команды lvreduce, но перед этим необходимо отмонтировать файловую систему, проверить её на ошибки и уменьшить ее размер:

- **root@ol-alp-ubuntu1:~# umount /data/**
- **root@ol-alp-ubuntu1:~# e2fsck -fy /dev/otus/test**
- e2fsck 1.47.0 (5-Feb-2023)
- Pass 1: Checking inodes, blocks, and sizes
- Pass 2: Checking directory structure
- Pass 3: Checking directory connectivity
- Pass 4: Checking reference counts
- Pass 5: Checking group summary information
- /dev/otus/test: 12/2883584 files (0.0% non-contiguous), 5338504/11512832 blocks
- **root@ol-alp-ubuntu1:~# resize2fs /dev/otus/test 30G**
- resize2fs 1.47.0 (5-Feb-2023)
- Resizing the filesystem on /dev/otus/test to 7864320 (4k) blocks.
- The filesystem on /dev/otus/test is now 7864320 (4k) blocks long.
- **root@ol-alp-ubuntu1:~# df -Th /data**
- Filesystem                        Type  Size  Used Avail Use% Mounted on
- /dev/mapper/ubuntu--vg-ubuntu--lv ext4   14G  4.8G  8.2G  37% /
- **root@ol-alp-ubuntu1:~# lvs /dev/otus/test**
- LV   VG   Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
- test otus -wi-a----- <43.92g

- # Работа со снапшотами
- **Снапшот создается командой lvcreate, только с флагом -s, который указывает на то, что это снимок:**
- **root@ol-alp-ubuntu1:~# lvcreate -L 500M -s -n test-snap /dev/otus/test**
- Logical volume "test-snap" created.
- **root@ol-alp-ubuntu1:~# vgs -o +lv_size,lv_name | grep test** # проверка
- otus        2   3   1 wz--n-  49.99g <5.49g <43.92g test
- otus        2   3   1 wz--n-  49.99g <5.49g 500.00m test-snap
- **root@ol-alp-ubuntu1:~# lsblk**
- NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
- sda                         8:0    0   30G  0 disk
- ├─sda1                      8:1    0    1M  0 part
- ├─sda2                      8:2    0    2G  0 part /boot
- └─sda3                      8:3    0   28G  0 part
-  └─ubuntu--vg-ubuntu--lv 252:0    0   14G  0 lvm  /
- sdb                         8:16   0   25G  0 disk
- ├─otus-small              252:2    0  100M  0 lvm
- └─otus-test-real          252:3    0 43.9G  0 lvm
-  ├─otus-test             252:1    0 43.9G  0 lvm
-  └─otus-test--snap       252:5    0 43.9G  0 lvm
- sdc                         8:32   0   25G  0 disk
- ├─**otus-test-real**          252:3    0 43.9G  0 lvm
- │ ├─otus-test             252:1    0 43.9G  0 lvm
- │ └─**otus-test--snap**       252:5    0 43.9G  0 lvm
- └─**otus-test--snap-cow**     252:4    0  500M  0 lvm
-  └─otus-test--snap       252:5    0 43.9G  0 lvm
- sdd                         8:48   0   25G  0 disk
- sde                         8:64   0   25G  0 disk
- sr0                        11:0    1  3.1G  0 rom
- **root@ol-alp-ubuntu1:~# mkdir /data-snap**
- **root@ol-alp-ubuntu1:~# mount /dev/otus/test-snap /data-snap/**
- **root@ol-alp-ubuntu1:~# ll /data-snap/**
- total 20445776
- drwxr-xr-x  3 root root        4096 Sep 12 06:47 ./
- drwxr-xr-x 26 root root        4096 Sep 12 07:21 ../
- drwx------  2 root root       16384 Sep 12 06:34 lost+found/
- -rw-r--r--  1 root root 20936445952 Sep 12 06:49 test.log
- # Можно также восстановить предыдущее состояние. “Откатиться” на снапшот.
- **root@ol-alp-ubuntu1:~# umount /data-snap**
- **root@ol-alp-ubuntu1:/# umount /data**
- umount: /data: not mounted.
- **root@ol-alp-ubuntu1:/# lvconvert --merge /dev/otus/test-snap**
- Merging of volume otus/test-snap started.
- otus/test: Merged: 100.00%
- **root@ol-alp-ubuntu1:/# mount /dev/otus/test /data**
- **root@ol-alp-ubuntu1:/# ll /data**
- total 20445776
- drwxr-xr-x  3 root root        4096 Sep 12 06:47 ./
- drwxr-xr-x 26 root root        4096 Sep 12 07:21 ../
- drwx------  2 root root       16384 Sep 12 06:34 lost+found/
- -rw-r--r--  1 root root 20936445952 Sep 12 06:49 test.log
- # Работа с LVM-RAID
- **root@ol-alp-ubuntu1:/# pvcreate /dev/sd{d,e}**
- Physical volume "/dev/sdd" successfully created.
- Physical volume "/dev/sde" successfully created.
- **root@ol-alp-ubuntu1:/# vgcreate vg0 /dev/sd{d,e}**
- Volume group "vg0" successfully create
- **root@ol-alp-ubuntu1:/# lvcreate -l+80%FREE -m1 -n mirror vg0**
- Logical volume "mirror" created.
- **root@ol-alp-ubuntu1:/# lvs**
- LV        VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
- small     otus      -wi-a----- 100.00m
- test      otus      -wi-ao---- <43.92g
- ubuntu-lv ubuntu-vg -wi-ao---- <14.00g
- mirror    vg0       rwi-a-r--- <20.00g                                    45.80



- **root@ol-alp-ubuntu1:~# lsblk**
- NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
- sda                         8:0    0   30G  0 disk
- ├─sda1                      8:1    0    1M  0 part
- ├─sda2                      8:2    0    2G  0 part /boot
- └─sda3                      8:3    0   28G  0 part
-   └─ubuntu--vg-ubuntu--lv 252:2    0   14G  0 lvm  /
- sdb                         8:16   0   25G  0 disk
- ├─otus-test               252:0    0 43.9G  0 lvm
- └─otus-small              252:1    0  100M  0 lvm
- sdc                         8:32   0   25G  0 disk
- └─otus-test               252:0    0 43.9G  0 lvm
- sdd                         8:48   0   25G  0 disk
- ├─vg0-mirror_rmeta_0      252:3    0    4M  0 lvm
- │ └─vg0-mirror            252:7    0   20G  0 lvm
- └─vg0-mirror_rimage_0     252:4    0   20G  0 lvm
-   └─vg0-mirror            252:7    0   20G  0 lvm
- sde                         8:64   0   25G  0 disk
- ├─vg0-mirror_rmeta_1      252:5    0    4M  0 lvm
- │ └─vg0-mirror            252:7    0   20G  0 lvm
- └─vg0-mirror_rimage_1     252:6    0   20G  0 lvm
-   └─vg0-mirror            252:7    0   20G  0 lvm
- sr0                        11:0    1 1024M  0 rom
- **root@ol-alp-ubuntu1:~#  lvdisplay /dev/otus/test**
-   --- Logical volume ---
-   LV Path                /dev/otus/test
-   LV Name                test
-   VG Name                otus
-   LV UUID                0B0NKg-ICGz-PyZM-SlqY-qg9j-pEgW-Izl0XI
-   LV Write Access        read/write
-  LV Creation host, time ol-alp-ubuntu1, 2025-09-12 06:17:06 +0000
-   LV Status              available
-   # open                 0
-  LV Size                <43.92 GiB
-   Current LE             11243
-   Segments               3
-   Allocation             inherit
-   Read ahead sectors     auto
-   - currently set to     256
-   Block device           252:0

- **root@ol-alp-ubuntu1:~# vgs**
-   VG        #PV #LV #SN Attr   VSize   VFree
-   otus        2   2   0 wz--n-  49.99g <5.98g
-   ubuntu-vg   1   1   0 wz--n- <28.00g 14.00g
-   vg0         2   1   0 wz--n-  49.99g  9.99g
- **root@ol-alp-ubuntu1:~# lvs**
-   LV        VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
-   small     otus      -wi-a----- 100.00m
-   test      otus      -wi-a----- <43.92g
-   ubuntu-lv ubuntu-vg -wi-ao---- <14.00g
-   mirror    vg0       rwi-a-r--- <20.00g                                    100.00
- **root@ol-alp-ubuntu1:~# lvremove /dev/otus/test**
- Do you really want to remove and DISCARD active logical volume otus/test? [y/n]: Y
-   Logical volume "test" successfully removed.
- **root@ol-alp-ubuntu1:~# lvremove /dev/otus/small**
- Do you really want to remove and DISCARD active logical volume otus/small? [y/n]: Y
-   Logical volume "small" successfully removed.
- **root@ol-alp-ubuntu1:~# vgremove otus**
-   Volume group "otus" successfully removed
- **root@ol-alp-ubuntu1:~# pvremove /dev/sdb**
-   Labels on physical volume "/dev/sdb" successfully wiped.
- **root@ol-alp-ubuntu1:~# pvremove /dev/sdc**
-   Labels on physical volume "/dev/sdc" successfully wiped.
- **root@ol-alp-ubuntu1:~# lsblk**
- NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
- sda                         8:0    0   30G  0 disk
- ├─sda1                      8:1    0    1M  0 part
- ├─sda2                      8:2    0    2G  0 part /boot
- └─sda3                      8:3    0   28G  0 part
-   └─ubuntu--vg-ubuntu--lv 252:2    0   14G  0 lvm  /
- sdb                         8:16   0   25G  0 disk
- sdc                         8:32   0   25G  0 disk
- sdd                         8:48   0   25G  0 disk
- ├─vg0-mirror_rmeta_0      252:3    0    4M  0 lvm
- │ └─vg0-mirror            252:7    0   20G  0 lvm
- └─vg0-mirror_rimage_0     252:4    0   20G  0 lvm
-   └─vg0-mirror            252:7    0   20G  0 lvm
- sde                         8:64   0   25G  0 disk
- ├─vg0-mirror_rmeta_1      252:5    0    4M  0 lvm
- │ └─vg0-mirror            252:7    0   20G  0 lvm
- └─vg0-mirror_rimage_1     252:6    0   20G  0 lvm
-   └─vg0-mirror            252:7    0   20G  0 lvm
- sr0                        11:0    1 1024M  0 rom
- # Домашнее задание (еще одно нашлось)
- **На виртуальной машине с Ubuntu 24.04 и LVM.
- **Уменьшить том под / до 8G.
- **Выделить том под /home.
- **Выделить том под /var - сделать в mirror.
- **/home - сделать том для снапшотов.
- **Прописать монтирование в fstab. Попробовать с разными опциями и разными файловыми системами (на выбор).
- **Работа со снапшотами:
- **сгенерить файлы в /home/;
- **снять снапшот;
- **удалить часть файлов;
- **восстановится со снапшота.
- ** * На дисках попробовать поставить btrfs/zfs — с кэшем, снапшотами и разметить там каталог /opt.
- ** Логировать работу можно с помощью утилиты script

- **root@ol-alp-ubuntu1:~# pvcreate /dev/sdb**
-   Physical volume "/dev/sdb" successfully created.
- **root@ol-alp-ubuntu1:~# vgcreate vg_root /dev/sdb**
-   Volume group "vg_root" successfully created
- **root@ol-alp-ubuntu1:~# lvcreate -n lv_root -l +100%FREE /dev/vg_root**
- WARNING: ext4 signature detected on /dev/vg_root/lv_root at offset 1080. Wipe it? [y/n]: Y
-   Wiping ext4 signature on /dev/vg_root/lv_root.
-   Logical volume "lv_root" created.
- **root@ol-alp-ubuntu1:~# mkfs.ext4 /dev/vg_root/lv_root**
- mke2fs 1.47.0 (5-Feb-2023)
- Creating filesystem with 6552576 4k blocks and 1638400 inodes
- Filesystem UUID: 783b3aed-d8d5-4c32-b246-57c6db19d784
- Superblock backups stored on blocks:
- 	4096000

- Allocating group tables: done
- Writing inode tables: done
- Creating journal (32768 blocks): done
- Writing superblocks and filesystem accounting information: done
- **root@ol-alp-ubuntu1:~# mount /dev/vg_root/lv_root /mnt**

- **root@ol-alp-ubuntu1:~# rsync -avxHAX --progress / /mnt/** # копируем все данные с / раздела в /mnt
- **root@ol-alp-ubuntu1:~# ls /mnt**
- bin                boot   dev  home  lib64              lost+found  mnt  proc  run   sbin.usr-is-merged  srv       sys  usr
- bin.usr-is-merged  cdrom  etc  lib   lib.usr-is-merged  media       opt  root  sbin  snap                swap.img  tmp  var
- **сконфигурируем grub для того, чтобы при старте перейти в новый /.
Сымитируем текущий root, сделаем в него chroot и обновим grub:**
- **root@ol-alp-ubuntu1:~# for i in /proc/ /sys/ /dev/ /run/ /boot/; \
 do mount --bind $i /mnt/$i; done**
- **root@ol-alp-ubuntu1:~# chroot /mnt/**
- **root@ol-alp-ubuntu1:/# grub-mkconfig -o /boot/grub/grub.cfg** # Cконфигурируем grub для того, чтобы при старте перейти в новый /.
Сымитируем текущий root, сделаем в него chroot и обновим grub:

- Sourcing file `/etc/default/grub'
- Generating grub configuration file ...
- Found linux image: /boot/vmlinuz-6.8.0-79-generic
- Found initrd image: /boot/initrd.img-6.8.0-79-generic
- Warning: os-prober will not be executed to detect other bootable partitions.
- Systems on them will not be added to the GRUB boot configuration.
- Check GRUB_DISABLE_OS_PROBER documentation entry.
- Adding boot menu entry for UEFI Firmware Settings ...
- done
- **root@ol-alp-ubuntu1:/# update-initramfs -u**
- update-initramfs: Generating /boot/initrd.img-6.8.0-79-generic
- **root@ol-alp-ubuntu1:/# reboot**
- # Теперь нам нужно изменить размер старой VG и вернуть на него рут. Для этого удаляем старый LV размером в 25G и создаём новый на 8G:
- **root@ol-alp-ubuntu1:/home/spg# lvremove /dev/ubuntu-vg/ubuntu-lv**
- Do you really want to remove and DISCARD active logical volume ubuntu-vg/ubuntu-lv? [y/n]: Y
-  Logical volume "ubuntu-lv" successfully removed.
- **root@ol-alp-ubuntu1:/home/spg# lvcreate -n ubuntu-vg/ubuntu-lv -L 8G /dev/ubuntu-vg**
- Logical volume "ubuntu-lv" created.
- **root@ol-alp-ubuntu1:/home/spg# mkfs.ext4 /dev/ubuntu-vg/ubuntu-lv**
- mke2fs 1.47.0 (5-Feb-2023)
- Discarding device blocks: done
- Creating filesystem with 2097152 4k blocks and 524288 inodes
- Filesystem UUID: 2a8d4d79-8b33-47a2-baf2-e5b9c408c43a
- Superblock backups stored on blocks:
- 	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

- Allocating group tables: done
- Writing inode tables: done
- Creating journal (16384 blocks): done
- Writing superblocks and filesystem accounting information: done

- **root@ol-alp-ubuntu1:/home/spg# mount /dev/ubuntu-vg/ubuntu-lv /mnt**
- **root@ol-alp-ubuntu1:/home/spg# rsync -avxHAX --progress / /mnt/**
- # Так же как в первый раз cконфигурируем grub.
- **root@ol-alp-ubuntu1:/home/spg# for i in /proc/ /sys/ /dev/ /run/ /boot/;  do mount --bind $i /mnt/$i; done**
- **root@ol-alp-ubuntu1:/home/spg# chroot /mnt/**
- **root@ol-alp-ubuntu1:/# grub-mkconfig -o /boot/grub/grub.cfg**
- Sourcing file `/etc/default/grub'
- Generating grub configuration file ...
- Found linux image: /boot/vmlinuz-6.8.0-79-generic
- Found initrd image: /boot/initrd.img-6.8.0-79-generic
- Warning: os-prober will not be executed to detect other bootable partitions.
- Systems on them will not be added to the GRUB boot configuration.
- Check GRUB_DISABLE_OS_PROBER documentation entry.
- Adding boot menu entry for UEFI Firmware Settings ...
- done
- **root@ol-alp-ubuntu1:/# update-initramfs -u**
- update-initramfs: Generating /boot/initrd.img-6.8.0-79-generic
- W: Couldn't identify type of root file system for fsck hook
- # Пока не перезагружаемся и не выходим из под chroot - мы можем заодно перенести /var.
- # Выделить том под /var в зеркало
- **root@ol-alp-ubuntu1:/# pvcreate /dev/sdc /dev/sdd**
-   Can't initialize physical volume "/dev/sdd" of volume group "vg0" without -ff
-   /dev/sdd: physical volume not initialized.
-   Physical volume "/dev/sdc" successfully created.
- **root@ol-alp-ubuntu1:/# vgcreate vg_var /dev/sdc /dev/sdd**
-   Physical volume '/dev/sdd' is already in volume group 'vg0'
-   /dev/sdd: physical volume not initialized.
- **root@ol-alp-ubuntu1:/# vgremove /dev/vg0**
-   Volume group "vg0" successfully removed
- **root@ol-alp-ubuntu1:/# vgcreate vg_var /dev/sdc /dev/sdd**
-   Volume group "vg_var" successfully created
- **root@ol-alp-ubuntu1:/# lvcreate -L 950M -m1 -n lv_var vg_var**
-   Rounding up size to full physical extent 952.00 MiB
-   Logical volume "lv_var" created.
- **root@ol-alp-ubuntu1:/# mkfs.ext4 /dev/vg_var/lv_var**
- mke2fs 1.47.0 (5-Feb-2023)
- Creating filesystem with 243712 4k blocks and 60928 inodes
- Filesystem UUID: 7452f181-6515-4b19-9215-9b8cc70da811
- Superblock backups stored on blocks:
- 	32768, 98304, 163840, 229376

- Allocating group tables: done
- Writing inode tables: done
- Creating journal (4096 blocks): done
- Writing superblocks and filesystem accounting information: done
- **root@ol-alp-ubuntu1:/# mount /dev/vg_var/lv_var /mnt**
- **root@ol-alp-ubuntu1:/# cp -aR /var/* /mnt/**
- **root@ol-alp-ubuntu1:/# mkdir /tmp/oldvar && mv /var/* /tmp/oldvar**
- **root@ol-alp-ubuntu1:/# umount /mnt**
- **root@ol-alp-ubuntu1:/# mount /dev/vg_var/lv_var /var**
- **root@ol-alp-ubuntu1:/# echo "`blkid | grep var: | awk '{print $2}'` \
 /var ext4 defaults 0 0" >> /etc/fstab**
- **root@ol-alp-ubuntu1:/# vi /etc/fstab**
- **root@ol-alp-ubuntu1:/# reboot**
- **root@ol-alp-ubuntu1:/home/spg# lvremove /dev/vg_root/lv_root
- Do you really want to remove and DISCARD active logical volume vg_root/lv_root? [y/n]: Y
-   Logical volume "lv_root" successfully removed.
- **root@ol-alp-ubuntu1:/home/spg# vgremove /dev/vg_root
-   Volume group "vg_root" successfully removed
- **root@ol-alp-ubuntu1:/home/spg# pvremove /dev/sdb**
-   Labels on physical volume "/dev/sdb" successfully wiped.
-  # Выделить том под /home
Выделяем том под /home по тому же принципу что делали для /var:
- **root@ol-alp-ubuntu1:/home/spg# lvcreate -n LogVol_Home -L 2G /dev/ubuntu-vg**
-   Logical volume "LogVol_Home" created.
- **root@ol-alp-ubuntu1:/home/spg# mkfs.ext4 /dev/ubuntu-vg/LogVol_Home**
- mke2fs 1.47.0 (5-Feb-2023)
- Discarding device blocks: done
- Creating filesystem with 524288 4k blocks and 131072 inodes
- Filesystem UUID: b28aacff-dc63-4343-98c8-fe64bd743c70
- Superblock backups stored on blocks:
- 	32768, 98304, 163840, 229376, 294912

- Allocating group tables: done
- Writing inode tables: done
- Creating journal (16384 blocks): done
- Writing superblocks and filesystem accounting information: done
- **root@ol-alp-ubuntu1:/home/spg# mount /dev/ubuntu-vg/LogVol_Home /mnt/**
- **root@ol-alp-ubuntu1:/home/spg# cp -aR /home/* /mnt/**
- **root@ol-alp-ubuntu1:/home/spg# rm -rf /home/* **
- **root@ol-alp-ubuntu1:/home/spg# umount /mnt**
- mount /dev/ubuntu-vg/LogVol_Home /home/
- # Правим fstab для автоматического монтирования /home:
- **root@ol-alp-ubuntu1:/home/spg# echo "`blkid | grep Home | awk '{print $2}'` \
 /home xfs defaults 0 0" >> /etc/fstab**
- **root@ol-alp-ubuntu1:/home/spg# vi /etc/fstab**
- # Работа со снапшотами
Генерируем файлы в /home/:
- **root@ol-alp-ubuntu1:/home/spg# touch /home/file{1..20**
- # Снять снапшот:
- ** root@ol-alp-ubuntu1:/home/spg# lvcreate -L 100MB -s -n home_snap \ /dev/ubuntu-vg/LogVol_Home**
-  Logical volume "home_snap" created.
-  **root@ol-alp-ubuntu1:/home/spg# rm -f /home/file{11..20}**
-  # Процесс восстановления из снапшота:
-  **root@ol-alp-ubuntu1:/home/spg# umount /home**
- **root@ol-alp-ubuntu1:/home/spg# lvconvert --merge /dev/ubuntu-vg/home_snap**
- Merging of volume ubuntu-vg/home_snap started.
- ubuntu-vg/LogVol_Home: Merged: 100.00%
- **root@ol-alp-ubuntu1:/home/spg# mount /dev/mapper/ubuntu--vg-LogVol_Home /home**
- mount: (hint) your fstab has been modified, but systemd still uses
- the old version; use 'systemctl daemon-reload' to reload.
- **root@ol-alp-ubuntu1:/home/spg# ls -al /home**
- total 28
- drwxr-xr-x  4 root root  4096 Sep 15 09:19 .
- drwxr-xr-x 23 root root  4096 Sep 15 05:58 ..
- -rw-r--r--  1 root root     0 Sep 15 09:19 file1
- -rw-r--r--  1 root root     0 Sep 15 09:19 file10
- -rw-r--r--  1 root root     0 Sep 15 09:19 file11
- -rw-r--r--  1 root root     0 Sep 15 09:19 file12
- -rw-r--r--  1 root root     0 Sep 15 09:19 file13
- -rw-r--r--  1 root root     0 Sep 15 09:19 file14
- -rw-r--r--  1 root root     0 Sep 15 09:19 file15
- -rw-r--r--  1 root root     0 Sep 15 09:19 file16
- -rw-r--r--  1 root root     0 Sep 15 09:19 file17
- -rw-r--r--  1 root root     0 Sep 15 09:19 file18
- -rw-r--r--  1 root root     0 Sep 15 09:19 file19
- -rw-r--r--  1 root root     0 Sep 15 09:19 file2
- -rw-r--r--  1 root root     0 Sep 15 09:19 file20
- -rw-r--r--  1 root root     0 Sep 15 09:19 file3
- -rw-r--r--  1 root root     0 Sep 15 09:19 file4
- -rw-r--r--  1 root root     0 Sep 15 09:19 file5
- -rw-r--r--  1 root root     0 Sep 15 09:19 file6
- -rw-r--r--  1 root root     0 Sep 15 09:19 file7
- -rw-r--r--  1 root root     0 Sep 15 09:19 file8
- -rw-r--r--  1 root root     0 Sep 15 09:19 file9
- drwx------  2 root root 16384 Sep 15 09:12 lost+found
- drwxr-x---  4 spg  spg   4096 Sep 15 06:01 spg
- # Файлы успешно восстановлены с помощью снапшота.

 ## 5 Урок

**Домашнее задание**
<ins>Практические навыки работы с ZFS</ins>

**Цель:** научится самостоятельно устанавливать ZFS, настраивать пулы, изучить основные возможности ZFS;

🎯 Что нужно сделать?

1. Определить алгоритм с наилучшим сжатием:
- определить, какие алгоритмы сжатия поддерживает zfs (gzip, zle, lzjb, lz4);
- создать 4 файловых системы, на каждой применить свой алгоритм сжатия;
- для сжатия использовать либо текстовый файл, либо группу файлов.
2. Определить настройки пула.
- С помощью команды zfs import собрать pool ZFS.
- Командами zfs определить настройки:
- размер хранилища;
- тип pool;
- значение recordsize;
- какое сжатие используется;
- какая контрольная сумма используется.
3. Работа со снапшотами:
- скопировать файл из удаленной директории;
- восстановить файл локально. zfs receive;
- найти зашифрованное сообщение в файле secret_message.

<details>
<summary> = Теория = </summary> 
# 📂 ZFS Метаданные

В **ZFS** метаданные — это служебная информация, которая описывает структуру и состояние пула, dataset'ов и файлов.  

---

## 🔹 Основные типы метаданных

### 1. Uberblock
- Точка входа в пул.  
- Хранит ссылку на корневой объект.  
- Несколько копий в разных местах пула (циклически обновляются).  

### 2. MOS (Meta Object Set)
- «Каталог» всех объектов в пуле.  
- Содержит ссылки на:
  - dataset'ы,  
  - снапшоты,  
  - space maps,  
  - ZIL.  

### 3. Block Pointer
- Указатель на блок данных.  
- Хранит:
  - физический адрес,  
  - размер блока,  
  - контрольную сумму,  
  - метод сжатия,  
  - количество копий.  

### 4. dnode
- Описывает объект (файл, каталог, снапшот).  
- Содержит:
  - атрибуты объекта,  
  - ссылки на block pointer’ы.  

### 5. ZIL (ZFS Intent Log)
- Журнал синхронных операций (`fsync`).  
- Обеспечивает целостность данных при сбоях.  

### 6. Space Maps
- Карта занятых и свободных блоков.  
- Используется для управления размещением.  

---

## 🔹 Особенности метаданных в ZFS
- **Контрольные суммы**: каждая структура самопроверяется.  
- **Несколько копий**: метаданные всегда хранятся минимум в двух экземплярах.  
- **Copy-on-Write**: метаданные никогда не перезаписываются, всегда создаётся новая версия.  

---
## 📌 Итог
ZFS метаданные — это «карта» всего пула.  
Они позволяют:
- монтировать файловую систему,  
- находить и проверять данные,  
- делать снапшоты и реплики,  
- восстанавливаться после сбоев.

---

# 🔐 Контрольные суммы в ZFS

## 📌 Что это такое
ZFS использует **контрольные суммы (checksums)** для защиты данных от повреждений.  
Каждый блок данных и каждый блок метаданных сопровождается хэш-суммой, которая хранится отдельно от самого блока.  

---

## 🔹 Как это работает
1. При записи данных ZFS вычисляет хэш (например, SHA-256 или Fletcher4).  
2. Контрольная сумма сохраняется **не рядом с данными**, а в их **родительском блоке (block pointer)**.  
3. При чтении:
   - ZFS пересчитывает хэш с прочитанного блока,  
   - сравнивает его с сохранённым значением,  
   - если есть ошибка → блок восстанавливается из копии (RAID-Z, зеркала).  

---

## 🔹 Особенности
- **End-to-End защита**: проверяется весь путь от приложения до диска.  
- **Самолечение (self-healing)**: если один блок повреждён, ZFS автоматически восстанавливает его из резервной копии.  
- **Copy-on-Write**: при изменении блоков всегда создаётся новая версия с новой контрольной суммой.  

---

## 🔹 Поддерживаемые алгоритмы
- Fletcher2 / Fletcher4 (быстрые, старые варианты).  
- SHA-256 (по умолчанию, надёжный).  
- Skein, Edon-R, SHA-512 (альтернативные, можно включать).  

📌 Итог
Контрольные суммы ZFS обеспечивают:
	•	обнаружение скрытых ошибок на диске (bit rot),
	•	автоматическое восстановление данных,
	•	гарантию целостности на уровне всей файловой системы


---

# 📦 Дедупликация в ZFS

## 📌 Что это такое
**Дедупликация** — это механизм, при котором ZFS хранит **только одну копию одинаковых блоков данных**.  
Если два файла содержат одинаковый блок, то в пуле он записывается лишь один раз, а остальные файлы указывают на него.  

---

## 🔹 Как это работает
1. При записи блока ZFS считает его **хэш (контрольную сумму)**.  
2. Проверяет в специальной структуре **DDT (Deduplication Table)**, есть ли такой блок уже в пуле.  
3. Если блок найден:
   - новый блок **не записывается**,  
   - создаётся только ссылка на существующий.  
4. Если блок новый:
   - записывается в пул,  
   - его хэш добавляется в DDT. 

---

## 🔹 Пример
Файл `A` и файл `B` содержат одинаковые блоки:  

A = [X][Y][Z]
B = [X][Y][Z]


Без дедупликации: хранится 6 блоков.  
С дедупликацией: хранится 3 блока, а оба файла указывают на одни и те же данные.  

---

## 🔹 Особенности и требования
- Дедупликация работает **на уровне блоков**, а не целых файлов.  
- Требует очень много **оперативной памяти**:  
  - примерно **1–5 ГБ RAM на каждый 1 ТБ данных**.  
  - таблица DDT должна помещаться в память для нормальной работы.  
- Может сильно **замедлить запись**, особенно на системах с малым количеством RAM.  

---

## 🔹 Когда использовать
✅ Подходит для:
- виртуализационных сред (VM, VDI), где много одинаковых блоков,  
- файлов с высокой степенью повторов (например, бэкапы образов).  

❌ Не рекомендуется для:
- домашних систем без большого объёма RAM,  
- пулов с разнородными файлами (например, фото, видео).

---

## 🔹 Как включить
bash
zfs set dedup=on tank/data

---

## 📌 Итог
Дедупликация в ZFS позволяет экономить место, но:
-	требует очень много памяти,
-	замедляет запись,
-	эффективна только в сценариях с высокой степенью повторяемости данных.

---

# ⚡ Кэширование в ZFS

## 📌 Что это такое
ZFS использует многоуровневую систему кэширования для ускорения работы с данными.  
Она включает **оперативную память** и, при необходимости, быстрые устройства (SSD).  

---

## 🔹 Основные уровни кэша

### 1. ARC (Adaptive Replacement Cache)
- Основной кэш в **оперативной памяти (RAM)**.  
- Хранит недавно использованные блоки данных и метаданные.  
- Умный алгоритм балансирует между:
  - **часто используемыми блоками** (frequency),  
  - **недавно использованными блоками** (recency).  
- Может занимать до 50–75% всей RAM.  

---

### 2. L2ARC (Level 2 ARC)
- Дополнительный кэш на SSD.  
- Хранит «вытесненные» из ARC блоки.  
- Используется только для **чтения** (read cache).  
- Полезен, если рабочий набор данных больше доступной RAM.  

---

### 3. ZIL (ZFS Intent Log)
- Журнал для **синхронных операций записи** (`fsync`).  
- По умолчанию хранится в пуле (на дисках).  
- Можно вынести на отдельное быстрое устройство (SSD/SLOG).  
- Ускоряет базы данных и приложения, которые делают много sync-записей.  

---

## 🔹 Как это работает
1. Чтение:
   - сначала поиск блока в **ARC**,  
   - если не найден → проверяется **L2ARC**,  
   - если и там нет → чтение с основного пула (HDD/SSD).  

2. Запись:
   - асинхронные записи складываются в память и сбрасываются позже,  
   - синхронные сначала фиксируются в **ZIL**, а потом пишутся в пул.  

---

## 📌 Итог
ZFS кэширование обеспечивает:
-	🔹 быстрый доступ к часто используемым данным (ARC, L2ARC),
-	🔹 защиту и ускорение синхронных записей (ZIL/SLOG),
-	🔹 эффективное использование RAM и SSD.
- Для максимальной производительности важно правильно сбалансировать:
-	количество RAM для ARC,
-	быстрые SSD для L2ARC и ZIL.

---

# 📸 Снапшоты в ZFS

## 📌 Что это такое
**Снапшот (snapshot)** — это моментальный снимок файловой системы или тома ZFS.  
Он фиксирует состояние данных в определённый момент времени и не требует копирования всего пула.  

---

## 🔹 Как это работает
- ZFS использует механизм **Copy-on-Write (COW)**.  
- При создании снапшота новые данные пишутся в новые блоки, а старые сохраняются для снапшота.  
- Снапшот занимает очень мало места, пока данные не меняются.  

---

## 🔹 Основные свойства
- Снапшот является **только для чтения**.  
- Создаётся мгновенно, независимо от размера dataset'а.  
- Хранит полное состояние файловой системы на момент создания.  
- Удаление снапшота освобождает блоки, которые больше нигде не используются.  

---

## 🔹 Пример использования

### Создать снапшот
- bash
- zfs snapshot tank/data@snap1
### Список снапшотов
- zfs list -t snapshot
### Смонтировать снапшот
- zfs mount tank/data@snap1
### Удалить снапшот
- zfs destroy tank/data@snap1
### Восстановить данные из снапшота
- zfs rollback tank/data@snap1
🔹 Зачем нужны снапшоты
- 🔹 Резервные копии «на лету» без остановки сервисов.
- 🔹 Быстрый откат после ошибок или неудачных обновлений.
- 🔹 История изменений (связка снапшотов + репликация).
- 🔹 Репликация на другие сервера (zfs send | zfs receive).

📌 Итог
### Снапшоты в ZFS — это:
- мгновенные снимки состояния данных,
- экономия места благодаря Copy-on-Write,
- удобный способ отката и резервирования,
- основа для репликации и инкрементальных бэкапов.

---

# 🌱 Клонирование в ZFS

## 📌 Что это такое
**Клон (clone)** в ZFS — это запись на основе снапшота, которая:
- изначально полностью идентична снапшоту,  
- является **полноценной файловой системой** (может изменяться),  
- использует общие блоки данных со снапшотом, экономя место.  

---

## 🔹 Особенности
- Клон всегда создаётся **из снапшота**.  
- В отличие от снапшота (только для чтения), клон — **доступен для записи**.  
- Клон зависит от исходного снапшота:  
  удалить снапшот можно только после удаления или отвязки всех его клонов.  
- Клоны экономят место благодаря **Copy-on-Write**.  

---

## 🔹 Пример использования

### 1. Создать снапшот
- bash
- zfs snapshot tank/data@snap1
### 2. Создать клон из снапшота
- zfs clone tank/data@snap1 tank/clone1
### 3. Проверить список файловых систем и клонов
- zfs list
### 4. Отвязать клон (превратить в независимую файловую систему)
- zfs promote tank/clone1
---
🔹 Зачем нужны клоны
- 🔹 Быстрое создание тестовых сред на основе актуальных данных.
- 🔹 Экономия места: клон использует те же блоки, что и снапшот.
- 🔹 Удобство разработки: можно экспериментировать с системой без риска.
- 🔹 Основа для CI/CD и тестирования обновлений.

📌 Итог
Клонирование в ZFS позволяет:
- создавать записываемые копии данных на базе снапшотов,
- экономить дисковое пространство,
- быстро разворачивать тестовые и рабочие окружения.

</details>

- ## 1. Определение алгоритма с наилучшим сжатием

- **spg@ol-alp-ubuntu1:~$ sudo -i**
- [sudo] password for spg:
- **root@ol-alp-ubuntu1:~# lsblk**
- NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
- sda                         8:0    0   30G  0 disk
- ├─sda1                      8:1    0    1M  0 part
- ├─sda2                      8:2    0    2G  0 part /boot
- └─sda3                      8:3    0   28G  0 part
-   └─ubuntu--vg-ubuntu--lv 252:0    0   14G  0 lvm  /
- sdb                         8:16   0  512M  0 disk
- sdc                         8:32   0  512M  0 disk
- sdd                         8:48   0  512M  0 disk
- sde                         8:64   0  512M  0 disk
- sdf                         8:80   0  512M  0 disk
- sdg                         8:96   0  512M  0 disk
- sdh                         8:112  0  512M  0 disk
- sdi                         8:128  0  512M  0 disk
- sr0                        11:0    1 1024M  0 rom
- **root@ol-alp-ubuntu1:~# apt install zfsutils-linux -y** # установка ZFS
- **root@ol-alp-ubuntu1:~# zpool create -f zfs_test mirror /dev/vdb /dev/vdc** # создаем пул на двух дисках (bc)
- **root@ol-alp-ubuntu1:~# zpool status**
-   pool: zfs_test
-  state: ONLINE
- config:

- NAME      STATE   READ WRITE CKSUM
- zfs_test  ONLINE   0     0     0
- mirror-0  ONLINE   0     0     0
- sdb     ONLINE     0     0     0
- sdc     ONLINE     0     0     0

- errors: No known data errors
- **root@ol-alp-ubuntu1:~# zpool export zfs_test**  # переименуем пул через экспорт-импорт в otus1
- **root@ol-alp-ubuntu1:~# zpool import zfs_test otus1**
- **root@ol-alp-ubuntu1:~# zpool status** #  посмотрим инфу по дискам
- pool: otus1
-  state: ONLINE
- config:

- NAME      STATE     READ WRITE CKSUM
- otus1     ONLINE     0     0     0
- mirror-0  ONLINE     0     0     0
- sdb     ONLINE       0     0     0
- sdc     ONLINE       0     0     0

- errors: No known data errors
- **root@ol-alp-ubuntu1:~# zpool create -f otus2 mirror /dev/sdd /dev/sde**
- **root@ol-alp-ubuntu1:~# zpool create -f otus3 mirror /dev/sdf /dev/sdg**
- **root@ol-alp-ubuntu1:~# zpool create -f otus4 mirror /dev/sdh /dev/sdi**
- **root@ol-alp-ubuntu1:~# zpool list** # создали 4 пула и посмотрим по ним инфу
- NAME    SIZE  ALLOC   FREE  CKPOINT  EXPANDSZ   FRAG    CAP  DEDUP    HEALTH  ALTROOT
- otus1   480M   130K   480M        -         -     0%     0%  1.00x    ONLINE  -
- otus2   480M   130K   480M        -         -     0%     0%  1.00x    ONLINE  -
- otus3   480M   110K   480M        -         -     0%     0%  1.00x    ONLINE  -
- otus4   480M   110K   480M        -         -     0%     0%  1.00x    ONLINE  -

- **root@ol-alp-ubuntu1:~# zfs set compression=lzjb otus1** #  добавим каждому пулу разный алгоритм сжатия
- **root@ol-alp-ubuntu1:~# zfs set compression=lz4 otus2**
- **root@ol-alp-ubuntu1:~# zfs set compression=gzip-9 otus3**
- **oot@ol-alp-ubuntu1:~# zfs set compression=zle otus4**
- **root@ol-alp-ubuntu1:~# zfs get all | grep compression** # проверим
- otus1  compression           lzjb                   local
- otus2  compression           lz4                    local
- otus3  compression           gzip-9                 local
- otus4  compression           zle                    local
- ## сжатие будет работать только с вновь записанными файлами, закачаем на все 4 пула один и тот же файл
- **root@ol-alp-ubuntu1:~# for i in {1..4}; do wget -P /otus$i https://gutenberg.org/cache/epub/2600/pg2600.converter.log; done**
- **root@ol-alp-ubuntu1:~# ls -l /otus*** # проверяем и видим, что метод сжатия в пуле otus3 (gzip-9) самый эффективный по сжатию
- /otus1:
- total **22111**
- -rw-r--r-- 1 root root 41174169 Sep  2 07:31 pg2600.converter.log

- /otus2:
- total **18013**
- -rw-r--r-- 1 root root 41174169 Sep  2 07:31 pg2600.converter.log

- /otus3:
- total **10969**
- -rw-r--r-- 1 root root 41174169 Sep  2 07:31 pg2600.converter.log

- /otus4:
- total **40237**
- -rw-r--r-- 1 root root 41174169 Sep  2 07:31 pg2600.converter.log
- **root@ol-alp-ubuntu1:~# zfs list** # проверим сколько занимает файл в наших пулах
- NAME    USED  AVAIL  REFER  MOUNTPOINT
- otus1  21.7M   330M  21.6M  /otus1
- otus2  17.7M   334M  17.6M  /otus2
- otus3  10.9M   341M  10.7M  /otus3
- otus4  39.4M   313M  39.3M  /otus4
- **root@ol-alp-ubuntu1:~# zfs get all | grep compressratio | grep -v ref** # проверим степень сжатия и убедимя что алгоритм gzip-9 самый эффективный по сжатию...
- otus1  compressratio         1.82x                  -
- otus2  compressratio         2.23x                  -
- otus3  compressratio         3.66x                  -
- otus4  compressratio         1.00x                  -
- # 2. Определение настроек пула
- **root@ol-alp-ubuntu1:~# wget -O archive.tar.gz --no-check-certificate 'https://drive.usercontent.google.com/download?id=1MvrcEp-WgAQe57aDEzxSRalPAwbNN1Bb&export=download'** # Скачиваем архив в домашний каталог
- **root@ol-alp-ubuntu1:~# tar -xzvf archive.tar.gz** #  расжимаем его
- zpoolexport/
- zpoolexport/filea
- zpoolexport/fileb
- **root@ol-alp-ubuntu1:~# zpool import -d zpoolexport/**
-    pool: otus # **имя пула otus импортируется из файла**
- id: 6554193320433390805
-   state: ONLINE
- status: Some supported features are not enabled on the pool.
- 	(Note that they may be intentionally disabled if the
- 	'compatibility' property is set.)
-  action: The pool can be imported using its name or numeric identifier, though
- 	some features will not be available without an explicit 'zpool upgrade'.
-  config:

- 	otus                         ONLINE
- mirror-0                   ONLINE
- /root/zpoolexport/filea  ONLINE
- /root/zpoolexport/fileb  ONLINE
- **root@ol-alp-ubuntu1:~#  zpool import -d zpoolexport/ otus** # импорт пула otus к нам в ОС
- **root@ol-alp-ubuntu1:~# zpool status**
-   pool: otus
-  state: ONLINE
- status: Some supported and requested features are not enabled on the pool.
- 	The pool can still be used, but some features are unavailable.
- action: Enable all features using 'zpool upgrade'. Once this is done,
- 	the pool may no longer be accessible by software that does not support
- 	the features. See zpool-features(7) for details.
- config:

- NAME                      STATE     READ WRITE CKSUM
- otus                     ONLINE       0     0     0
- mirror-0                 ONLINE       0     0     0
- /root/zpoolexport/filea  ONLINE       0     0     0
- /root/zpoolexport/fileb  ONLINE       0     0     0

- errors: No known data errors

- **root@ol-alp-ubuntu1:~# zfs get all otus** # запрос всех параметров
- **root@ol-alp-ubuntu1:~# zfs get available otus** # Размер
- NAME  PROPERTY   VALUE  SOURCE
- otus  available  350M   -
- **root@ol-alp-ubuntu1:~# zfs get readonly otus** # тип
- NAME  PROPERTY  VALUE   SOURCE
- otus  readonly  off     default
- **root@ol-alp-ubuntu1:~# zfs get recordsize otus** # значение recordsize
- NAME  PROPERTY    VALUE    SOURCE
- otus  recordsize  128K     local
- **root@ol-alp-ubuntu1:~# zfs get compression otus** # тип сжатия (или параметр отключения)
- NAME  PROPERTY     VALUE           SOURCE
- otus  compression  zle             local
- **root@ol-alp-ubuntu1:~# zfs get checksum otus** # тип контрольной суммы
- NAME  PROPERTY  VALUE      SOURCE
- otus  checksum  sha256     local
- ## 3. Работа со снапшотом, поиск сообщения от преподавателя
- **root@ol-alp-ubuntu1:~# pwd**
- /root
- root@ol-alp-ubuntu1:~# wget -O otus_task2.file --no-check-certificate https://drive.usercontent.google.com/download?id=1wgxjih8YZ-cqLqaZVa0lA3h3Y029c3oI&export=download # Скачаем файл, указанный в задании
- [1] 7119
- Redirecting output to ‘wget-log’.

- [1]+  Done                    wget -O otus_task2.file --no-check-certificate https://drive.usercontent.google.com/download?id=1wgxjih8YZ-cqLqaZVa0lA3h3Y029c3oI
- **root@ol-alp-ubuntu1:~# ls** # проверим
- archive.tar.gz  **otus_task2.file**  wget-log  zpoolexport
- **root@ol-alp-ubuntu1:~# zfs receive otus/test@today < otus_task2.file** # Восстановим файловую систему из снапшота
- **oot@ol-alp-ubuntu1:~# find /otus/test -name "secret_message"**
- /otus/test/task1/file_mess/secret_message
- /otus/test/task1/file_mess/secret_message
- -bash: /otus/test/task1/file_mess/secret_message: Permission denied
- **root@ol-alp-ubuntu1:~# cat /otus/test/task1/file_mess/secret_message**
- https://otus.ru/lessons/linux-hl/ # видим ссылку на курс OTUS
- https://otus.ru/lessons/linux-hl/

- -bash: https://otus.ru/lessons/linux-hl/: No such file or directory
## задание выполнено

---

 ## 6 Урок

**Домашнее задание**
<ins>Работа с NFS</ins>

**Цель:** научиться самостоятельно разворачивать сервис NFS и подключать к нему клиентов;

🎯 Что нужно сделать?

- запустить 2 виртуальных машины (сервер NFS и клиента);
- на сервере NFS должна быть подготовлена и экспортирована директория;
- в экспортированной директории должна быть поддиректория с именем upload с правами на запись в неё;
- экспортированная директория должна автоматически монтироваться на клиенте при старте виртуальной машины (systemd, autofs или fstab — любым способом);
- монтирование и работа NFS на клиенте должна быть организована с использованием NFSv3.

⭐️ Задание со звездочкой*

- настроить аутентификацию через KERBEROS с использованием NFSv4

<details>
<summary> = Теория = </summary> 
# NFS vs FUSE — сравнение

## 📌 Введение
- **NFS (Network File System)** — сетевой протокол, позволяющий монтировать удалённые файловые системы по сети.  
- **FUSE (Filesystem in Userspace)** — фреймворк для создания файловых систем в пространстве пользователя без написания драйверов ядра.  

---

## 📊 Сравнительная таблица

| Критерий               | **NFS**                                                                 | **FUSE**                                                                 |
|------------------------|-------------------------------------------------------------------------|--------------------------------------------------------------------------|
| **Что это**            | Сетевой протокол доступа к файловой системе                             | Фреймворк для реализации файловых систем в пространстве пользователя     |
| **Уровень**            | Работает в ядре ОС (через NFS-клиент/сервер)                            | Работает в userspace (через `libfuse` и драйвер ядра FUSE)               |
| **Тип использования**  | Подключение удалённых папок по сети                                     | Создание виртуальных/нестандартных файловых систем                       |
| **Примеры**            | `mount -t nfs server:/data /mnt`                                        | `sshfs user@host:/ /mnt`, `encfs`, `ntfs-3g`, `rclone mount`             |
| **Производительность** | Выше (часть логики в ядре, ограничение — скорость сети)                 | Ниже (переключения ядро ↔ userspace), но более гибко                     |
| **Сложность**          | Используется готовый драйвер ядра                                       | Можно писать FS на C/C++/Python/Rust                                     |
| **Применение**         | Централизованное хранение, кластеры, офисные сети                       | Облака, зашифрованные папки, нестандартные форматы файловых систем       |
| **Безопасность**       | NFSv3: слабая (по IP), NFSv4: Kerberos, ACL                             | Зависит от реализации (часто SSH, TLS или встроенное шифрование)         |
| **Плюсы**              | Простота, стабильность, скорость                                        | Универсальность, возможность монтировать «нестандартные» хранилища       |
| **Минусы**             | Жёсткая привязка к серверу и протоколу NFS                              | Более низкая производительность, зависит от качества реализации          |

---
## 🛠 Примеры использования

### 📂 NFS
- bash
# Монтирование каталога с удалённого NFS-сервера
- sudo mount -t nfs 192.168.1.10:/data /mnt/data

### 🔐 FUSE (sshfs)
# Монтирование удалённого каталога через SSH
- sshfs user@remote:/home/user /mnt/remote

---

## 🛠 Когда использовать

- ✅ **NFS** — если нужно просто и быстро расшарить каталог между машинами (локальная сеть, NAS, кластеры).  
- ✅ **FUSE** — если нужно нестандартное решение: облачные хранилища, зашифрованные данные, доступ по SSH или поддержка редких форматов.  
  </details>

  <details>
<summary> 
	
**Шпаргалка по редактору vim**
</summary>
- Vim Шпаргалка

## Краткое руководство по использованию Vim — одного из самых мощных текстовых редакторов.

---

## Режимы
- **Normal (обычный)** — режим по умолчанию (навигация, команды).
- **Insert (вставка)** — ввод текста (`i`, `a`, `o`).
- **Visual (выделение)** — работа с блоками текста (`v`, `V`, `Ctrl+v`).
- **Command-line** — команды (`:`).

---

## Навигация
- `h` / `l` — влево / вправо  
- `j` / `k` — вниз / вверх  
- `0` / `^` / `$` — начало / первый непробельный / конец строки  
- `w` / `e` — вперёд к началу / концу слова  
- `b` — назад к началу слова  
- `gg` — в начало файла  
- `G` — в конец файла  
- `:{n}` — перейти на строку `n`  

---

## Редактирование
- `i` — вставить перед курсором  
- `a` — вставить после курсора  
- `o` / `O` — новая строка ниже / выше  
- `x` — удалить символ  
- `dd` — удалить строку  
- `yy` — копировать строку  
- `p` — вставить после курсора  
- `u` — отменить (undo)  
- `Ctrl+r` — повторить (redo)  

---

## Поиск и замена
- `/слово` — поиск слова вперёд  
- `?слово` — поиск слова назад  
- `n` / `N` — повторить поиск вперёд / назад  
- `:%s/старое/новое/g` — замена в файле  
- `:.,$s/старое/новое/g` — замена с текущей до конца  

---

## Работа с файлами
- `:w` — сохранить  
- `:q` — выйти  
- `:wq` или `ZZ` — сохранить и выйти  
- `:q!` — выйти без сохранения  
- `:e имя` — открыть файл  
- `:r имя` — вставить содержимое файла  

---

## Полезное
- `.` — повтор последней команды  
- `>>` / `<<` — сдвиг строки вправо / влево (табуляция)  
- `:%!sort` — отсортировать файл через внешнюю команду  
- `:set number` — включить номера строк  
- `:syntax on` — подсветка синтаксиса  

---

## Выход из Vim (самое важное 😅)
- `:wq` — сохранить и выйти  
- `:q!` — выйти без сохранения  
- `ZZ` — сохранить и выйти (альтернатива)  

---

📌 Совет: практикуйся и используй `vimtutor` для интерактивного обучения.
</details>
---

**Выполнение домашнего задания:**
- запущены для виртуальные машины ol-apl-ubuntu-sernfs и ol-apl-ubuntu-clntnfs с ОС Ubuntu Linux (64-bit) 24.04.3 LTS
- **spg@ol-apl-ubuntu-sernfs:~$ sudo -i**
- [sudo] password for spg:
- **root@ol-apl-ubuntu-sernfs:~# apt install nfs-kernel-server** # Установка сервера NFS, Настройки сервера находятся в файле /etc/nfs.conf
- **root@ol-apl-ubuntu-sernfs:~# ss -tnplu** # проверяем наличие слушающих портов
- tcp         LISTEN       0            64                              0.0.0.0:2049                     0.0.0.0:*
- **root@ol-apl-ubuntu-sernfs:~# mkdir -p /srv/share/upload** # создаем директорию для экспорта
- **root@ol-apl-ubuntu-sernfs:~# chown -R nobody:nogroup /srv/share** # настраиваем владельцев
- **root@ol-apl-ubuntu-sernfs:~# chmod 0777 /srv/share/upload** # настраиваем права
- **root@ol-apl-ubuntu-sernfs:~# vim /etc/exports** # здесь лежит структура, которая позволит экспортировать ранее созданную директорию
- /srv/share 10.0.77.0/24(rw,sync,root_squash) # добавим туда строчку для экспорта нашего ресурса для нашей сети 10.0.77.0/24

- **root@ol-apl-ubuntu-sernfs:~# exportfs -r** # Экспортируем ранее созданную директорию
- exportfs: /etc/exports [1]: Neither 'subtree_check' or 'no_subtree_check' specified for export "10.0.77.0/24:/srv/share".
- Assuming default behaviour ('no_subtree_check').
- NOTE: this default has changed since nfs-utils version 1.0.x
- **root@ol-apl-ubuntu-sernfs:~# exportfs -s** # Проверяем, что экспортируется
- /srv/share  10.0.77.0/24(sync,wdelay,hide,no_subtree_check,sec=sys,rw,secure,root_squash,no_all_squash)
---
- ## Настраиваем клиент NFS
- **устанавливаем клиента NFS**
- **spg@ol-apl-ubuntu-clntnfs:~$ sudo -i**
- [sudo] password for spg:
- **root@ol-apl-ubuntu-clntnfs:~# apt install nfs-common**
- **root@ol-apl-ubuntu-clntnfs:~# echo "10.0.77.182:/srv/share/ /mnt nfs vers=3,noauto,x-systemd.automount 0 0" >> /etc/fstab** # добавляем монтирование
- **root@ol-apl-ubuntu-clntnfs:~# vim /etc/fstab** # проверяем строку монтирования удаленного ресурса на сервере nfs
- 10.0.77.182:/srv/share/ /mnt nfs vers=3,noauto,x-systemd.automount 0 0
- **root@ol-apl-ubuntu-clntnfs:~# systemctl daemon-reload**  # для перезагрузки конфигурации сервисов без остановки или перезапуска самих служб
- **root@ol-apl-ubuntu-clntnfs:~# systemctl restart remote-fs.target** # для перезапуска всех удалённых файловых систем, которые смонтированы через systemd
---
- ## Проверка работоспособности
- **root@ol-apl-ubuntu-sernfs:/srv/share/upload# cd /srv/share/upload/**
- **root@ol-apl-ubuntu-sernfs:/srv/share/upload# touch check_file**
- **root@ol-apl-ubuntu-sernfs:/srv/share/upload# ls -hal**
- total 8.0K
- drwxrwxrwx 2 nobody nogroup 4.0K Sep 22 12:26 .
- drwxr-xr-x 3 nobody nogroup 4.0K Sep 22 12:25 ..
- -rw-r--r-- 1 root   root       0 Sep 22 12:26 check_file
- **root@ol-apl-ubuntu-clntnfs:/mnt/upload# cd /mnt/upload/**
- **root@ol-apl-ubuntu-clntnfs:/mnt/upload# ls -hal**
- total 8.0K
- drwxrwxrwx 2 nobody nogroup 4.0K Sep 22 12:26 .
- drwxr-xr-x 3 nobody nogroup 4.0K Sep 22 12:25 ..
- -rw-r--r-- 1 root   root       0 Sep 22 12:26 check_file
---
- ## Проверки работоспособности стенда через перезагрузки:
- ##  Клиент
- **root@ol-apl-ubuntu-clntnfs:/mnt/upload# reboot**
- **spg@ol-apl-ubuntu-clntnfs:~$ sudo -i**
- [sudo] password for spg:
- **root@ol-apl-ubuntu-clntnfs:~# ls -hal  /mnt/upload/**
- total 8.0K
- drwxrwxrwx 2 nobody nogroup 4.0K Sep 22 12:26 .
- drwxr-xr-x 3 nobody nogroup 4.0K Sep 22 12:25 ..
- ## Сервер
- **root@ol-apl-ubuntu-sernfs:~# reboot**
- **root@ol-apl-ubuntu-sernfs:~# exportfs -s**
- /srv/share  10.0.77.0/24(sync,wdelay,hide,no_subtree_check,sec=sys,rw,secure,root_squash,no_all_squash)
- **root@ol-apl-ubuntu-sernfs:~# showmount -a**
- All mount points on ol-apl-ubuntu-sernfs:
- 10.0.77.142:/srv/share
- **root@ol-apl-ubuntu-sernfs:~# ls -hal  /srv/share/upload/**
- total 8.0K
- drwxrwxrwx 2 nobody nogroup 4.0K Sep 22 12:26 .
- drwxr-xr-x 3 nobody nogroup 4.0K Sep 22 12:25 ..
- -rw-r--r-- 1 root   root       0 Sep 22 12:26 check_file
- ## клиент
- **root@ol-apl-ubuntu-clntnfs:~# ls -hal  /mnt/upload/**
- total 8.0K
- drwxrwxrwx 2 nobody nogroup 4.0K Sep 22 12:26 .
- drwxr-xr-x 3 nobody nogroup 4.0K Sep 22 12:25 ..
- -rw-r--r-- 1 root   root       0 Sep 22 12:26 check_file
- - root@ol-apl-ubuntu-clntnfs:~#
- - -rw-r--r-- 1 root   root       0 Sep 22 12:26 check_file
- **root@ol-apl-ubuntu-clntnfs:~# cd /mnt/upload/**
- **root@ol-apl-ubuntu-clntnfs:/mnt/upload# touch final_check**
- **root@ol-apl-ubuntu-clntnfs:/mnt/upload# ls -hal**
- total 8.0K
- drwxrwxrwx 2 nobody nogroup 4.0K Sep 22 12:44 .
- drwxr-xr-x 3 nobody nogroup 4.0K Sep 22 12:25 ..
- -rw-r--r-- 1 root   root       0 Sep 22 12:26 **check_file**
- -rw-r--r-- 1 nobody nogroup    0 Sep 22 12:44 **final_check**
- ## Демонстрационный стенд работоспособен

## 7 урок
**Домашнее задание** <ins>"Сборка RPM-пакета и создание репозитория"</ins>

Цель: Научиться собирать RPM-пакеты.
Создавать собственный RPM-репозиторий.;

🎯**Задание**
- 1.создать свой RPM (можно взять свое приложение, либо собрать к примеру Apache с определенными опциями);
- 2.cоздать свой репозиторий и разместить там ранее собранный RPM;
- 3.реализовать это все либо в Vagrant, либо развернуть у себя через Nginx и дать ссылку на репозиторий.

<details>
	
<summary> = Теория = </summary>
# Сборка RPM-пакета и создание репозитория в Ubuntu

Этот документ описывает теоретические основы сборки RPM-пакетов и организации собственного репозитория на системе Ubuntu.  
Ubuntu по умолчанию работает с DEB-пакетами, но при необходимости можно собирать RPM для систем семейства RHEL/CentOS/Fedora.

---

## 📦 Что такое RPM
- **RPM (Red Hat Package Manager)** — формат бинарных пакетов, используемый в RHEL, CentOS, Fedora, openSUSE.  
- Аналог формата `.deb` в Debian/Ubuntu.  
- Содержит:
  - скомпилированные файлы,
  - метаданные (имя, версия, зависимости),
  - инструкции для установки и удаления.

---

## ⚙️ Основные компоненты сборки

1. **Исходники** — архив с исходным кодом (`mypkg-1.0.tar.gz`).  
2. **.spec-файл** — рецепт сборки:
   - имя и версия пакета,
   - список зависимостей,
   - разделы `%prep`, `%build`, `%install`, `%files`.  
3. **rpmbuild** — утилита, выполняющая сборку на основе `.spec`.  
   Стандартная структура каталогов `~/rpmbuild/`:
- **BUILD/** → промежуточные сборки
- **RPMS/** → готовые бинарные пакеты
- **SOURCES/** → исходные архивы
- **SPECS/** → spec-файлы
- **SRPMS/** → исходные SRPM-пакеты

  
## 📂 Репозиторий RPM
Что это
- Каталог с .rpm-пакетами и индексом метаданных.
- Метаданные позволяют yum или dnf:
- 1. показывать список пакетов,
- 2. разрешать зависимости,
- 3. обновлять пакеты.
  4. 
## Инструменты
- createrepo или createrepo_c — создают repodata/ с описанием пакетов.

## Принцип работы
- 1	Администратор складывает .rpm-файлы в каталог.
- 2	Запускает: createrepo /путь/к/каталогу
   появляется папка repodata/.
- Репозиторий раздаётся через HTTP/FTP/NFS. На клиентских системах добавляется .repo-файл в /etc/yum.repos.d/:
  
## ⚖️ Особенности при работе в Ubuntu
- Ubuntu сама RPM не использует.
- Сборка и репозиторий нужны, если Ubuntu используется:
- как сборочный сервер для CentOS/Fedora,
- или как репозиторий-сервер, раздающий RPM-клиентам.
- Для работы нужны пакеты: sudo apt install rpm rpm-build createrepo alien
 
## 📊 Схема процесса
- Исходники (.tar.gz)
- │
- ▼
- SPEC-файл (.spec)
- │
- ▼
- rpmbuild ───► RPM-пакет (.rpm)
- │
- ▼
- createrepo ──► Репозиторий (repodata/)
- │
- ▼
- Клиент (yum/dnf)
___

# DEB vs RPM

## Сравнение двух основных форматов пакетов в Linux: **DEB** (Debian/Ubuntu) и **RPM** (RHEL/CentOS/Fedora).

## 📦 Основные различия

| Характеристика       | DEB                                      | RPM                                       |
|-----------------------|-------------------------------------------|--------------------------------------------|
| **Семейство дистрибутивов** | Debian, Ubuntu, Linux Mint              | RHEL, CentOS, Fedora, openSUSE             |
| **Менеджер пакетов** | `dpkg`, `apt`                             | `rpm`, `yum`, `dnf`, `zypper`              |
| **Формат пакета**    | `.deb`                                    | `.rpm`                                     |
| **Метаданные**       | Control-файлы (`control`, `postinst`, `prerm`) | Spec-файл (`.spec`, секции `%prep`, `%build`, `%install`) |
| **Репозитории**      | `apt`-репозитории с `Packages.gz`          | `yum/dnf`-репозитории с `repodata/`        |
| **Инструменты сборки** | `dpkg-deb`, `debuild`, `pbuilder`         | `rpmbuild`                                 |
| **Уровень проверки** | Подписи GPG, контроль зависимостей         | Подписи GPG, контроль зависимостей         |
| **Совместимость**    | Используется только в Debian-подобных      | Используется в RedHat-подобных             |

---

## 🛠️ Инструменты конвертации

Иногда нужно преобразовать пакет из одного формата в другой.  
Для этого используется утилита **alien**:

# DEB → RPM
alien -r mypackage.deb

# RPM → DEB
alien -d mypackage.rpm

___

## 📊 Схема экосистемы
 Debian/Ubuntu ───► DEB ───► apt/dpkg
 RedHat/Fedora ───► RPM ───► yum/dnf/zypper

## ✅ Итог
- DEB — стандарт для Debian/Ubuntu.
- RPM — стандарт для RedHat/Fedora.
- Оба формата выполняют одну задачу: установку и управление пакетами
- Различаются экосистемой и инструментами.

## Как добавить локальный проект в свой репозиторий на GitGub:
- cd путь/к/проекту
- git remote add origin https://github.com/psibirenko-svg/spgrepo.git
- git branch -M main
- git push -u origin main
</details>

- **[root@AlmaLinux93 ~]# yum install -y wget rpmdevtools rpm-build createrepo \
 yum-utils cmake gcc git nano** # загружаем из Интернета инструменты для работы с RPM (rpmdevtools), основной пакет для сборки (rpm-build), для создания собственного YUM/DNF репозитория(createrepo), доп.утилиты (yum-utils), систему сборки пакетов (cmake), компилятор C (gcc), систему контроля версий (git) и текстовый редактор (nano)
- ...
- Complete!
- **[root@AlmaLinux93 ~]# mkdir rpm && cd rpm** # создаем рабочий каталог
- **[root@AlmaLinux93 rpm]#**
- ### Для примера возьмем пакет Nginx и соберем его с дополнительным модулем ngx_broli
- **root@AlmaLinux93 rpm]# yumdownloader --source nginx** # скачаем nginx RPM без установки в рабочий каталог
- enabling appstream-source repository
- enabling baseos-source repository
- enabling extras-source repository
- AlmaLinux 9 - AppStream - Source                                                          912 kB/s | 881 kB     00:00
- AlmaLinux 9 - BaseOS - Source                                                             387 kB/s | 377 kB     00:00
- AlmaLinux 9 - Extras - Source                                                              14 kB/s | 8.2 kB     00:00
- nginx-1.20.1-22.el9_6.3.alma.1.src.rpm                                                    3.8 MB/s | 1.1 MB     00:00
- **[root@AlmaLinux93 rpm]# ls**
- nginx-1.20.1-22.el9_6.3.alma.1.src.rpm
- **[root@AlmaLinux93 rpm]# ls /root/rpmbuild/**
- ***[root@AlmaLinux93 rpm]# rpm -Uvh nginx*.src.rpm**
- Updating / installing...
- 1:nginx-2:1.20.1-22.el9_6.3.alma.1 warning: user mockbuild does not exist - using root
- warning: group mock does not exist - using root
- ################################# [100%]
- **[root@AlmaLinux93 rpm]# ls /root/rpmbuild/**
- BUILD  RPMS  SOURCES  SPECS  SRPMS

- **[root@AlmaLinux93 rpm]# ls /root/rpmbuild/SPECS/**
- nginx.spec
- **[root@AlmaLinux93 rpm]# ls /root/rpmbuild/SOURCES/**
- 0001-remove-Werror-in-upstream-build-scripts.patch               UPGRADE-NOTES-1.6-to-1.10
- 0002-fix-PIDFile-handling.patch                                  macros.nginxmods.in
- 0003-Support-loading-cert-hardware-token-PKC.patch               maxim.key
- 0004-Set-proper-compiler-optimalization-level-O2-for-perl.patch  mdounin.key
- 0005-Init-openssl-engine-properly.patch                          nginx-1.20.1-CVE-2025-23419.patch
- 0006-Fix-ALPACA-security-issue.patch                             nginx-1.20.1.tar.gz
- 0007-Enable-TLSv1.3-by-default.patch                             nginx-1.20.1.tar.gz.asc
- 0008-CVE-2023-44487-HTTP-2-per-iteration-stream-handling.patch   nginx-logo.png
- 0009-defer-ENGINE_finish-calls-to-a-cleanup.patch                nginx-upgrade
- 0010-Optimized-chain-link-usage.patch                            nginx-upgrade.8
- 0011-CVE-2024-7347-Buffer-overread-in-the-mp4-module.patch       nginx.conf
- 0012-CVE-2022-41741-and-CVE-2022-41742-fix.patch                 nginx.logrotate
- 0013-SSL-use-of-the-SSL_OP_IGNORE_UNEXPECTED_EOF-option.patch    nginx.service
- 404.html                                                         nginx.sysusers
- 50x.html                                                         nginxmods.attr
- README.dynamic                                                   sb.key
- **[root@AlmaLinux93 rpm]# yum-builddep nginx** # Установка всех зависимостей, необходимых для сборки пакета Nginx из исходников (SRPM) на AlmaLinux/RHEL-подобных системах.
- **[root@AlmaLinux93 rpm]# cd /root**
- **[root@AlmaLinux93 ~]# git clone --recurse-submodules -j8 \
https://github.com/google/ngx_brotli** # нужно скачать исходный код модуля ngx_brotli — он
потребуется при сборке
- Cloning into 'ngx_brotli'...
- remote: Enumerating objects: 237, done.
- remote: Counting objects: 100% (37/37), done.
- remote: Compressing objects: 100% (16/16), done.
- remote: Total 237 (delta 24), reused 21 (delta 21), pack-reused 200 (from 1)
- Receiving objects: 100% (237/237), 79.51 KiB | 992.00 KiB/s, done.
- Resolving deltas: 100% (114/114), done.
- Submodule 'deps/brotli' (https://github.com/google/brotli.git) registered for path 'deps/brotli'
- Cloning into '/root/ngx_brotli/deps/brotli'...
- remote: Enumerating objects: 8473, done.
- remote: Counting objects: 100% (240/240), done.
- remote: Compressing objects: 100% (143/143), done.
- remote: Total 8473 (delta 146), reused 102 (delta 96), pack-reused 8233 (from 4)
- Receiving objects: 100% (8473/8473), 41.85 MiB | 30.03 MiB/s, done.
- Resolving deltas: 100% (5401/5401), done.
- Submodule path 'deps/brotli': checked out 'ed738e842d2fbdf2d6459e39267a633c4a9b2f5d'
- **[root@AlmaLinux93 ~]# cd ngx_brotli/deps/brotli**
- **[root@AlmaLinux93 brotli]# mkdir out && cd out**
- **[root@AlmaLinux93 out]# cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=OFF -DCMAKE_C_FLAGS="-Ofast -m64 -march=native -mtune=native -flto -funroll-loops -ffunction-sections -fdata-sections -Wl,--gc-sections" -DCMAKE_CXX_FLAGS="-Ofast -m64 -march=native -mtune=native -flto -funroll-loops -ffunction-sections -fdata-sections -Wl,--gc-sections" -DCMAKE_INSTALL_PREFIX=./installed ..** # Собираем модуль ngx_brotli: **-DCMAKE_BUILD_TYPE=Release** - с оптимизациями для релиза (без отладочной информации, с оптимизацией скорости),**-DBUILD_SHARED_LIBS=OFF** - сборка статических библиотек вместо динамических, **-DCMAKE_C_FLAGS="..."** - флаги компиляции для C: **-Ofast** — агрессивные оптимизации скорости; **-m64** — 64-битная архитектура; **-march=native -mtune=native** — использовать инструкции текущего процессора; **-flto** — Link Time Optimization (оптимизация на этапе линковки); **-funroll-loops** — раскручивание циклов; **-ffunction-sections**  **-fdata-sections** — разделение функций и данных на секции; **-Wl,--gc-sections** — удаление неиспользуемых секций на этапе линковки. **-DCMAKE_CXX_FLAGS="..."** - Те же флаги, но для компилятора C++. **-DCMAKE_INSTALL_PREFIX=./installed** - Устанавливать готовый билд в директорию ./installed.

- -- The C compiler identification is GNU 11.5.0
- -- Detecting C compiler ABI info
- -- Detecting C compiler ABI info - done
- -- Check for working C compiler: /bin/cc - skipped
- -- Detecting C compile features
- -- Detecting C compile features - done
- -- Build type is 'Release'
- -- Performing Test BROTLI_EMSCRIPTEN
- -- Performing Test BROTLI_EMSCRIPTEN - Failed
- -- Compiler is not EMSCRIPTEN
- -- Looking for log2
- -- Looking for log2 - not found
- -- Looking for log2
- -- Looking for log2 - found
- -- Configuring done (0.5s)
- -- Generating done (0.0s)
- CMake Warning:
- Manually-specified variables were not used by the project:

- CMAKE_CXX_FLAGS

-- Build files have been written to: /root/ngx_brotli/deps/brotli/out

- **[root@AlmaLinux93 out]# cmake --build . --config Release -j 2 --target brotlienc**
- [  3%] Building C object CMakeFiles/brotlicommon.dir/c/common/constants.c.o
- [  6%] Building C object CMakeFiles/brotlicommon.dir/c/common/context.c.o
- [ 10%] Building C object CMakeFiles/brotlicommon.dir/c/common/dictionary.c.o
- [ 13%] Building C object CMakeFiles/brotlicommon.dir/c/common/platform.c.o
- [ 17%] Building C object CMakeFiles/brotlicommon.dir/c/common/shared_dictionary.c.o
- [ 20%] Building C object CMakeFiles/brotlicommon.dir/c/common/transform.c.o
- [ 24%] Linking C static library libbrotlicommon.a
- [ 24%] Built target brotlicommon
- [ 27%] Building C object CMakeFiles/brotlienc.dir/c/enc/backward_references.c.o
- [ 31%] Building C object CMakeFiles/brotlienc.dir/c/enc/backward_references_hq.c.o
- [ 34%] Building C object CMakeFiles/brotlienc.dir/c/enc/bit_cost.c.o
- [ 37%] Building C object CMakeFiles/brotlienc.dir/c/enc/block_splitter.c.o
- [ 41%] Building C object CMakeFiles/brotlienc.dir/c/enc/brotli_bit_stream.c.o
- [ 44%] Building C object CMakeFiles/brotlienc.dir/c/enc/cluster.c.o
- [ 48%] Building C object CMakeFiles/brotlienc.dir/c/enc/command.c.o
- [ 51%] Building C object CMakeFiles/brotlienc.dir/c/enc/compound_dictionary.c.o
- [ 55%] Building C object CMakeFiles/brotlienc.dir/c/enc/compress_fragment.c.o
- [ 58%] Building C object CMakeFiles/brotlienc.dir/c/enc/compress_fragment_two_pass.c.o
- [ 62%] Building C object CMakeFiles/brotlienc.dir/c/enc/dictionary_hash.c.o
- [ 65%] Building C object CMakeFiles/brotlienc.dir/c/enc/encode.c.o
- [ 68%] Building C object CMakeFiles/brotlienc.dir/c/enc/encoder_dict.c.o
- [ 72%] Building C object CMakeFiles/brotlienc.dir/c/enc/entropy_encode.c.o
- [ 75%] Building C object CMakeFiles/brotlienc.dir/c/enc/fast_log.c.o
- [ 79%] Building C object CMakeFiles/brotlienc.dir/c/enc/histogram.c.o
- [ 82%] Building C object CMakeFiles/brotlienc.dir/c/enc/literal_cost.c.o
- [ 86%] Building C object CMakeFiles/brotlienc.dir/c/enc/memory.c.o
- [ 89%] Building C object CMakeFiles/brotlienc.dir/c/enc/metablock.c.o
- [ 93%] Building C object CMakeFiles/brotlienc.dir/c/enc/static_dict.c.o
- [ 96%] Building C object CMakeFiles/brotlienc.dir/c/enc/utf8_util.c.o
- [100%] Linking C static library libbrotlienc.a
- [100%] Built target brotlienc
- **[root@AlmaLinux93 out]# cd ../../../..**
- **[root@AlmaLinux93 ~]# pwd**
- /root
-  Нужно поправить сам spec файл, чтобы Nginx собирался с необходимыми нам опциями: находим секцию с параметрами configure (до условий if) и добавляем указание на модуль (не забудьте указать завершающий обратный слэш):
--add-module=/root/ngx_brotli \
- **[root@AlmaLinux93]# vi /root/rpmbuild/SPECS/nginx.spec**
- **[root@AlmaLinux93 SPECS]# rpmbuild -ba nginx.spec -D 'debug_package %{nil}'** # собираем пакет RPM, запускает сборку binary и source пакетов (-b = build, a = all). То есть создаются: 	бинарный RPM ~/rpmbuild/RPMS/… и 	исходный SRPM ~/rpmbuild/SRPMS/… и -D 'debug_package - отключает автоматическую генерацию пакета с отладочными символами

- ...
- Executing(%license): /bin/sh -e /var/tmp/rpm-tmp.lNW9Nj
- + umask 022
- + cd /root/rpmbuild/BUILD
- + cd nginx-1.20.1
- + LICENSEDIR=/root/rpmbuild/BUILDROOT/nginx-1.20.1-22.el9.3.alma.1.x86_64/usr/share/licenses/nginx-core
- + export LC_ALL=C
- + LC_ALL=C
- + export LICENSEDIR
- + /usr/bin/mkdir -p /root/rpmbuild/BUILDROOT/nginx-1.20.1-22.el9.3.alma.1.x86_64/usr/share/licenses/nginx-core
- + cp -pr LICENSE /root/rpmbuild/BUILDROOT/nginx-1.20.1-22.el9.3.alma.1.x86_64/usr/share/licenses/nginx-core
- + RPM_EC=0
- ++ jobs -p
- + exit 0
- **root@AlmaLinux93 rpmbuild]# ls -hal RPMS/x86_64/** # смотрим, что пакеты создались
- ...
-rw-r--r--. 1 root root   37K Sep 24 13:50 nginx-1.20.1-22.el9.3.alma.1.x86_64.rpm
- ...
- Копируем пакеты в общий каталог
- ***[root@AlmaLinux93 rpmbuild]# cp ~/rpmbuild/RPMS/noarch/* ~/rpmbuild/RPMS/x86_64/** 
- **[root@AlmaLinux93 rpmbuild]# cd ~/rpmbuild/RPMS/x86_64**
- **[root@AlmaLinux93 x86_64]# yum localinstall *.rpm***
- ...
- Installed:
- almalinux-logos-httpd-90.6-2.el9.noarch                         nginx-2:1.20.1-22.el9.3.alma.1.x86_64
- nginx-all-modules-2:1.20.1-22.el9.3.alma.1.noarch               nginx-core-2:1.20.1-22.el9.3.alma.1.x86_64
- nginx-filesystem-2:1.20.1-22.el9.3.alma.1.noarch                nginx-mod-devel-2:1.20.1-22.el9.3.alma.1.x86_64
- nginx-mod-http-image-filter-2:1.20.1-22.el9.3.alma.1.x86_64     nginx-mod-http-perl-2:1.20.1-22.el9.3.alma.1.x86_64
- nginx-mod-http-xslt-filter-2:1.20.1-22.el9.3.alma.1.x86_64      nginx-mod-mail-2:1.20.1-22.el9.3.alma.1.x86_64
- nginx-mod-stream-2:1.20.1-22.el9.3.alma.1.x86_64
- Complete!
- **[root@AlmaLinux93 x86_64]# systemctl start nginx**
- **[root@AlmaLinux93 x86_64]# systemctl status nginx**
- ...
- Sep 24 14:11:30 AlmaLinux93 systemd[1]: Starting The nginx HTTP and reverse proxy server...
- Sep 24 14:11:30 AlmaLinux93 nginx[49885]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
- Sep 24 14:11:30 AlmaLinux93 nginx[49885]: nginx: configuration file /etc/nginx/nginx.conf test is successful
- Sep 24 14:11:30 AlmaLinux93 systemd[1]: Started The nginx HTTP and reverse proxy server.

---

# Создем свой репозиторий и размещаем там ранее собранный RPM

- **[root@AlmaLinux93 x86_64]# mkdir /usr/share/nginx/html/repo**
- **[root@AlmaLinux93 x86_64]# cp ~/rpmbuild/RPMS/x86_64/*.rpm /usr/share/nginx/html/repo/** #Директория для статики у Nginx по умолчанию /usr/share/nginx/html. Создадим там каталог repo: копируем туда наши собранные RPM-пакеты

- **root@AlmaLinux93 x86_64]# ls /usr/share/nginx/html/repo/** # проверяем
- nginx-1.20.1-22.el9.3.alma.1.x86_64.rpm              nginx-mod-http-image-filter-1.20.1-22.el9.3.alma.1.x86_64.rpm
- nginx-all-modules-1.20.1-22.el9.3.alma.1.noarch.rpm  nginx-mod-http-perl-1.20.1-22.el9.3.alma.1.x86_64.rpm
- nginx-core-1.20.1-22.el9.3.alma.1.x86_64.rpm         nginx-mod-http-xslt-filter-1.20.1-22.el9.3.alma.1.x86_64.rpm
- nginx-filesystem-1.20.1-22.el9.3.alma.1.noarch.rpm   nginx-mod-mail-1.20.1-22.el9.3.alma.1.x86_64.rpm
- nginx-mod-devel-1.20.1-22.el9.3.alma.1.x86_64.rpm    nginx-mod-stream-1.20.1-22.el9.3.alma.1.x86_64.rpm
- **[root@AlmaLinux93 x86_64]# createrepo /usr/share/nginx/html/repo/** # Инициализируем репозиторий
- Directory walk started
- Directory walk done - 10 packages
- Temporary output repo path: /usr/share/nginx/html/repo/.repodata/
- Preparing sqlite DBs
- Pool started (with 5 workers)
- Pool finished
- **root@AlmaLinux93 x86_64]# vi /etc/nginx/nginx.conf** # настроим в NGINX доступ к листингу каталога. В файле /etc/nginx/nginx.conf в блоке server добавим следующие директивы:
- index index.html index.htm;
- autoindex on;
- **[root@AlmaLinux93 x86_64]# nginx -t** #  перезапускаем nginx
- nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
- nginx: configuration file /etc/nginx/nginx.conf test is successful
- **[root@AlmaLinux93 x86_64]# nginx -s reload**
- <html>
- <head><title>Index of /repo/</title></head>
- <body>
- <h1>Index of /repo/</h1><hr><pre><a href="../">../</a>
- <a href="repodata/">repodata/</a>                                          25-Sep-2025 12:15                   -
- <a href="nginx-1.20.1-22.el9.3.alma.1.x86_64.rpm">nginx-1.20.1-22.el9.3.alma.1.x86_64.rpm</a>            25-Sep-2025 12:11               36976
- <a href="nginx-all-modules-1.20.1-22.el9.3.alma.1.noarch.rpm">nginx-all-modules-1.20.1-22.el9.3.alma.1.noarch..&gt;</a> 25-Sep-2025 12:11                8089
- <a href="nginx-core-1.20.1-22.el9.3.alma.1.x86_64.rpm">nginx-core-1.20.1-22.el9.3.alma.1.x86_64.rpm</a>       25-Sep-2025 12:11             1030199
- <a href="nginx-filesystem-1.20.1-22.el9.3.alma.1.noarch.rpm">nginx-filesystem-1.20.1-22.el9.3.alma.1.noarch.rpm</a> 25-Sep-2025 12:11                9696
- <a href="nginx-mod-devel-1.20.1-22.el9.3.alma.1.x86_64.rpm">nginx-mod-devel-1.20.1-22.el9.3.alma.1.x86_64.rpm</a>  25-Sep-2025 12:11              761144
- <a href="nginx-mod-http-image-filter-1.20.1-22.el9.3.alma.1.x86_64.rpm">nginx-mod-http-image-filter-1.20.1-22.el9.3.alm..&gt;</a> 25-Sep-2025 12:11               20101
- <a href="nginx-mod-http-perl-1.20.1-22.el9.3.alma.1.x86_64.rpm">nginx-mod-http-perl-1.20.1-22.el9.3.alma.1.x86_..&gt;</a> 25-Sep-2025 12:11               31607
- <a href="nginx-mod-http-xslt-filter-1.20.1-22.el9.3.alma.1.x86_64.rpm">nginx-mod-http-xslt-filter-1.20.1-22.el9.3.alma..&gt;</a> 25-Sep-2025 12:11               18885
- <a href="nginx-mod-mail-1.20.1-22.el9.3.alma.1.x86_64.rpm">nginx-mod-mail-1.20.1-22.el9.3.alma.1.x86_64.rpm</a>   25-Sep-2025 12:11               54514
- <a href="nginx-mod-stream-1.20.1-22.el9.3.alma.1.x86_64.rpm">nginx-mod-stream-1.20.1-22.el9.3.alma.1.x86_64.rpm</a> 25-Sep-2025 12:11               81157
- </pre><hr></body>
- </html>
- **[root@AlmaLinux93 x86_64]# cat >> /etc/yum.repos.d/otus.repo << EOF** # Все готово для того, чтобы протестировать репозиторий.Добавим его в /etc/yum.repos.d
- > [otus]
- > name=otus-linux
- > baseurl=http://localhost/repo
- > gpgcheck=0
- > enabled=1
- > EOF
- **[root@AlmaLinux93 x86_64]# yum repolist enabled | grep otus**
- otus                             otus-linux
- **[root@AlmaLinux93 x86_64]# cd /usr/share/nginx/html/repo/** # Добавим пакет в наш репозиторий
- **[root@AlmaLinux93 repo]# wget https://repo.percona.com/yum/percona-release-latest.noarch.rpm**
- --2025-09-26 11:38:38--  https://repo.percona.com/yum/percona-release-latest.noarch.rpm
- Resolving repo.percona.com (repo.percona.com)... 49.12.125.205, 2a01:4f8:242:5792::2
- Connecting to repo.percona.com (repo.percona.com)|49.12.125.205|:443... connected.
- HTTP request sent, awaiting response... 200 OK
- Length: 28532 (28K) [application/x-redhat-package-manager]
- Saving to: ‘percona-release-latest.noarch.rpm’

- percona-release-latest.noarch.rpm       100%[=============================================================================>]  27.86K  --.-KB/s    in 0s

- 2025-09-26 11:38:39 (292 MB/s) - ‘percona-release-latest.noarch.rpm’ saved [28532/28532]
- **[root@AlmaLinux93 repo]# createrepo /usr/share/nginx/html/repo/** # Обновим список пакетов в репозитории
- Directory walk started
- Directory walk done - 11 packages
- Temporary output repo path: /usr/share/nginx/html/repo/.repodata/
- Preparing sqlite DBs
- Pool started (with 5 workers)
- Pool finished
- **[root@AlmaLinux93 repo]# yum makecache**
- AlmaLinux 9 - AppStream                                                                                                       6.9 kB/s | 4.2 kB     00:00
- AlmaLinux 9 - BaseOS                                                                                                          5.9 kB/s | 3.8 kB     00:00
- AlmaLinux 9 - Extras                                                                                                          7.7 kB/s | 3.3 kB     00:00
- otus-linux                                                                                                                    2.9 MB/s | 3.0 kB     00:00
- otus-linux                                                                                                                    2.1 MB/s | 7.2 kB     00:00
- **[root@AlmaLinux93 repo]# yum list | grep otus**
- percona-release.noarch                               1.0-32                              otus
---

- **[root@AlmaLinux93 repo]# yum install -y percona-release.noarch** # Так как Nginx у нас уже стоит, установим репозиторий percona-release
- Last metadata expiration check: 0:01:48 ago on Fri Sep 26 11:42:24 2025.
- Dependencies resolved.
- ==============================================================================================================================================================
-  Package                                      Architecture                        Version                             Repository                         Size
- ==============================================================================================================================================================
- Installing:
-  percona-release                              noarch                              1.0-32                              otus                               28 k

- Transaction Summary
- ==============================================================================================================================================================
- Install  1 Package

- Total download size: 28 k
- Installed size: 50 k
- Downloading Packages:
- percona-release-latest.noarch.rpm                                                                                              18 MB/s |  28 kB     00:00
- --------------------------------------------------------------------------------------------------------------------------------------------------------------
- Total                                                                                                                         2.7 MB/s |  28 kB     00:00
- Running transaction check
- Transaction check succeeded.
- Running transaction test
- Transaction test succeeded.
- Running transaction
-   Preparing        :                                                                                                                                      1/1
-   Installing       : percona-release-1.0-32.noarch                                                                                                        1/1
-   Running scriptlet: percona-release-1.0-32.noarch                                                                                                        1/1
- * Enabling the Percona Release repository
- <*> All done!
- * Enabling the Percona Telemetry repository
- <*> All done!
- * Enabling the PMM2 Client repository
- <*> All done!
- The percona-release package now contains a percona-release script that can enable additional repositories for our newer products.

- Note: currently there are no repositories that contain Percona products or distributions enabled. We recommend you to enable Percona Distribution repositories instead of - - - individual product repositories, because with the Distribution you will get not only the database itself but also a set of other componets that will help you work with your - - database.

- For example, to enable the Percona Distribution for MySQL 8.0 repository use:

-   percona-release setup pdps8.0

- Note: To avoid conflicts with older product versions, the percona-release setup command may disable our original repository for some products.

- For more information, please visit:
-   https://docs.percona.com/percona-software-repositories/percona-release.html


-   Verifying        : percona-release-1.0-32.noarch                                                                                                        1/1

- Installed:
-   percona-release-1.0-32.noarch

- **Complete!**

---

root@AlmaLinux93 repo]# git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint: 	git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint: 	git branch -m <name>
Initialized empty Git repository in /usr/share/nginx/html/repo/.git/



## 8 урок
**Домашнее задание** <ins>"Работа с загрузчиком"</ins>

Цель: научиться попадать в систему без пароля;
устанавливать систему с LVM и переименовывать в VG;

🎯**Задание**
- 1. Включить отображение меню Grub.
- 2. Попасть в систему без пароля несколькими способами.
- 3. Установить систему с LVM, после чего переименовать VG.

<details>
	
<summary> = Теория = </summary>

</details>

# 1.Включаем отображение меню Grub

- **root@ol-apl-ubuntu:~# vim /etc/default/grub** # Для отображения меню нужно отредактировать конфигурационный файл
- "/etc/default/grub" 40L, 1538B                                                                 1,1           All
- ...
- GRUB_DEFAULT=0
- **#GRUB_TIMEOUT_STYLE=hidden**
- **GRUB_TIMEOUT=10**
- GRUB_DISTRIBUTOR=`( . /etc/os-release; echo ${NAME:-Ubuntu} ) 2>/dev/null || echo Ubuntu`
- GRUB_CMDLINE_LINUX_DEFAULT=""
- GRUB_CMDLINE_LINUX=""
- ...
- **root@ol-apl-ubuntu:~# update-grub** # обновляем конфигурацию GRUB
- Sourcing file `/etc/default/grub'
- Generating grub configuration file ...
- Found linux image: /boot/vmlinuz-6.8.0-84-generic
- Found initrd image: /boot/initrd.img-6.8.0-84-generic
- Found linux image: /boot/vmlinuz-6.8.0-83-generic
- Found initrd image: /boot/initrd.img-6.8.0-83-generic
- Warning: os-prober will not be executed to detect other bootable partitions.
- Systems on them will not be added to the GRUB boot configuration.
- Check GRUB_DISABLE_OS_PROBER documentation entry.
- Adding boot menu entry for UEFI Firmware Settings ...
- done
- **root@ol-apl-ubuntu:~# reboot** # проверяем, меню GRUB появилось
- нажимаем "e" (edit) когда при загрузке появляется меню GRUB, попадаем в окно, где мы можем изменить параметры загрузки
-
# 2. Попасть в систему без пароля несколькими способами:

- **Способ 1. init=/bin/bash**
- В конце строки, начинающейся с linux, добавляем init=/bin/bash
- 
- и нажимаем сtrl-x для загрузки в систему
- Вы попали в систему. Но есть один нюанс. Рутовая файловая
система при этом монтируется в режиме Read-Only. Если вы хотите перемонтировать ее в режим Read-Write, можно воспользоваться командой:
- **root@(none):/# mount -o remount,rw /
- **root@(none):/# vim 123 # создаем файл 123, редактируем, записывыем и проверяем: ЕСТЬ права на запись!
- 
- **Способ 2. Recovery mode**
- В меню загрузчика на первом уровне выбрать второй пункт (Advanced options…), далее загрузить пункт меню с указанием recovery mode в названии. 
- Получим меню режима восстановления.
- В этом меню сначала включаем поддержку сети **(network)** для того, чтобы файловая система перемонтировалась в режим read/write (либо это можно сделать вручную).
- Далее выбираем пункт **root** и попадаем в консоль с пользователем root. Если вы ранее устанавливали пароль для пользователя root (по умолчанию его нет), то необходимо его ввести. 
В этой консоли можно производить любые манипуляции с системой. РАБОТАЕТ!!
- **root@ol-apl-ubuntu:˜# pw**
- /root
- **root@ol-apl-ubuntu:˜# vim 222** # редактируем и проверяем, удаляем
- **root@ol-apl-ubuntu:˜# vim /etc/group** # редактируем для примера...

- # 3. Установить систему с LVM, после чего переименовать VG
- 
- **spg@ol-apl-ubuntu:~$ sudo -i**
- [sudo] password for spg:
- **root@ol-apl-ubuntu:~# vgs** # смотрим текущее состояние системы
- VG        #PV #LV #SN Attr   VSize   VFree
- **ubuntu-vg   1   1   0 wz--n- <28.00g 14.00g**

- **root@ol-apl-ubuntu:~# vgrename ubuntu-vg ubuntu-otus** # переименовываем Volume Group
- Volume group "ubuntu-vg" successfully renamed to "ubuntu-otus"
- 
- **root@ol-apl-ubuntu:~# vim /boot/grub/grub.cfg** #Далее правим /boot/grub/grub.cfg. Везде заменяем старое название VG на новое (в файле дефис меняется на два дефиса ubuntu--vg ubuntu--otus).
- **root@ol-apl-ubuntu:~# reboot**

- Broadcast message from root@ol-apl-ubuntu on pts/1 (Wed 2025-10-01 09:22:27 UTC):

- The system will reboot now!

- **root@ol-apl-ubuntu:~# vgs**
-  VG          #PV #LV #SN Attr   VSize   VFree
-  **ubuntu-otus**   1   1   0 wz--n- <28.00g 14.00g

# 2 месяц
## 9 урок
**Домашнее задание** <ins>"Systemd - создание unit-файла"</ins>

-  Цель: Научиться редактировать существующие и создавать новые unit-файлы;

🎯**Задание
- 1. Написать service, который будет раз в 30 секунд мониторить лог на предмет наличия ключевого слова (файл лога и ключевое слово должны задаваться в /etc/default).
- 2. Установить spawn-fcgi и создать unit-файл (spawn-fcgi.sevice) с помощью переделки init-скрипта (https://gist.github.com/cea2k/1318020).
- 3. Доработать unit-файл Nginx (nginx.service) для запуска нескольких инстансов сервера с разными конфигурационными файлами одновременно.
<details>
<summary> = Теория = </summary>
	# Systemd — шпаргалка

## 🔹 Что такое systemd
**systemd** — это init-система Linux, которая:
- управляет сервисами и демонами,
- настраивает автозапуск,
- собирает логи (`journald`),
- работает с таймерами (аналог cron),
- контролирует ресурсы (cgroups).

---

## 🔹 Основные команды (`systemctl`)

### Управление сервисами
- sudo systemctl start nginx      # запустить
- sudo systemctl stop nginx       # остановить
- sudo systemctl restart nginx    # перезапустить
- sudo systemctl reload nginx     # перезагрузить конфиг

### Автозагрузка
sudo systemctl enable nginx     # включить автозапуск
sudo systemctl disable nginx    # выключить автозапуск

### Проверка статуса
- systemctl status nginx

🔹 Логи
- journalctl -u nginx.service     # логи сервиса nginx
- journalctl -f                   # "tail -f" для всех логов
- journalctl --since "10 min ago" # логи за последние 10 минут

🔹 Юнит-файл (пример сервиса)
- /etc/systemd/system/myapp.service:

 [Unit]
- Description=My Test App
- After=network.target

[Service]
- ExecStart=/usr/bin/python3 /opt/myapp/app.py
- WorkingDirectory=/opt/myapp
- Restart=always
- User=www-data

[Install]
- WantedBy=multi-user.target

🔹 Таймер (аналог cron)
- Пример запуска скрипта раз в час.
- Сервис /etc/systemd/system/myscript.service:

[Unit]
- Description=Run script

[Service]
- ExecStart=/usr/local/bin/myscript.sh
- Таймер /etc/systemd/system/myscript.timer:

[Unit]
- Description=Run script every hour

[Timer]
OnCalendar=hourly
Persistent=true

[Install]
- WantedBy=timers.target

### Активация:
- sudo systemctl enable --now myscript.timer

⚡ Итог
-	•	systemctl — управление сервисами
-	•	journalctl — просмотр логов
-	•	unit-файлы — конфигурация сервисов
-	•	timers — альтернатива cron

# Systemd Units — шпаргалка

## 🔹 Что такое Unit
**Unit** — это основной объект в systemd.  
Каждый unit описывает один ресурс: сервис, сокет, устройство, точку монтирования, таймер и т.д.

---

## 🔹 Основные типы Unit
- **service** — сервис или демон (например, `nginx.service`)
- **socket** — сокет для активации сервисов по требованию (`cups.socket`)
- **device** — устройство ядра (`dev-sda.device`)
- **mount** — точка монтирования (`mnt-data.mount`)
- **automount** — автоматическое монтирование
- **target** — группа юнитов (аналог runlevel, например `multi-user.target`)
- **timer** — запуск заданий по расписанию (`backup.timer`)
- **path** — отслеживание изменений в файловой системе
- **slice** — группы процессов для управления ресурсами (cgroups)
- **scope** — единичный набор процессов (обычно создаётся автоматически)

---

## 🔹 Где хранятся Unit-файлы
- `/etc/systemd/system/` — юниты администратора (приоритетные)
- `/lib/systemd/system/` или `/usr/lib/systemd/system/` — системные юниты
- `~/.config/systemd/user/` — пользовательские юниты

---

## 🔹 Структура Unit-файла
Пример `myapp.service`:

[Unit]
Description=My Application
After=network.target

[Service]
ExecStart=/usr/bin/python3 /opt/myapp/app.py
WorkingDirectory=/opt/myapp
Restart=always
User=www-data

[Install]
WantedBy=multi-user.target

</details>

 - ## 1. Написать service, который будет раз в 30 секунд мониторить лог на предмет наличия ключевого слова (файл лога и ключевое слово должны задаваться в /etc/default).

- **root@ol-apl-ubuntu:~# cat > /etc/default/watchlog**
- #Configuration file for my watchlog service
- #Place it to /etc/default

- #File and word in that file that we will be monit
- WORD="**ALERT**"
- LOG=/var/log/watchlog.log

- **root@ol-apl-ubuntu:~# cat /var/log/syslog > /var/log/watchlog.log** # И потом в строки кое-где добавляем ключевое слово ‘**ALERT**’
- **root@ol-apl-ubuntu:~# cat > /opt/watchlog.sh**
#!/bin/bash

- WORD=$1
- LOG=$2
- DATE=`date`

- if grep $WORD $LOG &> /dev/null
- then
- logger "$DATE: I found word, Master!" # Команда logger отправляет лог в системный журнал.
- else
- exit 0
- fi

- **root@ol-apl-ubuntu:~# vim /opt/watchlog.sh**
- **root@ol-apl-ubuntu:~# chmod +x /opt/watchlog.sh**
- **root@ol-apl-ubuntu:~# cat > /etc/systemd/system/watchlog.service** # Создадим юнит для сервиса
- [Unit]
- Description=My watchlog service

- [Service]
- Type=oneshot
- EnvironmentFile=/etc/default/watchlog
- ExecStart=/opt/watchlog.sh $WORD $LOG
- **root@ol-apl-ubuntu:~# cat > /etc/systemd/system/watchlog.timer** # Создадим юнит для таймера
- [Unit]
- Description=Run watchlog script every 30 second

- [Timer]
- #Run every 30 second
- OnUnitActiveSec=30
- Unit=watchlog.service

- [Install]
- WantedBy=multi-user.target

- **root@ol-apl-ubuntu:~# systemctl start watchlog.timer** # запускаем таймер
- **root@ol-apl-ubuntu:~# systemctl start watchlog.service** # таймер не работал пока не запустил сервис (?)
- **root@ol-apl-ubuntu:~# tail -f 1000 /var/log/syslog  | grep word** #  и время указанное в timer не точно работает...
- **root@ol-apl-ubuntu:~# vi /etc/systemd/system/watchlog.timer** # после 30 поставил "s" -seconds, ничего не изменилось (таймер срабатывает не точно раз в 30 секунд)
- **root@ol-apl-ubuntu:~# sudo systemctl daemon-reload**
- **root@ol-apl-ubuntu:~# sudo systemctl enable --now /etc/systemd/system/watchlog.timer**
- **root@ol-apl-ubuntu:~# tail -f 1000 /var/log/syslog  | grep word**
- tail: cannot open '1000' for reading: No such file or directory
- 2025-10-01T16:57:44.553189+03:00 ol-apl-ubuntu root: Wed Oct  1 04:57:44 PM MSK 2025: I found word, Master!
- 2025-10-01T16:58:42.720890+03:00 ol-apl-ubuntu root: Wed Oct  1 04:58:42 PM MSK 2025: I found word, Master!
- 2025-10-01T16:59:52.724261+03:00 ol-apl-ubuntu root: Wed Oct  1 04:59:52 PM MSK 2025: I found word, Master!
- 2025-10-01T17:00:52.719809+03:00 ol-apl-ubuntu root: Wed Oct  1 05:00:52 PM MSK 2025: I found word, Master!
- 2025-10-01T17:01:52.720875+03:00 ol-apl-ubuntu root: Wed Oct  1 05:01:52 PM MSK 2025: I found word, Master!
- 2025-10-01T17:02:52.722077+03:00 ol-apl-ubuntu root: Wed Oct  1 05:02:52 PM MSK 2025: I found word, Master!
- 2025-10-01T17:03:42.719089+03:00 ol-apl-ubuntu root: Wed Oct  1 05:03:42 PM MSK 2025: I found word, Master!
- 2025-10-01T17:04:32.719106+03:00 ol-apl-ubuntu root: Wed Oct  1 05:04:32 PM MSK 2025: I found word, Master!
- 2025-10-01T17:05:42.721282+03:00 ol-apl-ubuntu root: Wed Oct  1 05:05:42 PM MSK 2025: I found word, Master!
- 2025-10-01T17:06:42.716960+03:00 ol-apl-ubuntu root: Wed Oct  1 05:06:42 PM MSK 2025: I found word, Master!

- 
- ## 2. Установить spawn-fcgi и создать unit-файл (spawn-fcgi.sevice) с помощью переделки init-скрипта
- 
- **root@ol-apl-ubuntu:~# apt install spawn-fcgi php php-cgi php-cli  apache2 libapache2-mod-fcgid -y** # Устанавливаем spawn-fcgi и необходимые для него пакеты
- **root@ol-apl-ubuntu:~# cat > /etc/spawn-fcgi/fcgi.conf**
- -bash: /etc/spawn-fcgi/fcgi.conf: No such file or directory

- **root@ol-apl-ubuntu:~# mkdir /etc/spawn-fcgi** # создаем файл с настройками для будущего сервиса
- **root@ol-apl-ubuntu:~# cat > /etc/spawn-fcgi/fcgi.conf**
- #You must set some working options before the "spawn-fcgi" service will work.
- #If SOCKET points to a file, then this file is cleaned up by the init script.
- 
- #See spawn-fcgi(1) for all possible options.
- 
- #Example :
- SOCKET=/var/run/php-fcgi.sock
- OPTIONS="-u www-data -g www-data -s $SOCKET -S -M 0600 -C 32 -F 1 -- /usr/bin/php-cgi"
- **root@ol-apl-ubuntu:~# vim /etc/spawn-fcgi/fcgi.conf** # проверяем
- **root@ol-apl-ubuntu:~# cat > /etc/systemd/system/spawn-fcgi.service** # юнит-файл
- [Unit]
- Description=Spawn-fcgi startup service by Otus
- After=network.target

- [Service]
- Type=simple
- PIDFile=/var/run/spawn-fcgi.pid
- EnvironmentFile=/etc/spawn-fcgi/fcgi.conf
- ExecStart=/usr/bin/spawn-fcgi -n $OPTIONS
- KillMode=process

- [Install]
- WantedBy=multi-user.target
- **oot@ol-apl-ubuntu:~# vim  /etc/systemd/system/spawn-fcgi.service** # проверяем
- **root@ol-apl-ubuntu:~# systemctl start spawn-fcgi**
- **root@ol-apl-ubuntu:~# systemctl status spawn-fcgi**
- ● spawn-fcgi.service - Spawn-fcgi startup service by Otus
- Loaded: loaded (/etc/systemd/system/spawn-fcgi.service; disabled; preset: enabled)
- Active: active (running) since Fri 2025-10-03 11:19:00 MSK; 10s ago
- Main PID: 37457 (php-cgi)
- Tasks: 33 (limit: 2268)
- Memory: 14.5M (peak: 14.5M)
- CPU: 38ms
- CGroup: /system.slice/spawn-fcgi.service
-  ├─37457 /usr/bin/php-cgi
-  ├─37458 /usr/bin/php-cgi
-  ├─37459 /usr/bin/php-cgi
-  ...

-  ## 3. Доработать unit-файл Nginx (nginx.service) для запуска нескольких инстансов сервера с разными конфигурационными файлами одновременно

- **root@ol-apl-ubuntu:~# apt install nginx -y** # Установим Nginx из стандартного репозитория
- **root@ol-apl-ubuntu:~# cat > /etc/systemd/system/nginx@.service** # Для запуска нескольких экземпляров сервиса модифицируем исходный service для использования различной конфигурации, а также PID-файлов. Для этого создадим новый Unit для работы с шаблонами
- #Stop dance for nginx
- #=======================
- #
- #ExecStop sends SIGSTOP (graceful stop) to the nginx process.
- #If, after 5s (--retry QUIT/5) nginx is still running, systemd takes control
- #and sends SIGTERM (fast shutdown) to the main process.
- #After another 5s (TimeoutStopSec=5), and if nginx is alive, systemd sends
- #SIGKILL to all the remaining processes in the process group (KillMode=mixed).
- #
- #nginx signals reference doc:
- #http://nginx.org/en/docs/control.html
- #
- [Unit]
- Description=A high performance web server and a reverse proxy server
- Documentation=man:nginx(8)
- After=network.target nss-lookup.target

- [Service]
- Type=forking
- PIDFile=/run/nginx-%I.pid
- ExecStartPre=/usr/sbin/nginx -t -c /etc/nginx/nginx-%I.conf -q -g 'daemon on; master_process on;'
- ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx-%I.conf -g 'daemon on; master_process on;'
- ExecReload=/usr/sbin/nginx -c /etc/nginx/nginx-%I.conf -g 'daemon on; master_process on;' -s reload
- ExecStop=-/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx-%I.pid
- TimeoutStopSec=5
- KillMode=mixed

- [Install]
- WantedBy=multi-user.target

- **root@ol-apl-ubuntu:~# vim /etc/systemd/system/nginx@.service** # проверяем
- **root@ol-apl-ubuntu:~# cp -p  /etc/nginx/nginx.conf /etc/nginx/nginx-first.conf** # создем два файла конфигурации (/etc/nginx/nginx-first.conf, /etc/nginx/nginx-second.conf).  из стандартного конфига /etc/nginx/nginx.conf, с модификацией путей до PID-файлов и разделением по портам
- **@ol-apl-ubuntu:~# cp -p  /etc/nginx/nginx.conf /etc/nginx/nginx-second.conf**
- **@ol-apl-ubuntu:~# vim /etc/nginx/nginx-fist.conf**
- ...
- pid /run/**nginx-first.pid**;
- ...
- http {
-
- ##
- #Basic Settings
- ##
-
- sendfile on;
- tcp_nopush on;
- types_hash_max_size 2048;
- #server_tokens off;
- server {
- listen **9001**;
- }
- ...
- - #include /etc/nginx/sites-enabled/*;
- }
- ...
- #include /etc/nginx/sites-enabled/*;
- **@ol-apl-ubuntu:~# vim /etc/nginx/nginx-fist.conf** # проверяем
- - ...
- pid /run/**nginx-second.pid**;
- ...
- http {
-
- ##
- #Basic Settings
- ##
-
- sendfile on;
- tcp_nopush on;
- types_hash_max_size 2048;
- #server_tokens off;
- server {
- listen **9002**;
- }
- ...
- - #include /etc/nginx/sites-enabled/*;
-
- **root@ol-apl-ubuntu:/etc/nginx# systemctl start nginx@first**
- **root@ol-apl-ubuntu:/etc/nginx# systemctl start nginx@second**
- **root@ol-apl-ubuntu:/etc/nginx# systemctl status nginx@second**
- ● nginx@second.service - A high performance web server and a reverse proxy server
- Loaded: loaded (/etc/systemd/system/nginx@.service; disabled; preset: enabled)
-   Active: active (running) since Fri 2025-10-03 14:22:35 MSK; 17min ago
-   Docs: man:nginx(8)
-   Process: 39470 ExecStartPre=/usr/sbin/nginx -t -c /etc/nginx/nginx-second.conf -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
-   Process: 39475 ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx-second.conf -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
-   Main PID: 39477 (nginx)
-   Tasks: 2 (limit: 2268)
-   Memory: 1.7M (peak: 1.9M)
-   CPU: 11ms
-   CGroup: /system.slice/system-nginx.slice/nginx@second.service
-   ├─39477 "nginx: master process /usr/sbin/nginx -c /etc/nginx/nginx-second.conf -g daemon on; master_process on;"
-   └─39478 "nginx: worker process"

- Oct 03 14:22:35 ol-apl-ubuntu systemd[1]: Starting nginx@second.service - A high performance web server and a reverse proxy server...
- Oct 03 14:22:35 ol-apl-ubuntu systemd[1]: Started nginx@second.service - A high performance web server and a reverse proxy server.
- **root@ol-apl-ubuntu:/etc/nginx# ss -tnulp | grep nginx** # смотрим какие порты слушаются:
- tcp   LISTEN 0      511               0.0.0.0:9001      0.0.0.0:*    users:(("nginx",pid=39765,fd=5),("nginx",pid=39764,fd=5))
- tcp   LISTEN 0      511               0.0.0.0:9002      0.0.0.0:*    users:(("nginx",pid=39478,fd=5),("nginx",pid=39477,fd=5))

- **root@ol-apl-ubuntu:/etc/nginx# ps afx | grep nginx** # смотрим список процессов
-   39591 pts/1    Tl     0:00                          \_ vim nginx-first.conf
-   39813 pts/1    S+     0:00                          \_ grep --color=auto nginx
-   39477 ?        Ss     0:00 nginx: master process /usr/sbin/nginx -c /etc/nginx/nginx-second.conf -g daemon on; master_process on;
-   39478 ?        S      0:00  \_ nginx: worker process
-   39764 ?        Ss     0:00 nginx: master process /usr/sbin/nginx -c /etc/nginx/nginx-first.conf -g daemon on; master_process on;
-   39765 ?        S      0:00  \_ nginx: worker process

## 10 урок
**Домашнее задание** <ins>"Systemd - создание unit-файла"</ins>

-  Цель: написать bash-скрипт, который ежечасно формирует и отправляет на email отчёт о работе веб-сервера;

🎯**Задание**
- Написать скрипт для CRON, который раз в час формирует отчёт и отправляет его на заданную почту.


- **Отчёт должен содержать:**

- IP-адреса с наибольшим числом запросов (с момента последнего запуска);
- Запрашиваемые URL с наибольшим числом запросов (с момента последнего запуска);
- Ошибки веб-сервера/приложения (с момента последнего запуска);
- HTTP-коды ответов с указанием их количества (с момента последнего запуска).
- Скрипт должен предотвращать одновременный запуск нескольких копий, до его завершения.
- В письме должен быть прописан обрабатываемый временной диапазон.
  
<details>
<summary> = Теория = </summary>
# 🧩 Регулярные выражения в Linux (Regex Cheatsheet)

> 📘 Регулярные выражения (Regular Expressions, RegEx) — это шаблоны для поиска, фильтрации и обработки текста в Linux и других системах.  
> Работают в `grep`, `sed`, `awk`, `perl`, `bash` и многих других утилитах.

---

## 🧠 Основные метасимволы

| Символ | Значение | Пример | Совпадения |
|:-------|:----------|:--------|:-------------|
| `.` | Любой символ | `a.b` | `acb`, `a_b`, `a9b` |
| `^` | Начало строки | `^INFO` | `INFO: start` |
| `$` | Конец строки | `end$` | `The end` |
| `*` | 0 или больше повторений | `lo*l` | `ll`, `lol`, `loool` |
| `+` | 1 или больше повторений | `go+d` | `good`, `gooood` |
| `?` | 0 или 1 повторение | `colou?r` | `color`, `colour` |
| `[]` | Класс символов | `[A-Z]` | Любая заглавная буква |
| `[^]` | Исключение | `[^0-9]` | Любой символ, кроме цифры |
| `{n,m}` | Повторы от n до m | `[0-9]{2,4}` | Числа длиной 2–4 цифры |
| `()` | Группа | `(abc)+` | Повтор группы `abc` |
| `|` | Логическое “или” | `cat|dog` | `cat` или `dog` |
| `\` | Экранирование | `\.` | Точка `.` |

---

## 🔍 Использование в Linux

### grep

- grep -E "^ERROR" /var/log/syslog # Поиск строк, начинающихся с ERROR

- grep -Eo "([0-9]{1,3}\.){3}[0-9]{1,3}" access.log # Вывод только совпадений (IP-адресов)

- sed -E 's/[0-9]+/NUM/g' file.txt # Заменяет все числа на слово NUM

awk '/ERROR|CRITICAL/ {print $0}' /var/log/app.log # Выводит строки с ERROR или CRITICAL

- Назначение					Шаблон													Пример
- IP-адрес					([0-9]{1,3}\.){3}[0-9]{1,3}								192.168.1.10
- Email						[[:alnum:]\._%+-]+@[[:alnum:]\.-]+\.[a-z]{2,}			user@mail.com
- URL							https?://[a-zA-Z0-9\./_-]+								https://example.com/test
- Дата (dd/mm/yyyy)			[0-9]{2}/[0-9]{2}/[0-9]{4}								08/10/2025
- Ошибки логов				`(ERROR													CRITICAL
- HTTP-коды					\" [0-9]{3}												" 404
- Время (HH:MM:SS)			[0-9]{2}:[0-9]{2}:[0-9]{2}								12:30:45

- ⚙️ В Bash
- line="192.168.0.1"
- if [[ $line =~ ^([0-9]{1,3}\.){3}[0-9]{1,3}$ ]]; then
-     echo "Это IP-адрес"
- fi

- 📎 Пример: анализ лога Nginx
- LOG=/var/log/nginx/access.log

- # Частые IP
- grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' "$LOG" | sort | uniq -c | sort -nr | head

- # Частые URL
- grep -Eo '"(GET|POST) [^ ]+' "$LOG" | cut -d' ' -f2 | sort | uniq -c | sort -nr | head

- # Ошибки
- grep -E "error|crit|alert" /var/log/nginx/error.log

</details>
 
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx

## 🚀 Скрипт
- **root@ol-apl-ubuntu:/usr/local/bin# cat my_report2.sh**
```bash
#!/bin/bash
# Скрипт: my_report.sh
# Написать скрипт, который формирует отчёт и отправляет его на заданную почту.
# Ключевые моменты скрипта:
#	1.Блокировка через flock предотвращает одновременный запуск нескольких копий.
#	2.STATEFILE хранит время последнего запуска, чтобы учитывать только новые строки лога.
#	3.AWK-парсер извлекает дату из формата [07/Oct/2025:10:43:56 +0300] и сравнивает её с последним запуском.
#	4.Топ IP и URL считаются через awk, sort, uniq -c.
#	5.Ошибки и HTTP-коды подсчитываются отдельно.
#	6.Отправка через mail автоматически шлёт отчёт на e-mail.
#	7.TMPFILE + очистка — аккуратное временное хранение отчёта.


# === Настройки ===
LOGFILE="/var/log/nginx/example.local.access.log" # Путь к лог-файлу веб-сервера
STATEFILE="/var/tmp/web_report_state" # Файл для хранения времени последнего запуска
LOCKFILE="/var/tmp/web_report.lock"  # Файл блокировки, чтобы не запускать одновременно несколько копий
MAIL_TO="spg@garant.ru" # Почта, куда отправляется отчёт
HOSTNAME=$(hostname) # Имя хоста для включения в отчёт

# === Проверка на одновременный запуск ===
exec 9>"$LOCKFILE" # Открываем дескриптор 9 на LOCKFILE
if ! flock -n 9; then # Пытаемся захватить блокировку без ожидания
   echo "[$(date)] Уже запущено, выходим."
    exit 1
fi

# === Время последнего запуска ===
if [ -f "$STATEFILE" ]; then
    LAST_RUN=$(cat "$STATEFILE") # Читаем время последнего запуска
else
    LAST_RUN=0 # Если файл отсутствует — первый запуск
fi
CURRENT_TIME=$(date +%s) # Текущее время в формате UNIX timestamp

# === Извлечение новыx строк из лога (# Берём только строки, созданные после последнего запуска)===
NEWLINES=$(awk -v last="$LAST_RUN" '
    match($0, /\[([0-9]{2})\/([A-Za-z]{3})\/([0-9]{4}):([0-9]{2}:[0-9]{2}:[0-9]{2}) ([+\-][0-9]{4})\]/, m) {
        day = m[1]; mon = m[2]; year = m[3]; time = m[4]; tz = m[5];
        formatted = day " " mon " " year " " time " " tz # Преобразуем для date
        cmd = "date -d \"" formatted "\" +%s" # Преобразуем в UNIX timestamp
        cmd | getline t
        close(cmd)
        if (t > last) print $0 # Если новее LAST_RUN, выводим
    }
' "$LOGFILE")
# Если новых строк нет, заканчиваем работу
if [ -z "$NEWLINES" ]; then
    echo "[$(date)] Нет новых строк в логе, отчёт не требуется."
    echo "$CURRENT_TIME" > "$STATEFILE"
    exit 0
fi

# === Формируем отчёт ===
TMPFILE=$(mktemp) # Временный файл для отчёта
{
    echo "Отчёт о веб-трафике с сервера $HOSTNAME"
    echo "Период: $(date -d "@$LAST_RUN") — $(date -d "@$CURRENT_TIME")"
    echo
    echo "=== Топ-10 IP-адресов ==="
    echo "$NEWLINES" | awk '{print $1}' | sort | uniq -c | sort -nr | head -10
    echo
    echo "=== Топ-10 запрашиваемых URL ==="
    echo "$NEWLINES" | awk '{for (i=1;i<=NF;i++) if ($i ~ /^"?GET|POST|HEAD$/) print $(i+1)}' | sort | uniq -c | sort -nr | head -10
    echo
    echo "=== Ошибки (HTTP 4xx/5xx) ==="
    echo "$NEWLINES" | awk '$9 ~ /^[45][0-9][0-9]$/' | tail -20
    echo
    echo "=== Коды ответов ==="
    echo "$NEWLINES" | awk '{print $9}' | grep -E '^[0-9]{3}$' | sort | uniq -c | sort -nr
} > "$TMPFILE"

# === Отправляем отчёт по почте ===
mail -s "Web report $HOSTNAME ($(date))" "$MAIL_TO" < "$TMPFILE"

# === Обновляем время последнего запуска ===
echo "$CURRENT_TIME" > "$STATEFILE"

# === Очистка ===
rm -f "$TMPFILE"
flock -u 9
rm -f "$LOCKFILE"
```
- 
- **Письмо-отчет**
- Subject: Web report ol-apl-ubuntu (Fri Oct 10 11:19:55 AM MSK 2025)
- To: <spg@garant.ru>
- User-Agent: mail (GNU Mailutils 3.17)
- Date: Fri, 10 Oct 2025 11:19:55 +0300
- Message-Id: <20251010081955.E350E65811@ol-apl-ubuntu.garant.ru>
- From: root <root@ol-apl-ubuntu.garant.ru>

- Отчёт о веб-трафике с сервера ol-apl-ubuntu
- **Период: Tue Oct  7 12:14:15 PM MSK 2025 — Fri Oct 10 11:19:55 AM MSK 2025**

- === Топ-10 IP-адресов ===
- 46 10.0.77.13
- 7  10.0.77.5

- === Топ-10 запрашиваемых URL ===
- 20/about.html
- 16 /about.html
- 12 /index.html
- 5 /contact.html

- === Ошибки (HTTP 4xx/5xx) ===
- 10.0.77.13 - - [10/Oct/2025:10:54:37 +0300] "GET /apple-touch-icon-precomposed.png HTTP/1.1" 404 134 "-" "com.apple.WebKit.Networking/21622.1.22.11.15Network/5569.1.3 macOS/26.0.1"
- 10.0.77.13 - - [10/Oct/2025:10:54:37 +0300] "GET /apple-touch-icon.png HTTP/1.1" 404 134 "-" "com.apple.WebKit.Networking/21622.1.22.11.15 Network/5569.1.3 macOS/26.0.1"
- 10.0.77.13 - - [10/Oct/2025:10:54:37 +0300] "GET /favicon.ico HTTP/1.1" 404 134 "-" "com.apple.WebKit.Networking/21622.1.22.11.15 Network/5569.1.3  macOS/26.0.1"
- 10.0.77.13 - - [10/Oct/2025:11:11:51 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.0.1 Safari/605.1.15"
- 10.0.77.13 - - [10/Oct/2025:11:12:45 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.0.1 Safari/605.1.15"
- 10.0.77.13 - - [10/Oct/2025:11:18:46 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.0.1 Safari/605.1.15"
- 10.0.77.13 - - [10/Oct/2025:11:19:01 +0300] "GET /apple-touch-icon-precomposed.png HTTP/1.1" 404 134 "-" "com.apple.WebKit.Networking/21622.1.22.11.15 Network/5569.1.3 macOS/26.0.1"
- 10.0.77.13 - - [10/Oct/2025:11:19:01 +0300] "GET /apple-touch-icon.png HTTP/1.1" 404 134 "-" "com.apple.WebKit.Networking/21622.1.22.11.15 Network/5569.1.3 macOS/26.0.1"
- 10.0.77.13 - - [10/Oct/2025:11:19:01 +0300] "GET /favicon.ico HTTP/1.1" 404 134 "-" "com.apple.WebKit.Networking/21622.1.22.11.15 Network/5569.1.3 macOS/26.0.1"
- 10.0.77.5 - - [10/Oct/2025:11:19:05 +0300] "GET /favicon.ico HTTP/1.1" 404 134 "http://10.0.77.142/about.html" "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:142.0) Gecko/20100101 Firefox/142.0"
- 10.0.77.13 - - [10/Oct/2025:11:19:18 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.0.1 Safari/605.1.15"
- 10.0.77.13 - - [10/Oct/2025:11:19:20 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.0.1 Safari/605.1.15"
- 10.0.77.13 - - [10/Oct/2025:11:19:35 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:143.0) Gecko/20100101 Firefox/143.0"
- 10.0.77.13 - - [10/Oct/2025:11:19:38 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:143.0) Gecko/20100101 Firefox/143.0"
- 10.0.77.13 - - [10/Oct/2025:11:19:39 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:143.0) Gecko/20100101 Firefox/143.0"
- 10.0.77.13 - - [10/Oct/2025:11:19:39 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:143.0) Gecko/20100101 Firefox/143.0"

- === Коды ответов ===
- 19 200
- 18 304
- 16 404
- **root@ol-apl-ubuntu:/usr/local/bin# ./my_report2.sh** # повторно запускаем скрипт без обращений к тестовому сайту
- [Fri Oct 10 11:25:54 AM MSK 2025] Нет новых строк в логе, отчёт не требуется.
- **root@ol-apl-ubuntu:/usr/local/bin# ./my_report2.sh** # еще раз запускаем скрипт после обращений к тестовому сайту
- **root@ol-apl-ubuntu:/usr/local/bin# mail -u spg** # смотрим отчет в почте
- - **Письмо-отчет**
- >N  26 root               Fri Oct 10 11:28  27/1267  Web report ol-apl-ubuntu (Fri Oct 10 11:28:52 AM MSK 2025)
- ? 26
- Return-Path: <root@ol-apl-ubuntu.garant.ru>
- X-Original-To: spg@garant.ru
- Delivered-To: spg@garant.ru
- Received: by ol-apl-ubuntu.garant.ru (Postfix, from userid 0)
- 	id C979665964; Fri, 10 Oct 2025 11:28:52 +0300 (MSK)
- Subject: Web report ol-apl-ubuntu (Fri Oct 10 11:28:52 AM MSK 2025)
- To: <spg@garant.ru>
- User-Agent: mail (GNU Mailutils 3.17)
- Date: Fri, 10 Oct 2025 11:28:52 +0300
- Message-Id: <20251010082852.C979665964@ol-apl-ubuntu.garant.ru>
- From: root <root@ol-apl-ubuntu.garant.ru>

- Отчёт о веб-трафике с сервера ol-apl-ubuntu
- **Период: Fri Oct 10 11:25:54 AM MSK 2025 — Fri Oct 10 11:28:52 AM MSK 2025**

- === Топ-10 IP-адресов ===
- 12 10.0.77.13
- 7  10.0.77.5
- 
- === Топ-10 запрашиваемых URL ===
- 8 /about.html
- 6 /contact.html
- 4 /index.html
- 1 /about.htmlhttp://10.0.77.142/about.html

- === Ошибки (HTTP 4xx/5xx) ===
- 10.0.77.13 - - [10/Oct/2025:11:28:30 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.0.1 Safari/605.1.15"
- 10.0.77.13 - - [10/Oct/2025:11:28:42 +0300] "GET /%3C?php HTTP/1.1" 404 134 "http://10.0.77.142/contact.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:143.0) Gecko/20100101 Firefox/143.0"

- === Коды ответов ===
- 3 304
- 2 404
---
- ## Переодичность запуска через CRON
- **root@ol-apl-ubuntu:/usr/local/bin# crontab -e** #  прописываем в CRON
- 0 * * * * → каждый час в нулевую минуту
- /usr/local/bin/report.sh → путь к скрипту
- >> /var/log/report.log 2>&1 → перенаправление вывода и ошибок в лог

- 0 * * * * /usr/local/bin/my_reporti2.sh >> /var/log/my_report.log 2>&1
---
- ## Переодичность запуска через сервис по таймеру (материалы предыдущего ДЗ)
- **root@ol-apl-ubuntu:/usr/local/bin# vim /etc/systemd/system/my_report.service**
- [Unit]
- Description=My watchlog service

- [Service]
- Type=oneshot
- EnvironmentFile=/var/log/nginx/example.local.access.log
- ExecStart=/usr/local/bin/my_report2.sh


- **root@ol-apl-ubuntu:/usr/local/bin# vim /etc/systemd/system/my_report.timere**
- Unit]
- Description=Run my_report2 script every 60 second

- [Timer]
- #Run every 60 second
- OnUnitActiveSec=60
- Unit=my_report.service

- [Install]
- WantedBy=multi-user.target



- **root@ol-apl-ubuntu:/usr/local/bin# mail -u spg**
- 30 root               Fri Oct 10 13:42  29/901   Web report ol-apl-ubuntu (Fri Oct 10 01:42:45 PM MSK 2025)
- ? quit
- Held 30 messages in /var/mail/spg
- root@ol-apl-ubuntu:/usr/local/bin# systemctl start my_report.service
- root@ol-apl-ubuntu:/usr/local/bin# systemctl start my_report.timer
- root@ol-apl-ubuntu:/usr/local/bin# systemctl daemon-reload
- root@ol-apl-ubuntu:/usr/local/bin# systemctl enable --now /etc/systemd/system/my_report.timer
- Created symlink /etc/systemd/system/multi-user.target.wants/my_report.timer → /etc/systemd/system/my_report.timer.>N  31 root               Fri Oct 10 - - 14:45  26/868   Web report ol-apl-ubuntu (Fri Oct 10 02:45:00 PM MSK 2025)
- **root@ol-apl-ubuntu:/usr/local/bin# mail -u spg**
- >N  31 root               Fri Oct 10 14:45  26/868   Web report ol-apl-ubuntu (Fri Oct 10 02:45:00 PM MSK 2025)
- ? 31
- Return-Path: <root@ol-apl-ubuntu.garant.ru>
- X-Original-To: spg@garant.ru
- Delivered-To: spg@garant.ru
- Received: by ol-apl-ubuntu.garant.ru (Postfix, from userid 0)
- 	id BC69465811; Fri, 10 Oct 2025 14:45:00 +0300 (MSK)
- Subject: Web report ol-apl-ubuntu (Fri Oct 10 02:45:00 PM MSK 2025)
- To: <spg@garant.ru>
- User-Agent: mail (GNU Mailutils 3.17)
- Date: Fri, 10 Oct 2025 14:45:00 +0300
- Message-Id: <20251010114500.BC69465811@ol-apl-ubuntu.garant.ru>
- From: root <root@ol-apl-ubuntu.garant.ru>

- Отчёт о веб-трафике с сервера ol-apl-ubuntu
- Период: Fri Oct 10 02:33:38 PM MSK 2025 — Fri Oct 10 02:45:00 PM MSK 2025

- === Топ-10 IP-адресов ===
- 2 10.0.77.13

- === Топ-10 запрашиваемых URL ===
- 1 /styles.css
- 1 /contact.html

- === Ошибки (HTTP 4xx/5xx) ===

- === Коды ответов ===
- 2 304

- **Работает**

## 12 урок
**Домашнее задание** <ins>"Работа с процессами"</ins>

-  Цель: Работать с процессами;

🎯**Задание**
- написать свою реализацию lsof.


- **Отчёт должен содержать:**

- Понимание работы утилиты с файлами;

  
<details>
<summary> = Теория = </summary>

📂 Структура каталога /proc
🧩 1. Общесистемная информация

- **/proc/cpuinfo** - Информация о процессоре: модель, частота, количество ядер, флаги.
- **/proc/meminfo**  - Подробности об использовании оперативной памяти.
- **/proc/uptime** - Время работы системы с момента загрузки.
- **/proc/loadavg** - Средняя нагрузка системы за 1, 5 и 15 минут.
- **/proc/version** - Версия ядра и компилятора.
- **/proc/cmdline** - Параметры, переданные ядру при загрузке.
- **/proc/modules** - Загруженные модули ядра.
- **/proc/filesystems** - Поддерживаемые файловые системы.
- **/proc/partitions** - Таблица разделов на устройствах.
- **/proc/diskstats** - Статистика чтения/записи для каждого блока.
- **/proc/interrupts** - Счётчики аппаратных прерываний.
- **/proc/swaps** - Используемые swap-разделы.
- **/proc/mounts** - Точки монтирования и используемые файловые системы.
- **/proc/ioports** - Аппаратные порты ввода/вывода.
- **/proc/iomem** - Карта распределения физической памяти.
- **/proc/net/** - Подкаталог с информацией о сетевых интерфейсах и соединениях.
- **/proc/sys/** - Интерфейс настройки параметров ядра (sysctl).

👤 2. Каталоги процессов
- Каждый запущенный процесс имеет свой каталог /proc/[pid]/, где [pid] — его числовой идентификатор.
- Например: /proc/1234/

- **/proc/[pid]/cmdline** - Команда и аргументы, с которыми процесс был запущен.
- **/proc/[pid]/cwd** - Ссылка на текущий рабочий каталог процесса.
- **/proc/[pid]/environ** - Переменные окружения.
- **/proc/[pid]/exe** - Симлинк на исполняемый файл.
- **/proc/[pid]/fd/** - Дескрипторы открытых файлов.
- **/proc/[pid]/maps** - Карта памяти процесса.
- **/proc/[pid]/mem** - Содержимое памяти процесса (только для чтения root).
- **/proc/[pid]/stat** - Статистика: состояние, использование CPU и памяти, приоритет и т. д.
- **/proc/[pid]/status** - Удобочитаемая сводка по процессу (UID, VmRSS, состояние, приоритет).
- **/proc/[pid]/task/** - Потоки (threads) этого процесса.
- **/proc/[pid]/io** - Счётчики ввода/вывода.
- **/proc/[pid]/net/** - Сетевые соединения, связанные с этим процессом.
- **/proc/[pid]/mounts** - Список смонтированных ФС, видимых процессом (namespace).

⚙️ 3. Системные подкаталоги

- **/proc/bus/** - Информация о шинах (PCI, USB и др.).
- **/proc/driver/** - Информация от конкретных драйверов устройств.
- **/proc/sys/** - Дерево параметров ядра, управляемых через sysctl. Пример: /proc/sys/net/ipv4/ip_forward.
- **/proc/tty/** - Терминалы и их драйверы.
- **/proc/acpi/** - (Если включено) — информация об энергопотреблении, батарее, ACPI событиях.
- **/proc/scsi/** - Информация о SCSI-устройствах.


	
# 🧰 lsof — List Open Files

**`lsof`** (от _List Open Files_) — это системная утилита Linux/Unix, показывающая **все открытые файлы** в системе.  
В Linux всё является файлом — поэтому `lsof` отображает не только обычные файлы, но и:

- 📁 директории  
- ⚙️ устройства (`/dev/sda1`, `/dev/tty`)  
- 🌐 сетевые соединения (TCP/UDP)  
- 🔌 сокеты  
- 📚 библиотеки и маппинги памяти  
- 🧵 именованные каналы (pipes, FIFOs)

---

## 🧠 Основная идея

Каждый процесс в Linux имеет собственную таблицу **открытых файловых дескрипторов** (`/proc/<pid>/fd`).  
`lsof` обходит все процессы и выводит, какие файлы они открыли.

---

## 💡 Базовое использование

Показывает все открытые файлы всех процессов (часто длинный вывод, требует sudo).

🔍 Часто используемые опции
- Команда                   Описание
- **lsof -p <PID>** -           показать все файлы, открытые конкретным процессом
- **lsof <файл>** -             какие процессы держат файл открытым
- **lsof +D <каталог>** -       все открытые файлы внутри каталога (рекурсивно)
- **lsof -u <пользователь>** -  все файлы, открытые процессами пользователя
- **lsof -i** -                 все сетевые соединения
- **lsof -iTCP -sTCP:LISTEN** - процессы, слушающие TCP-порты
- **lsof -i :80** -             кто использует порт 80
- **lsof -a -u root -i** -      сетевые соединения процессов root
- **lsof /dev/sda1** -          процессы, использующие устройство /dev/sda1
- **lsof +L1** -                удалённые, но всё ещё занятые файлы
- 
📄 Пример вывода
- COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
- bash     1092 pavel  cwd  DIR  8,1     4096    2   /
- bash     1092 pavel  txt  REG  8,1   1113504 123 /usr/bin/bash
- bash     1092 pavel    0u  CHR 136,0      0t0  3 /dev/pts/0
- bash     1092 pavel    1u  CHR 136,0      0t0  3 /dev/pts/0
- bash     1092 pavel    2u  CHR 136,0      0t0  3 /dev/pts/0
- 
🧩 Расшифровка столбцов

- **COMMAND** -имя процесса
- **PID** - идентификатор процесса
- **USER** - владелец
- **FD** - дескриптор файла (0=stdin, 1=stdout, 2=stderr, cwd=текущий каталог, txt=исполняемый файл)
- **TYPE** - тип файла (REG, DIR, CHR, FIFO, IPv4, IPv6)
- **NAME** - путь к файлу или описание сокета

⚡ Полезные сценарии
- Цель                                  Команда
- 🔒 Кто держит файл открытым?          **lsof /var/log/syslog**
- 🌐 Что слушает порт 22?               **lsof -i :22**
- 🧹 Найти удалённые, но занятые файлы  **lsof +L1**
- 📂 Что открыто из каталога /mnt?      **lsof +D /mnt**
- 👤 Файлы пользователя                 **lsof -u $USER**

⚙️ Как это работает
- lsof использует данные из /proc:
- 	•	/proc/<pid>/fd/ — ссылки на открытые файлы
- 	•	/proc/<pid>/maps — маппинги памяти (библиотеки)
- 	•	/proc/net/* — сетевые сокеты
- На основе этих данных формируется таблица открытых файлов всех процессов.

---

🧠 Полезные приёмы **awk** для анализа **/proc**

📊 1. Использовать /proc/meminfo — анализ памяти
- **Показать общий объём и свободную память:**

```bash
awk '/MemTotal|MemFree|Buffers|Cached/ {print}' /proc/meminfo
```

- **Посчитать использование памяти в процентах:**

```bash
awk '/MemTotal/ {total=$2} /MemAvailable/ {avail=$2} END {printf "Memory used: %.1f%%\n", 100*(1-avail/total)}' /proc/meminfo
```

💻 2. /proc/cpuinfo — информация о процессоре
- **Показать все модели CPU:**

```bash  
awk -F': ' '/model name/ {print $2}' /proc/cpuinfo
```

- **Посчитать количество логических ядер:**

```bash  
awk '/^processor/ {n++} END {print "CPU cores:", n}' /proc/cpuinfo
```

🚀 3. /proc/loadavg — загрузка системы
- **Просто форматированный вывод:**

```bash  
awk '{printf "Load average: 1min=%s 5min=%s 15min=%s\n", $1, $2, $3}' /proc/loadavg
```

🔧 4. /proc/uptime — время работы системы
- **Сделать человекопонятный вывод аптайма:**

```bash  
aawk '{h=int($1/3600); m=int(($1%3600)/60); s=int($1%60); printf "Uptime: %dh %dm %ds\n", h, m, s}' /proc/uptime
```

🧩 5. /proc/[pid]/status — анализ процессов
- **Например, вывести всех процессов с использованием памяти > 100 000 KB:**

```bash  
for pid in /proc/[0-9]*; do
  awk -v pid=$(basename "$pid") '/VmRSS:/ {if ($2>100000) printf "%-6s %s KB\n", pid, $2}' "$pid/status" 2>/dev/null
done
```

🧱 6. /proc/[pid]/fd — подсчёт открытых файлов

```bash  
for pid in /proc/[0-9]*; do
  user=$(awk '/^Uid:/ {print $2}' "$pid/status" 2>/dev/null | xargs -I{} getent passwd {} | cut -d: -f1)
  [ -d "$pid/fd" ] && count=$(ls "$pid/fd" 2>/dev/null | wc -l)
  [ -n "$count" ] && echo "$pid $user $count"
done | awk '{if($3>50) printf "PID=%s USER=%s OPEN_FD=%s\n", $1,$2,$3}'
```

🧮 7. /proc/net/dev — статистика сетевых интерфейсов
- **Посчитать входящий/исходящий трафик:**

```bash  
awk 'NR>2 {print $1, "RX=" $2/1024 "KB", "TX=" $10/1024 "KB"}' /proc/net/dev
```

🔋 8. /proc/stat — использование CPU
- **Посчитать общий процент загрузки CPU за секунду:**

```bash  
awk '/^cpu / {u=$2; n=$3; s=$4; i=$5; total=u+n+s+i; printf "%d %d\n", u+s, total}' /proc/stat > /tmp/cpu1
sleep 1
awk '/^cpu / {u=$2; n=$3; s=$4; i=$5; total=u+n+s+i; printf "%d %d\n", u+s, total}' /proc/stat > /tmp/cpu2
awk 'NR==FNR{u1=$1;t1=$2;next}{u2=$1;t2=$2}END{printf "CPU usage: %.1f%%\n", 100*(u2-u1)/(t2-t1)}' /tmp/cpu1 /tmp/cpu2
```

🔥 10. /proc/swaps — использование swap

```bash  
awk 'NR>1 {printf "%s: %s/%s kB used\n", $1, $4, $3}' /proc/swaps
```

🧾 Бонус: всё сразу в виде короткого системного отчёта

```bash  
echo "=== CPU ==="
awk -F': ' '/model name/ {print $2; exit}' /proc/cpuinfo
awk '/^cpu / {printf "Load: %.1f%%\n", 100*($2+$4)/($2+$4+$5)}' /proc/stat

echo "=== MEM ==="
awk '/MemTotal|MemFree|Buffers|Cached/ {print}' /proc/meminfo

echo "=== UPTIME ==="
awk '{printf "Uptime: %.2f hours\n", $1/3600}' /proc/uptime
```
---
🧩 proc_monitor — мини-мониторинг из /proc # информативный Bash-скрипт

```bash  
#!/usr/bin/env bash
#
# proc_monitor — системная сводка на основе /proc
# Автор: ты :)
# Зависимости: только bash, awk, sleep
#

# === Цвета для красоты ===
RED="\033[1;31m"
GREEN="\033[1;32m"
YELLOW="\033[1;33m"
CYAN="\033[1;36m"
RESET="\033[0m"

while true; do
  clear
  echo -e "${CYAN}==== SYSTEM STATUS ($(date +"%F %T")) ====${RESET}"

  # ---- CPU ----
cpu_usage=$(awk '
  /^cpu / {
    u1=$2+$3+$4; t1=$2+$3+$4+$5+$6+$7+$8
    system("sleep 1")
    getline < "/proc/stat"
    u2=$2+$3+$4; t2=$2+$3+$4+$5+$6+$7+$8
    printf "%d", 100*(u2-u1)/(t2-t1)
  }' /proc/stat)
echo -e "${GREEN}CPU usage:${RESET} ${cpu_usage}%"

  # ---- MEMORY ----
  awk '
    /MemTotal:/ {total=$2}
    /MemAvailable:/ {avail=$2}
    END {
      used=total-avail;
      printf "\033[1;32mMemory:\033[0m %.1f%% used (%d / %d MB)\n", 100*used/total, used/1024, total/1024
    }
  ' /proc/meminfo

  # ---- LOAD AVG ----
  awk '{printf "\033[1;32mLoad avg:\033[0m 1min=%s 5min=%s 15min=%s\n", $1, $2, $3}' /proc/loadavg

  # ---- UPTIME ----
  awk '{h=int($1/3600); m=int(($1%3600)/60); printf "\033[1;32mUptime:\033[0m %dh %dm\n", h, m}' /proc/uptime

  # ---- PROCESSES ----
  procs=$(ls -d /proc/[0-9]* 2>/dev/null | wc -l)
  echo -e "${GREEN}Processes:${RESET} $procs"

  # ---- TOP 5 по памяти ----
  echo -e "\n${YELLOW}Top 5 processes by memory:${RESET}"
  printf "%-8s %-20s %10s\n" "PID" "COMMAND" "RSS(KB)"
  for pid in /proc/[0-9]*; do
    status="$pid/status"
    [ -r "$status" ] || continue
    rss=$(awk '/VmRSS:/ {print $2}' "$status")
    comm=$(<"$pid/comm")
    [ -n "$rss" ] && printf "%-8d %-20s %10d\n" "$(basename "$pid")" "$comm" "$rss"
  done | sort -k3 -nr | head -n 5

  # ---- DISK ----
  echo -e "\n${YELLOW}Disk activity (/proc/diskstats):${RESET}"
  awk '{if ($3 ~ /^sd|nvme|vd/) printf "%-6s reads=%-8s writes=%-8s\n", $3, $4, $8}' /proc/diskstats

  # ---- NET ----
  echo -e "\n${YELLOW}Network traffic (/proc/net/dev):${RESET}"
  awk 'NR>2 {printf "%-8s RX=%-10.0fKB TX=%-10.0fKB\n", $1, $2/1024, $10/1024}' /proc/net/dev

  echo
  sleep 7
done
```

</details>

---

## Домашнее задание

- **root@ol-apl-ubuntu:/usr/local/bin# cat /proc/cpuinfo** # инфо о процессоре
- processor	: 0
- vendor_id	: GenuineIntel
- cpu family	: 6
- model		: 85
- model name	: Intel(R) Xeon(R) Gold 6238R CPU @ 2.20GHz
- stepping	: 7
- microcode	: 0x5003707
- cpu MHz		: 2194.843
- cache size	: 39424 KB
- physical id	: 0
- siblings	: 1
- core id		: 0
- cpu cores	: 1

- **root@ol-apl-ubuntu:/usr/local/bin# grep Mem /proc/meminfo** # Инфо о памяти
- MemTotal:        2015348 kB
- MemFree:          795792 kB
- MemAvailable:    1578184 kB

- **root@ol-apl-ubuntu:/usr/local/bin# cat /proc/swaps** # использование SWAP
- Filename				Type		Size		Used		Priority
- /swap.img                               file		2097148		0		-2

- **root@ol-apl-ubuntu:/usr/local/bin# cat /proc/net/dev сетевые** # инетерфейсы
- Inter-|   Receive                                                |  Transmit
- face |bytes    packets errs drop fifo frame compressed multicast|bytes    packets errs drop fifo colls carrier compressed
- lo:  168351    1785    0    0    0     0          0         0   168351    1785    0    0    0     0       0          0
- ens192: 189391314 1782688    0  712    0     0          0      5071 39149174  324460    0    0    0     0       0          0

- **root@ol-apl-ubuntu:/usr/local/bin# cat /proc/mounts** # монтирование файловой системы
- sysfs /sys sysfs rw,nosuid,nodev,noexec,relatime 0 0
- proc /proc proc rw,nosuid,nodev,noexec,relatime 0 0
- udev /dev devtmpfs rw,nosuid,relatime,size=967776k,nr_inodes=241944,mode=755,inode64 0 0
- devpts /dev/pts devpts rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000 0 0
- tmpfs /run tmpfs rw,nosuid,nodev,noexec,relatime,size=201536k,mode=755,inode64 0 0
- /dev/mapper/ubuntu--otus-ubuntu--lv / ext4 rw,relatime 0 0
- ...



# Минимальный аналог lsof на Perl
# Показывает: COMMAND PID USER FD NAME
- **root@ol-apl-ubuntu:/usr/local/bin# vim my_lsof2.pl**

```bash

#!/usr/bin/env perl
use strict; # жёсткий режим проверки синтаксиса.
use warnings; # вывод предупреждений о потенциальных ошибках
use File::Basename; # использовать имя скрипта

opendir(my $proc, "/proc") or die "Не могу открыть /proc: $!"; # работа с каталогом /proc

printf "%-15s %6s %-8s %3s %s\n", "COMMAND", "PID", "USER", "FD", "NAME"; # вывод "шапки"

while (my $pid = readdir($proc)) { # читаем из каталога /proc пиды
    next unless $pid =~ /^\d+$/;              # Только числовые PID
    my $base = "/proc/$pid"; # получаем обрабатываемый каталог пида

    # Имя команды, читаем имя команды (процесса) из каталога /proc/<pid>/comm
    my $comm = ""; #объявляем переменную
    if (open my $c, '<', "$base/comm") { # открываем для чтения каталог comm в выбранном каталоге пида
        chomp($comm = <$c>); # читает первую строку и записывает в переменную
        close $c;
    } else { # если не удалось считать (файл закрылся) идем дальше (next)
        next;
    }

    # Имя пользователя (по uid из /proc/<pid>/status)
    my $user = ""; #объявляем переменную
    if (open my $s, '<', "$base/status") { # читаем строчки из status
        while (<$s>) {
            if (/^Uid:\s+(\d+)/) { # ищем "Uid"
                my $uid = $1; 
                $user = getpwuid($uid) // $uid; # записываем в переменную
                last;
            }
        }
        close $s;
    }

    my $fd_dir = "$base/fd"; 
    next unless -d $fd_dir;

    opendir(my $fdh, $fd_dir) or next; # если каталога fd нет (например, процесс уже завершён), пропускаем
    while (my $fd = readdir($fdh)) {  # перебираем все элементы каталога  — номера файловых дескрипторов
        next if $fd eq '.' or $fd eq '..'; # пропускаем служебные записи
        my $link = readlink("$fd_dir/$fd"); # читаем символическую ссылку, на которую указывает дескриптор
        next unless defined $link; # пропускаем, если не прочиталась
        printf "%-15s %6d %-8s %3s %s\n", $comm, $pid, $user, $fd, $link; # выводим наши переменные (построчно в цикле пока есть)
    }
    closedir($fdh);
}
closedir($proc);


```
```bash
root@ol-apl-ubuntu:/usr/local/bin# ./my_lsof2.pl | { head -n 1; tail -n 20; } # вывод первой (шапки) и последних 20 строк результата работы
COMMAND            PID USER      FD NAME
pickup          386139 postfix    0 /dev/null
pickup          386139 postfix    1 /dev/null
pickup          386139 postfix    2 /dev/null
pickup          386139 postfix    3 pipe:[15403]
pickup          386139 postfix    4 pipe:[15403]
pickup          386139 postfix    5 socket:[15327]
pickup          386139 postfix    6 socket:[15325]
pickup          386139 postfix    7 socket:[1626153]
pickup          386139 postfix    8 anon_inode:[eventpoll]
pickup          386139 postfix    9 pipe:[1626166]
pickup          386139 postfix   10 pipe:[1626166]
perl            387639 root       0 /dev/pts/1
perl            387639 root       1 pipe:[1638256]
perl            387639 root       2 /dev/pts/1
perl            387639 root       3 /proc
perl            387639 root       4 /proc/387639/fd
bash            387640 root       0 pipe:[1638256]
bash            387640 root       1 /dev/pts/1
bash            387640 root       2 /dev/pts/1
bash            387640 root     255 /dev/pts/1
root@ol-apl-ubuntu:/usr/local/bin#

```
## 15 урок
**Домашнее задание** <ins>"Практика с SELinux"</ins>

**Цель**: работать с SELinux: диагностировать проблемы и модифицировать политики SELinux для корректной работы приложений, если это требуется;

🎯**Задание**
- Запустить nginx на нестандартном порту 3-мя разными способами:
- 1. переключатели setsebool;
- 2. добавление нестандартного порта в имеющийся тип;
- 3. формирование и установка модуля SELinux.


<details>
<summary> = Теория = </summary>
	
🛡️ SELinux — краткое руководство
📘 Что это
- SELinux (Security-Enhanced Linux) — это система мандатного контроля доступа (MAC), встроенная в ядро Linux. Она ограничивает действия процессов даже при наличии у них root-прав.
- SELinux — это второй уровень безопасности, который контролирует, что именно процесс может делать с файлами, портами, сокетами и другими объектами.

⚙️ Основные принципы
- SELinux основывается на политиках безопасности — наборах правил, которые описывают, какой процесс (домен) имеет доступ к какому объекту (контексту).
- Каждый файл и процесс имеет контекст безопасности, например:
- ls -Z /var/www/html
- Результат:
- -rw-r--r--. root root system_u:object_r:httpd_sys_content_t:s0 index.html
- Здесь httpd_sys_content_t — тип безопасности, который разрешён для чтения веб-сервером httpd.

🚦 Режимы работы SELinux
- Режим							Описание
- enforcing						SELinux активно применяет политики и блокирует запрещённые действия
- permissive						Только записывает нарушения в лог (/var/log/audit/audit.log), но не блокирует
- disabled						SELinux полностью отключён
- Проверить текущий режим:
- getenforce
- или
- sestatus

🔧 Временное переключение режима
- sudo setenforce 0   # Перевести в permissive
- sudo setenforce 1   # Вернуть enforcing

🔧 Постоянная настройка режима
- sudo nano /etc/selinux/config
- Измени строку: SELINUX=enforcing
- на одну из: 
- SELINUX=permissive
- SELINUX=disabled

📂 Политики SELinux
Основные типы политик:
- Политика				Назначение
- targeted				Защищает только сетевые сервисы (по умолчанию в CentOS, RHEL, Fedora)
- mls						Многоуровневая система безопасности (Military Level Security)
- minimum					Минимальный набор правил (упрощённая политика)
- Проверить:
- sestatus | grep Policy

🧩 Работа с контекстами
- Посмотреть контексты:
- ls -Z

- Изменить контекст файла:
- sudo chcon -t httpd_sys_content_t /var/www/html/index.html

- Восстановить стандартные контексты (по политике):
- sudo restorecon -Rv /var/www/html

🧠 Типичные примеры
| Ситуация | Решение |
|----------|-----------|
| `Apache не видит файлы в /srv/www` | chcon -R -t httpd_sys_content_t /srv/www |
| `nginx не может слушать нестандартный порт` | semanage port -a -t http_port_t -p tcp 8080 |
| `Приложение не может записать лог` | проверить audit.log → скорректировать контекст chcon -t var_log_t |

🔍 Логи SELinux
- Проверить нарушения:
- sudo cat /var/log/audit/audit.log | grep denied
- Упрощённый просмотр:
- sudo ausearch -m avc
- Автоматическое предложение решения:
- Утилита sealert — часть пакета setroubleshoot, который помогает понять, почему SELinux блокирует действие.

🧠 Взаимодействие с Docker / Kubernetes
	•	Контейнеры работают с типом container_t.
	•	Можно разрешить доступ к файлам, пометив их типом container_file_t.
	•	Иногда при работе с bind mounts нужно использовать флаг :z или :Z:
- docker run -v /data:/data:Z nginx

💡 Коротко: как жить с SELinux
	1	Не отключай SELinux без причины. Лучше временно включи permissive и разбери логи.
	2	Используй restorecon — часто решает проблему.
	3	Ставь утилиту policycoreutils-python-utils для semanage, restorecon, chcon.

- SELinux — это действительно второй уровень защиты (MAC),
- а первый — это DAC (Discretionary Access Control).

🔹 1. DAC — Дискреционный контроль доступа (по умолчанию)
- Это базовая модель Unix-подобных систем.
- Пример: у каждого файла есть три атрибута доступа:
- Владелец (user)
- Группа (group)
- Остальные (others)
- Права: чтение r, запись w, выполнение x

🔹 2. MAC — Мандатный контроль доступа (второй уровень)
- MAC добавляет поверх DAC систему политик, где решает уже не владелец файла, а глобальные правила безопасности.
- Например:
	•	У веб-сервера httpd может быть полный доступ к /var/www, но SELinux не позволит ему читать /etc/passwd — даже если права DAC это разрешают.
- В модели MAC:
- Процессы и файлы имеют контексты безопасности. Доступ разрешается только если политика явно это позволяет.

⚙️ Как они работают вместе
	1	Сначала проверяется DAC (обычные UNIX-права, ACL).
	2	Если DAC разрешает, то SELinux (MAC) проводит дополнительную проверку по политике.
	3	Если оба разрешают — доступ дан.
- То есть:
- Разрешено = DAC + MAC
- Запрещено = если хотя бы один сказал “нет”

💡 Коротко:
| Уровень | Что делает |
|----------|-----------|
| `DAC` | Классические UNIX-права (chmod, chown, umask, ACL) |
| `MAC` | Политики безопасности ядра (SELinux, AppArmor и т.д.) |
| `RBAC (доп.)` | Role-Based Access Control — роли пользователей (часто внутри MAC) |


</details>

---
## Домашняя работа
- прописываем в конф файл nginx дополнительный порт 4881, так как у нас не готовый стенд
- **[root@AlmaLinux ~]# systemctl start nginx**
- **[root@AlmaLinux ~]# systemctl status nginx**
- **● nginx.service - The nginx HTTP and reverse proxy server
- Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: disabled)
- Active: active (running) since Tue 2025-10-21 14:05:19 MSK; 6min ago
- Process: 11133 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
- Process: 11134 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
- Process: 11135 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
- Main PID: 11136 (nginx)
- Tasks: 2 (limit: 48850)
- Memory: 1.9M
- CPU: 16ms
- CGroup: /system.slice/nginx.service
-  └─11136 "nginx: master process /usr/sbin/nginx"
-  └─11137 "nginx: worker process"

- Oct 21 14:05:19 AlmaLinux systemd[1]: Starting The nginx HTTP and reverse proxy server...
- Oct 21 14:05:19 AlmaLinux nginx[11134]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
- Oct 21 14:05:19 AlmaLinux nginx[11134]: nginx: configuration file /etc/nginx/nginx.conf test is successful
- Oct 21 14:05:19 AlmaLinux systemd[1]: Started The nginx HTTP and reverse proxy server.
- **[root@AlmaLinux ~]# systemctl status firewalld** # проверяем FireWall
- ● firewalld.service - firewalld - dynamic firewall daemon
- Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; preset: enabled)
- Active: **active (running)** since Tue 2025-10-21 13:52:32 MSK; 28min ago # запущен :(
- Docs: man:firewalld(1)
- Main PID: 808 (firewalld)
- Tasks: 2 (limit: 48850)
- Memory: 42.4M
- CPU: 401ms
- CGroup: /system.slice/firewalld.service
- └─808 /usr/bin/python3 -s /usr/sbin/firewalld --nofork --nopid

- Oct 21 13:52:31 AlmaLinux systemd[1]: Starting firewalld - dynamic firewall daemon...
- Oct 21 13:52:32 AlmaLinux systemd[1]: Started firewalld - dynamic firewall daemon.
- **[root@AlmaLinux ~]# systemctl stop firewalld** # гасим FireWall
- **[root@AlmaLinux ~]# systemctl status firewalld** # проверяем
- ○ firewalld.service - firewalld - dynamic firewall daemon
- Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; preset: enabled)
- Active: **inactive (dead)** since Tue 2025-10-21 14:22:14 MSK; 2s ago # потух :)
- Duration: 29min 42.334s
- Docs: man:firewalld(1)
- Process: 808 ExecStart=/usr/sbin/firewalld --nofork --nopid $FIREWALLD_ARGS (code=exited, status=0/SUCCESS)
- Main PID: 808 (code=exited, status=0/SUCCESS)
- CPU: 459ms
- 
- **[root@AlmaLinux ~]# nginx -t** # проверяем конфигурацию nginx
- nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
- nginx: configuration file /etc/nginx/nginx.conf test is successful
- **[root@AlmaLinux ~]# sestatus** # проверяем статус SELinux
- SELinux status:                 enabled
- SELinuxfs mount:                /sys/fs/selinux
- SELinux root directory:         /etc/selinux
- Loaded policy name:             targeted
- Current mode:                   enforcing
- Mode from config file:          enforcing
- Policy MLS status:              enabled
- Policy deny_unknown status:     allowed
- Memory protection checking:     actual (secure)
- Max kernel policy version:      33

- **[root@AlmaLinux ~]# getenforce** # режим работы SELinux
- **Enforcing** # Данный режим означает, что SELinux будет блокировать запрещенную активность.
- 
## 1. Разрешим в SELinux работу nginx на порту TCP 4881 c помощью переключателей setsebool

- **http://10.0.77.182:4881**
- <img width="523" height="99" alt="Screenshot 2025-10-21 at 14 46 13" src="https://github.com/user-attachments/assets/7bb19e61-0fe4-4b91-9bc4-8f0e263c6649" />

- **[root@AlmaLinux ~]# grep 4881 /var/log/audit/audit.log**
- type=AVC msg=audit(**1761217234.568:48**): avc:  denied  { name_bind } for  pid=1004 comm="nginx" src=4881 - - - - scontext=system_u:system_r:httpd_t:s0 tcontext=system_u:object_r:unreserved_port_t:s0 tclass=tcp_socket permissive=0
- **[root@AlmaLinux ~]# grep 1761217234.568:48** /var/log/audit/audit.log | audit2why # Утилита audit2why покажет почему трафик блокируется 
 и перезапустим nginx: setsebool -P nis_enabled on

- type=AVC msg=audit(1761217234.568:48): avc:  denied  { name_bind } for  pid=1004 comm="nginx" src=4881 - scontext=system_u:system_r:httpd_t:s0 tcontext=system_u:object_r:unreserved_port_t:s0 tclass=tcp_socket permissive=0

- Was caused by:
- The boolean nis_enabled was set incorrectly.
- Description:
- Allow nis to enabled

- Allow access by executing:
  ### setsebool -P nis_enabled 1 # нам нужно поменять параметр nis_enabled
- 
- **[root@AlmaLinux ~]# setsebool -P nis_enabled on** # Включим параметр nis_enabled
- **[root@AlmaLinux ~]# systemctl restart nginx** # перезапустим nginx
- **[root@AlmaLinux ~]# systemctl status nginx** # проверим статус
- ● nginx.service - The nginx HTTP and reverse proxy server
- Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: disabled)
- Active: active (running) since Thu 2025-10-23 14:19:31 MSK; 8s ago
	
- **http://10.0.77.182:4881** # проверим, слушает ли nginx порт 4881
- <img width="790" height="312" alt="Screenshot 2025-10-23 at 14 06 59" src="https://github.com/user-attachments/assets/edb7c5f8-57a6-4b3e-bf9e-5666e5034eb7" />
- **[root@AlmaLinux ~]# getsebool -a | grep nis_enabled**
- nis_enabled --> on
- **[root@AlmaLinux ~]# setsebool -P nis_enabled off** # вернем все обратно
- 

## 2. Разрешим в SELinux работу nginx на порту TCP 4881 c помощью добавления нестандартного порта в имеющийся тип:
-
- **[root@AlmaLinux ~]# semanage port -l | grep http**
- http_cache_port_t              tcp      8080, 8118, 8123, 10001-10010
- http_cache_port_t              udp      3130
- http_port_t                    tcp      80, 81, 443, 488, 8008, 8009, 8443, 9000
- pegasus_http_port_t            tcp      5988
- pegasus_https_port_t           tcp      5989

<img width="614" height="172" alt="Screenshot 2025-10-21 at 15 36 58" src="https://github.com/user-attachments/assets/a33953a0-e895-4048-b1b6-aa3eb9904aa0" />

- [root@AlmaLinux ~]# semanage port -a -t http_port_t -p tcp 4881
- [root@AlmaLinux ~]# semanage port -l | grep  http_port_t
- http_port_t                    tcp      **4881**, 80, 81, 443, 488, 8008, 8009, 8443, 9000
- pegasus_http_port_t            tcp      5988
- **[root@AlmaLinux ~]# systemctl restart nginx && systemctl status nginx**
- ● nginx.service - The nginx HTTP and reverse proxy server
- Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: disabled)
- Active: active (running) since Thu 2025-10-23 15:21:47 MSK; 10ms ago

<img width="646" height="459" alt="Screenshot 2025-10-23 at 15 24 34" src="https://github.com/user-attachments/assets/9fcfda94-239f-42f0-b382-af438cbf35b0" />

- **[root@AlmaLinux ~]# semanage port -d -t http_port_t -p tcp 4881**
- **[root@AlmaLinux ~]# semanage port -l | grep http**
- http_cache_port_t              tcp      8080, 8118, 8123, 10001-10010
- http_cache_port_t              udp      3130
- http_port_t                    tcp      80, 81, 443, 488, 8008, 8009, 8443, 9000
- pegasus_http_port_t            tcp      5988
- pegasus_https_port_t           tcp      5989
- **[root@AlmaLinux ~]# systemctl restart nginx && systemctl status nginx**

- <img width="931" height="496" alt="Screenshot 2025-10-23 at 15 26 55" src="https://github.com/user-attachments/assets/77c836b2-3ea6-439d-a4c8-9bc2f0213451" />

## 3. Разрешим в SELinux работу nginx на порту TCP 4881 c помощью формирования и установки модуля SELinux:
- **[root@AlmaLinux ~]# systemctl start nginx**
- Job for nginx.service failed because the control process exited with error code.
- See "systemctl status nginx.service" and "journalctl -xeu nginx.service" for details.
### Nginx не запускается, так как SELinux продолжает его блокировать. 
- **[root@AlmaLinux ~]# grep nginx /var/log/audit/audit.log** # Посмотрим логи SELinux, которые относятся к Nginx: 
- type=SERVICE_START msg=audit(1761287760.047:221): pid=1 uid=0 auid=4294967295 ses=4294967295 subj=system_u:system_r:init_t:s0 msg='unit=nginx comm="systemd" exe="/usr/lib/systemd/systemd" hostname=? addr=? terminal=? res=failed'UID="root" AUID="unset"
- **[root@AlmaLinux ~]# grep nginx /var/log/audit/audit.log | audit2allow -M nginx** # Воспользуемся утилитой - audit2allow для того, чтобы на основе логов SELinux сделать модуль, разрешающий работу nginx на нестандартном порту
- ******************** IMPORTANT ***********************
- To make this policy package active, execute:

- semodule -i nginx.pp # и как его применить, чтобы разрешить нестандартный порт
- **[root@AlmaLinux ~]# semodule -i nginx.pp** # применяем
- **[root@AlmaLinux ~]# systemctl start nginx** # запускаем nginx
- **[root@AlmaLinux ~]# systemctl status nginx** # проверяем
- ● nginx.service - The nginx HTTP and reverse proxy server
- Loaded: loaded (/usr/lib/systemd/system/nginx.service; **enabled**; **preset: disabled**)
- Active: **active** (running) since Fri 2025-10-24 10:06:41 MSK; 40s ago
  ### http://10.0.77.182:4881 доступна:

- <img width="579" height="270" alt="Screenshot 2025-10-24 at 10 09 45" src="https://github.com/user-attachments/assets/2acb963f-0568-4d1a-815f-55db2d831767" />

- **[root@AlmaLinux ~]# semodule -l** # просмотр всех установленных модулей
- **[root@AlmaLinux ~]# semodule -r nginx** # удаление установленного модуля nginx
- libsemanage.semanage_direct_remove_key: Removing last nginx module (no other nginx module exists at another priority).

- <img width="594" height="119" alt="Screenshot 2025-10-24 at 10 16 56" src="https://github.com/user-attachments/assets/00213e67-0c25-406b-ba88-7059db7a4f6f" />



## 16 урок
**Домашнее задание** <ins>"Первые шаги с Ansible"</ins>

-  Цель: написать первые скрипты с Ansible;

🎯**Задание**
- На  сервере, используя Ansible, необходимо развернуть nginx со следующими условиями:

- необходимо использовать модуль yum/apt;
- конфигурационные файлы должны быть взяты из шаблона jinja2 с переменными;
- после установки nginx должен быть в режиме enabled в systemd;
- должен быть использован notify для старта nginx после установки;
- сайт должен слушать на нестандартном порту — 8080, для этого использовать переменные в Ansible.

  
<details>
<summary> = Теория = </summary>
# 🧠 Ansible — Теория и основы автоматизации

> Ansible — это инструмент автоматизации для управления конфигурациями, развертывания и оркестрации систем без необходимости установки агентов на управляемых узлах.

---

## 📦 Основные концепции

| Термин | Описание |
|--------|-----------|
| **Control Node** | Сервер, где установлен Ansible и откуда выполняются playbooks |
| **Managed Nodes** | Целевые сервера, которыми управляет Ansible |
| **Inventory** | Файл со списком управляемых хостов |
| **Playbook** | YAML-файл, описывающий сценарий автоматизации |
| **Task** | Конкретное действие в playbook (например, установка пакета) |
| **Module** | Исполняемый блок кода, выполняющий конкретную задачу (например, `yum`, `copy`, `template`) |
| **Role** | Логическая структура для организации задач, шаблонов и переменных |
| **Facts** | Системная информация, собираемая Ansible с управляемых узлов |
| **Handler** | Задачи, запускаемые по событию (например, перезапуск службы после изменения конфигурации) |

---

## ⚙️ Установка Ansible

```bash
# AlmaLinux / Oracle / CentOS
sudo dnf install epel-release -y
sudo dnf install ansible -y
- Проверка версии
- ansible --version
```
## Installing Ansible on Ubuntu

- Ubuntu provides Ansible packages through a Personal Package Archive (PPA) that contains more recent versions than the standard repositories.

- Ubuntu builds are available in a PPA here.

- Configure the PPA on your system and install Ansible:

- $ sudo apt update
- $ sudo apt install software-properties-common
- $ sudo add-apt-repository --yes --update ppa:ansible/ansible
- $ sudo apt install ansible


📁 Структура проекта Ansible
Пример типовой структуры:
```bash
project/
├── ansible.cfg
├── inventory
│   ├── hosts.ini
├── playbooks/
│   ├── site.yml
│   └── webservers.yml
└── roles/
    ├── nginx/
    │   ├── tasks/
    │   │   └── main.yml
    │   ├── templates/
    │   │   └── nginx.conf.j2
    │   └── vars/
    │       └── main.yml
```
🧾 Файл inventory
- Inventory — это список хостов, на которые Ansible будет применять задачи.
- Пример (inventory/hosts.ini):

- [webservers]
- 192.168.1.10
- 192.168.1.11

- [dbservers]
- db1.example.com ansible_user=root

- Проверка соединения:
- ansible all -i inventory/hosts.ini -m ping

🧩 Пример Playbook (site.yml)
---
```bash
- name: Установка и запуск Nginx
  hosts: webservers
  become: yes
  tasks:
    - name: Установить пакет nginx
      yum:
        name: nginx
        state: present

    - name: Включить и запустить службу nginx
      service:
        name: nginx
        state: started
        enabled: yes
```
- Запуск:
- ansible-playbook -i inventory/hosts.ini playbooks/site.yml

🧱 Переменные (Variables)
- Переменные можно определять в разных местах:
```bash
Место								Приоритет											Пример
В playbook							низкий												vars:
В group_vars/						средний												group_vars/webservers.yml
В host_vars/						высокий												host_vars/db1.yml
Через командную строку				самый высокий										-e var=value
```
- Пример использования:
```bash
vars:
  nginx_port: 8080

tasks:
  - name: Изменить конфигурацию nginx
    template:
      src: nginx.conf.j2
      dest: /etc/nginx/nginx.conf
```
🧰 Модули Ansible
```bash
Категория			Пример модуля								Назначение
Система				user, group, hostname						Управление пользователями и хостами
Файлы				copy, template, file, unarchive				Работа с файлами
Сеть				firewalld, iptables, nmcli					Настройка сети
Пакеты				yum, apt, dnf								Управление пакетами
Сервисы				service, systemd							Управление службами
Утилиты				command, shell, debug						Выполнение команд
```
🔁 Handlers (Обработчики)
- Используются, чтобы выполнять действие только при изменениях.
```bash
- tasks:
  - name: Копируем конфиг nginx
    template:
      src: nginx.conf.j2
      dest: /etc/nginx/nginx.conf
    notify: restart nginx

handlers:
  - name: restart nginx
    service:
      name: nginx
      state: restarted
```
🧩 Roles (Роли)
- Роли структурируют код Ansible. Пример:
```bash
- roles/
└── nginx/
    ├── tasks/main.yml
    ├── handlers/main.yml
    ├── templates/nginx.conf.j2
    └── vars/main.yml
```
- Использование в site.yml:
```bash
- hosts: webservers
  roles:
    - nginx
```
🔐 Работа с паролями (Ansible Vault)
- Шифрование чувствительных данных:
```bash
ansible-vault create secrets.yml
ansible-vault edit secrets.yml
ansible-vault view secrets.yml
```
- Запуск с паролем:
```bash
ansible-playbook site.yml --ask-vault-pass
```

🧮 Полезные команды
```bash
КомандаНазначение
ansible all -m ping			Проверка доступности всех хостов
ansible-inventory --list	Показать инвентарь
ansible-playbook --check	Проверка без изменений (dry-run)
ansible-config dump			Показать текущие настройки
ansible-doc -l				Список доступных модулей
```
🧠 Принципы работы Ansible
- 1	Без агента — SSH-доступ к хостам.
- 2	Идемпотентность — одно и то же действие не выполняется повторно, если состояние уже достигнуто.
- 3	Язык YAML — декларативное описание конфигурации.
- 4	Расширяемость — через модули и роли.
- 5	Контроль изменений — можно безопасно тестировать через --check.


💬 “Ansible делает сложное простым, а рутинное — автоматическим.”

</details>

---
- **root@ansibleserver:~# ansible --version**
- ansible [core 2.19.3]
-   config file = /etc/ansible/ansible.cfg
-   configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
-   ansible python module location = /usr/lib/python3/dist-packages/ansible
-   ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
-   executable location = /usr/bin/ansible
-   python version = 3.12.3 (main, Aug 14 2025, 17:47:21) [GCC 13.3.0] (/usr/bin/python3)
-   jinja version = 3.1.2
-   pyyaml version = 6.0.1 (with libyaml v0.2.5)

- **root@ansibleserver:~/project/inventory# pwd**
/root/project/inventory
- **root@ansibleserver:~/project/inventory# vi hosts.ini**
```bash
[nginx]
10.0.77.142 ansible_user=spg ansible_ssh_private_key_file=/root/.ssh/id_rsa
```
- **root@ansibleserver:~/project/inventory# ssh-keygen -t rsa -b 4096 -C "ansible@ansibleserver"**
- Generating public/private rsa key pair.
- **root@ansibleserver:~/project/inventory# ls -l /root/.ssh/id_rsa***
- -rw------- 1 root root 3389 Oct 27 13:09 /root/.ssh/id_rsa
- -rw-r--r-- 1 root root  747 Oct 27 13:09 /root/.ssh/id_rsa.pub
- **root@ansibleserver:~/project/inventory# ssh-copy-id -i /root/.ssh/id_rsa.pub spg@10.0.77.142**
- **root@ansibleserver:~/project/inventory# ansible  nginx -i /root/project/inventory/hosts.ini -m ping**
- ***[WARNING]: Host '10.0.77.142' is using the discovered Python interpreter at '/usr/bin/python3.12', but - future installation of another Python interpreter could cause a different interpreter to be discovered. - See https://docs.ansible.com/ansible-core/2.19/reference_appendices/interpreter_discovery.html for more - information.***
 ```bash
  10.0.77.142 | SUCCESS => {
    "ansible_facts": {
         "discovered_interpreter_python": "/usr/bin/python3.12"
     },
     "changed": false,
    "ping": "pong"
}
```

- **root@ansibleserver:~/project# vi ansible.cfg**
```bash
[defaults]
inventory = inventory/hosts.ini
remote_user = spg
host_key_checking = False
retry_files_enabled = False
```

- **root@ansibleserver:~/project/inventory# vi hosts.ini**
```bash
[nginx]
10.0.77.142 ansible_port=22 ansible_ssh_private_key_file=/root/.ssh/id_rsa
```
- **root@ansibleserver:~/project# ansible  nginx -i /root/project/inventory/hosts.ini -m ping**
- ***[WARNING]: Host '10.0.77.142' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.19/reference_appendices/interpreter_discovery.html for more information.***
```bash  
10.0.77.142 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.12"
    },
    "changed": false,
    "ping": "pong"
}
```

- **root@ansibleserver:~/project# ansible  nginx -m command -a "uname -r"**
```bash
10.0.77.142 | CHANGED | rc=0 >>
6.8.0-86-generic
```

- **root@ansibleserver:~/project# ansible  nginx -m systemd -a name=firewalld**
```bash
10.0.77.142 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.12"
    },
    "changed": false,
    "name": "firewalld",
    "status": {
        "ActiveEnterTimestampMonotonic": "0",
        "ActiveExitTimestampMonotonic": "0",
        "ActiveState": "inactive",
```

- ****
```bash

```
