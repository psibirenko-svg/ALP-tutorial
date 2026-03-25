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
- **root@ansibleserver:~/project# vi nginx.ym** # начинаем писать плейбук для установки NGINX
```bash
---
- name: NGINX | Install and configure NGINX
  hosts: nginx
  # become: true # мне не нужно, так как использую ключи (10.0.77.142 ansible_user=spg ansible_ssh_private_key_file=/root/.ssh/id_rsa)
 
  tasks:
    - name: update
      apt:
        update_cache=yes

    - name: NGINX | Install NGINX
      apt:
        name : nginx
        state: latest
```
- ***root@ansibleserver:~/project# ansible-playbook nginx.yml**
```bash
PLAY [NGINX | Install and configure NGINX] ******************************************************

TASK [Gathering Facts] **************************************************************************
[WARNING]: Host '10.0.77.142' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.19/reference_appendices/interpreter_discovery.html for more information.
ok: [10.0.77.142]

TASK [update] ***********************************************************************************
[ERROR]: Task failed: Module failed: Failed to lock apt for exclusive operation: Failed to lock directory /var/lib/apt/lists/: E:Could not open lock file /var/lib/apt/lists/lock - open (13: Permission denied)
Origin: /root/project/nginx.yml:7:7

5
6   tasks:
7     - name: update
        ^ column 7

fatal: [10.0.77.142]: FAILED! => {"changed": false, "msg": "Failed to lock apt for exclusive operation: Failed to lock directory /var/lib/apt/lists/: E:Could not open lock file /var/lib/apt/lists/lock - open (13: Permission denied)"}

PLAY RECAP **************************************************************************************
10.0.77.142                : ok=1    changed=0    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0
ed=0    ignored=0
PLAY: command not found
Command 'Install' not found, did you mean:
  command 'install' from deb coreutils (9.4-3ubuntu6.1)
Try: apt install <deb name>
TASK: command not found
[WARNING]:: command not found
ok:: command not found
TASK: command not found
-bash: syntax error near unexpected token `('
Origin:: command not found
5: command not found
6: command not found
7: command not found
^: command not found
fatal:: command not found
PLAY: command not found
10.0.77.142: command not found
```
## Что-то не работает ДЗ...
- **root@ansibleserver:~/project# cat inventory/hosts.ini** # пробуем прописать пользователя на машину @ansibleclient
```bash
[nginx]
10.0.77.142 ansible_user=spg ansible_port=22 ansible_ssh_private_key_file=/root/.ssh/id_rsa
```
- **root@ansibleserver:~/project# ansible-playbook nginx.yml**
```bash
PLAY [NGINX | Install and configure NGINX] ******************************************************

TASK [Gathering Facts] **************************************************************************
[ERROR]: Task failed: Missing sudo password
fatal: [10.0.77.142]: FAILED! => {"changed": false, "msg": "Task failed: Missing sudo password"}

PLAY RECAP **************************************************************************************
10.0.77.142                : ok=0    changed=0    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0
```
- **root@ansibleserver:~/project# cat inventory/hosts.ini** # пробуем прописать и пароль пользователя на машину @ansibleclient
```bash
[nginx]
10.0.77.142 ansible_user=spg ansible_become_password=******* ansible_port=22 ansible_ssh_private_key_file=/root/.ssh/id_rsa
```
- **root@ansibleserver:~/project# ansible-playbook nginx.yml** 
```bash
PLAY [NGINX | Install and configure NGINX] ******************************************************

TASK [Gathering Facts] **************************************************************************
[WARNING]: Host '10.0.77.142' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.19/reference_appendices/interpreter_discovery.html for more information.
ok: [10.0.77.142]

TASK [update] ***********************************************************************************
changed: [10.0.77.142]

TASK [NGINX | Install NGINX] ********************************************************************
changed: [10.0.77.142]

PLAY RECAP **************************************************************************************
10.0.77.142                : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
## Работает
- **root@ansibleserver:~/project# cat nginx.yml** # в результате
```bash
---
- name: NGINX | Install and configure NGINX
  hosts: nginx
  become: true
  vars:
    nginx_listen_port: 8080

  tasks:
    - name: update
      apt:
        update_cache=yes
      tags:
        - update apt

    - name: NGINX | Install NGINX
      apt:
        name : nginx
        state: latest
      notify:
        - restart nginx
      tags:
        - nginx-package

    - name: NGINX | Create NGINX config file from template
      template:
        src: templates/nginx.config.j2
        dest: /etc/nginx/nginx.conf
      notify:
        - restart nginx
      tags:
        - nginx-configuration

  handlers:
    - name: restart nginx
      systemd:
        name: nginx
        state: restarted
        enabled: yes

    - name: reload nginx
      systemd:
        name: nginx
        state: reloaded
  ```
- **root@ansibleserver:~/project# cat templates/nginx.config.j2** # шаблон (template:)
```bash
# {{ ansible_managed }}
events {
    worker_connections 1024;
}

http {
    server {
        listen       {{ nginx_listen_port }} default_server;
        server_name  default_server;
        root         /usr/share/nginx/html;

        location / {
        }
    }
}
```
- **root@ansibleserver:~/project# ansible-playbook nginx.yml** # Запускаем получившийся файл nginx.yml. 
```bash
PLAY [NGINX | Install and configure NGINX] ******************************************************

TASK [Gathering Facts] **************************************************************************
[WARNING]: Host '10.0.77.142' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.19/reference_appendices/interpreter_discovery.html for more information.
ok: [10.0.77.142]

TASK [update] ***********************************************************************************
changed: [10.0.77.142]

TASK [NGINX | Install NGINX] ********************************************************************
ok: [10.0.77.142]

TASK [NGINX | Create NGINX config file from template] *******************************************
changed: [10.0.77.142]

RUNNING HANDLER [restart nginx] *****************************************************************
changed: [10.0.77.142]

PLAY RECAP **************************************************************************************
10.0.77.142                : ok=5    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
- **root@ansibleserver:~/project# curl http://10.0.77.142:8080** # ПРОВЕРЯЕМ
```bash 
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
## установлен, работает, слушает порт 8080



---
## 18 урок VAGRANT!
**Домашнее задание** <ins>"Расширенная настройка дисков и сетей"</ins>

-  Цель: научиться добавлять диски и настраивать сетевые соединения;

🎯**Задание**
- 1. Подготовка окружения:

- Убедитесть, что установле VirtualBox и Vagrant.
- Создайте директорию для проекта.
- 2. Создать базовую виртуальную машину:
- Использовать можно любой образ.
- Настроите память ВМ: 1024 МБ.
- 3. Добавление дисков:
- Добавьте пару виртуальных диска размером 1 ГБ каждый.
- 4. Настройка сети:
- Настройте проброс 80 порта с гостевой системы на порт 8080 хостовой системы.
- 5. ## Провижининг:

## Напишите провижининг, который:
- Форматирует добавленные диски в файловую систему ext4.
- Создает точки монтирования /mnt/disk1 и /mnt/disk2.
- Монтирует диски в указанные директории.
- Добавляет записи в /etc/fstab для автоматического монтирования при загрузке.

## Результаты на MacOS M4 (Apple Silicon :)

- **spg@spg-mac ~ % which vagrant**
- /usr/local/bin/vagrant

- **spg@spg-mac ~ % which virtualbox**
- /usr/local/bin/virtualbox

- **spg@spg-mac ~ % which vagrant **  
- /usr/local/bin/vagrant

- **spg@spg-mac ~ % vagrant -v**
- Vagrant 2.4.9

- **spg@spg-mac ~ % virtualbox -h**
- Oracle VirtualBox Manager v7.2.0
- Copyright (C) 2005-2025 Oracle and/or its affiliates

- **pg@spg-mac ~ % VBoxManage --version**         
- 7.2.0r170228

- **spg@spg-mac ~ % vagrant box list**
- There are no installed boxes! Use `vagrant box add` to add some.

- **spg@spg-mac ~ % ls -hal Downloads/focal-server-cloudimg-amd64-vagrant.box**
- -rwx------  1 spg  staff   587M Nov  1 09:52 Downloads/focal-server-cloudimg-amd64-vagrant.box

spg@spg-mac ~ % vagrant box add Downloads/focal-server-cloudimg-amd64-vagrant.box --name ubuntu/test
==> box: Box file was not detected as metadata. Adding it directly...
==> box: Adding box 'ubuntu/test' (v0) for provider: (arm64)
    box: Unpacking necessary files from: file:///Users/spg/Downloads/focal-server-cloudimg-amd64-vagrant.box
==> box: Successfully added box 'ubuntu/test' (v0) for '(arm64)'!
----
##  Вывод после недели попыток выполнить ДЗ на маке с М4:
- VirtualBox - не работает;
- Lima - забросили поддержку;
- Qemu - нет box-ов под arm64;
- Parallels Desktop - только платные, 14 -дневного триала уже нет;
- VMware Fusion - Vagrant Plugin: vagrant-vmware-desktop - платный;
- Rosetta2 - не хватает времени попробовать...
  
 
## ДЗ под Windows c VirtualBox

- **PS C:\Users\spg> vagrant -v**
- Vagrant 2.4.9
- **PS C:\Users\spg\.VirtualBox> cat selectorwindow.log**
- 00:00:00.427401 VirtualBox GUI VM Selector Window 7.2.4 r170995 win.amd64 (Oct 17 2025 12:31:09) release log
- 00:00:00.427405 Log opened 2025-11-10T06:55:22.896040200Z
- 00:00:00.427406 Build Type: release
- 00:00:00.427407 OS Product: Windows 10
- 00:00:00.427527 OS Release: 10.0.19045.3693
- 00:00:00.427528 OS Service Pack:
- 00:00:00.449061 DMI Product Name: MS-7673
- 00:00:00.454285 DMI Product Version: 1.0
- 00:00:00.454302 Firmware type: BIOS
- 00:00:00.454311 Host RAM: 8162MB (7.9GB) total, 4642MB (4.5GB) available
- 00:00:00.454318 Executable: C:\Program Files\Oracle\VirtualBox\VirtualBox.exe
- 00:00:00.454319 Process ID: 11888
- 00:00:00.454319 Package type: WINDOWS_64BITS_GENERIC
- 00:00:00.454320 Windows Features:
- 00:00:00.454321   Core Isolation (Memory Integrity): Not supported
- 00:00:00.466500 Qt version: 6.8.0
- 00:00:00.468161 GUI: UIMediumEnumerator: Initial medium-enumeration finished!
- 00:00:00.545723 GUI: UIMediumEnumerator: Medium-enumeration started...
- 00:00:02.852674 GUI: UIMediumEnumerator: Medium-enumeration finished!
- **PS C:\Users\spg\.VirtualBox> cd ../**
- **PS C:\Users\spg> mkdir Vagrant_win**
- Каталог: C:\Users\spg
```bash
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        10.11.2025     10:12                Vagrant_win
```
- **PS C:\Users\spg> mkdir C:\vagrant\ubuntu**

- **PS C:\Users\spg> cd C:\vagrant\ubuntu**

- **PS C:\vagrant\ubuntu> vagrant up**
```bash
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'ubuntu/jammy64'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'ubuntu/jammy64' version '20241002.0.0' is up to date...
==> default: Setting the name of the VM: ubuntu-with-disks
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
Timed out while waiting for the machine to boot. This means that
Vagrant was unable to communicate with the guest machine within
the configured ("config.vm.boot_timeout" value) time period.

If you look above, you should be able to see the error(s) that
Vagrant had when attempting to connect to the machine. These errors
are usually good hints as to what may be wrong.

If you're using a custom box, make sure that networking is properly
working and you're able to connect to the machine. It is a common
problem that networking isn't setup properly in these boxes.
Verify that authentication configurations are also setup properly,
as well.

If the box appears to be booting properly, you may want to increase
the timeout ("config.vm.boot_timeout") value.
```
 ## Перешел на новую машину под ОС Windows (ресурсоемкое ДЗ)
 PS C:\Users\spg> vboxmanage --version
7.2.4r170995
PS C:\Users\spg> vagrant -v
Vagrant 2.4.9
PS C:\Users\spg> cd C:\vagrant\
PS C:\vagrant> ls
```bash

    Каталог: C:\vagrant


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        10.11.2025     15:45                ubuntu

```
PS C:\vagrant> cd .\ubuntu\
PS C:\vagrant\ubuntu> ls
```bash

    Каталог: C:\vagrant\ubuntu


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        10.11.2025     15:45                .vagrant
d-----        10.11.2025     15:45                boxes
-a----        10.11.2025     12:41            387 Vagrantfile
-a----        10.11.2025     10:55           1142 Vagrantfile22
-a----        10.11.2025     11:22           2480 Vagrantfile_main

```
PS C:\vagrant\ubuntu> vagrant box list
There are no installed boxes! Use `vagrant box add` to add some.
PS C:\vagrant\ubuntu> vagrant box add ubuntu/jammy64 "C:\vagrant\ubuntu\boxes\jammy-server-cloudimg-amd64-vagrant.box" --provider virtualbox
```bash
==> box: Box file was not detected as metadata. Adding it directly...
==> box: Adding box 'ubuntu/jammy64' (v0) for provider: virtualbox (i386)
    box: Unpacking necessary files from: file:///C:/vagrant/ubuntu/boxes/jammy-server-cloudimg-amd64-vagrant.box
    box:
==> box: Successfully added box 'ubuntu/jammy64' (v0) for 'virtualbox (i386)'!
```
## Создаем ВМ
PS C:\vagrant\ubuntu> vagrant up
```bash
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'ubuntu/jammy64'...
==> default: Matching MAC address for NAT networking...
==> default: Setting the name of the VM: ubuntu-with-disks
Vagrant is currently configured to create VirtualBox synced folders with
the `SharedFoldersEnableSymlinksCreate` option enabled. If the Vagrant
guest is not trusted, you may want to disable this option. For more
information on this option, please refer to the VirtualBox manual:

  https://www.virtualbox.org/manual/ch04.html#sharedfolders

This option can be disabled globally with an environment variable:

  VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

or on a per folder basis within the Vagrantfile:

  config.vm.synced_folder '/host/path', '/guest/path', SharedFoldersEnableSymlinksCreate: false
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
    default: The guest additions on this VM do not match the installed version of
    default: VirtualBox! In most cases this is fine, but in rare cases it can
    default: prevent things such as shared folders from working properly. If you see
    default: shared folder errors, please make sure the guest additions within the
    default: virtual machine match the version of VirtualBox you have installed on
    default: your host and reload your VM.
    default:
    default: Guest Additions Version: 6.0.0 r127566
    default: VirtualBox Version: 7.2
==> default: Setting hostname...
==> default: Mounting shared folders...
    default: C:/vagrant/ubuntu => /vagrant
```
- **PS C:\vagrant\ubuntu> cat .\Vagrantfile**
```bash

Vagrant.configure("2") do |config|
  # Базовый образ
  config.vm.box = "ubuntu/jammy64"        # образ виртуальной машины Ubuntu 22.04
  # Имя и базовые ресурсы ВМ
  config.vm.hostname = "ubuntu-test"
  config.vm.provider "virtualbox" do |vb|
    vb.name = "ubuntu-with-disks"
    vb.memory = 1024
    vb.cpus = 2
  end

  # Вместо NAT включаем мост (bridge)
  config.vm.network "public_network"
  # Меняем SSH-порт гостевой системы (на 2222)
  # Обычно Vagrant сам пробрасывает 22 -> 2222, но можно указать явно:
  config.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh"

  # Проброс HTTP — порт 80 гостя на 8080 хоста
  config.vm.network "forwarded_port", guest: 80, host: 8080, id: "http"

  # Дополнительно можно увеличить таймаут загрузки
  config.vm.boot_timeout = 600
end

```
- **PS C:\vagrant\ubuntu> vagrant destroy -f**
- ==> default: Destroying VM and associated drives...
- **PS C:\vagrant\ubuntu> vagrant up**

```bash
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'ubuntu/jammy64'...
==> default: Matching MAC address for NAT networking...
==> default: Setting the name of the VM: ubuntu-with-disks
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
    default: Adapter 2: bridged
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
    default: 80 (guest) => 8080 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
    default: The guest additions on this VM do not match the installed version of
    default: VirtualBox! In most cases this is fine, but in rare cases it can
    default: prevent things such as shared folders from working properly. If you see
    default: shared folder errors, please make sure the guest additions within the
    default: virtual machine match the version of VirtualBox you have installed on
    default: your host and reload your VM.
    default:
    default: Guest Additions Version: 6.0.0 r127566
    default: VirtualBox Version: 7.2
==> default: Setting hostname...
==> default: Configuring and enabling network interfaces...
==> default: Mounting shared folders...
    default: C:/vagrant/ubuntu => /vagrant

```
- **PS C:\vagrant\ubuntu> vagrant port**

```bash
The forwarded ports for the machine are listed below. Please note that
these values may differ from values configured in the Vagrantfile if the
provider supports automatic port collision detection and resolution.

    80 (guest) => 8080 (host)
    22 (guest) => 2222 (host)


```
- **PS C:\vagrant\ubuntu> vagrant ssh-config**
```bash
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile C:/vagrant/ubuntu/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
  PubkeyAcceptedKeyTypes +ssh-rsa
  HostKeyAlgorithms +ssh-rsa
```

- **PS C:\vagrant\ubuntu> ssh -p 2222 -i .vagrant\machines\default\virtualbox\private_key vagrant@127.0.0.1**
```bash
The authenticity of host '[127.0.0.1]:2222 ([127.0.0.1]:2222)' can't be established.
ED25519 key fingerprint is SHA256:7KZXz2N4uxRwSzGkXd6B01otNEVIDWBw7fOw3NaKrZs.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
...
```

- **vagrant@ubuntu-test:~$ uname -a**
- Linux ubuntu-test 5.15.0-161-generic #171-Ubuntu SMP Sat Oct 11 08:17:01 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux

- **PS C:\vagrant\ubuntu> netstat -ano | findstr "2222"**
- TCP    0.0.0.0:2222           0.0.0.0:0              LISTENING       8072 # VirtualBox действительно слушает порт и перенаправляет его в гостевую ОС
- **PS C:\vagrant\ubuntu> netstat -ano | findstr "8080"**
- TCP    0.0.0.0:8080           0.0.0.0:0              LISTENING       8072 # VirtualBox действительно слушает порт и перенаправляет его в гостевую ОС
- TCP    10.0.77.141:50581      10.0.1.191:8080        CLOSE_WAIT      7940

## Vagrantfile
```bash
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

#  config.vm.provider :virtualbox

  config.vm.provider :virtualbox do |vb|
    vb.name = "ubuntu-jammy-vm"   # Задаем имя виртуальной машины
    vb.memory = 1024              # Устанавливаем 1024 MB оперативной памяти
    vb.cpus = 2                   # Устанавливаем 2 процессора (ядра)
  end


  config.vm.disk :disk, size: "1GB", name: "extra_storage1"
  config.vm.disk :disk, size: "1GB", name: "extra_storage2"

  config.vm.network "private_network", ip: "10.0.77.161"
  config.vm.network "forwarded_port", guest: 80, host: 8080, id: "http"

# --- Provisioning: разметка и монтирование дисков ---
  config.vm.provision "shell", inline: <<-SHELL
    # Обновляем список дисков
    DISKS=("sdb" "sdc")
    MOUNTPOINTS=("/mnt/disk1" "/mnt/disk2")

    for i in ${!DISKS[@]}; do
      DISK=/dev/${DISKS[$i]}
      MOUNT=${MOUNTPOINTS[$i]}

      # Разметка, если диск не размечен
      if ! blkid $DISK; then
        echo "Creating partition on $DISK"
        echo -e "o\nn\np\n1\n\n\nw" | fdisk $DISK
        partprobe $DISK
      fi

      # Форматирование, если нет файловой системы
      if ! blkid ${DISK}1; then
        echo "Formatting ${DISK}1 as ext4"
        mkfs.ext4 ${DISK}1
      fi

      # Создаем точку монтирования
      mkdir -p $MOUNT

      # Монтируем и добавляем в /etc/fstab
      UUID=$(blkid -s UUID -o value ${DISK}1)
      grep -q $UUID /etc/fstab || echo "UUID=$UUID $MOUNT ext4 defaults 0 2" >> /etc/fstab
      mount $MOUNT
    done

 # Обновляем список пакетов
    sudo apt-get update

    # Устанавливаем Nginx
    sudo apt-get install -y nginx

    # Запускаем Nginx
    sudo systemctl start nginx

    # Включаем Nginx на старте системы
    sudo systemctl enable nginx

    # Проверяем статус сервиса Nginx
    sudo systemctl status nginx

  SHELL
end
```
- **Контрольные выводы работы скрипта:**


<img width="1409" height="791" alt="Screenshot 2025-11-12 at 14 36 03" src="https://github.com/user-attachments/assets/f3baa5a1-15ca-4e6f-8a3e-c3beb6591760" />


- **vagrant@ubuntu-jammy:~$ ss -tulnp | grep 80**
```bash
tcp   LISTEN 0      511             0.0.0.0:80        0.0.0.0:*
tcp   LISTEN 0      511                [::]:80           [::]:*
```
- **vagrant@ubuntu-jammy:~$ lsblk**
```bash
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0 63.8M  1 loop /snap/core20/2669
loop1    7:1    0 91.4M  1 loop /snap/lxd/35819
loop2    7:2    0 50.9M  1 loop /snap/snapd/25577
sda      8:0    0   40G  0 disk
└─sda1   8:1    0   40G  0 part /
sdb      8:16   0   10M  0 disk
sdc      8:32   0    1G  0 disk
└─sdc1   8:33   0 1023M  0 part
sdd      8:48   0    1G  0 disk
```
- **vagrant@ubuntu-jammy:~$ df -h /mnt/***
```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        39G  1.8G   37G   5% /
/dev/sda1        39G  1.8G   37G   5% /
```
- **vagrant@ubuntu-jammy:~$ ip a**
```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 02:53:41:1d:bc:3a brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 metric 100 brd 10.0.2.255 scope global dynamic enp0s3
       valid_lft 83826sec preferred_lft 83826sec
    inet6 fd17:625c:f037:2:53:41ff:fe1d:bc3a/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 86338sec preferred_lft 14338sec
    inet6 fe80::53:41ff:fe1d:bc3a/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8b:72:a9 brd ff:ff:ff:ff:ff:ff
    inet 10.0.77.161/24 brd 10.0.77.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe8b:72a9/64 scope link
       valid_lft forever preferred_lft forever
 ``` 
## 19 урок DOCKER
**Домашнее задание** <ins>"Практика с DOCKER"</ins>

**Цель**: освоить базовые принципы работы с Docker, научиться создавать, настраивать и управлять контейнерами;

🎯**Задание**
- Установите Docker на хост машину https://docs.docker.com/engine/install/ubuntu/
- Установите Docker Compose - как плагин, или как отдельное приложение
- Создайте свой кастомный образ nginx на базе alpine. После запуска nginx должен отдавать кастомную страницу (достаточно изменить дефолтную страницу nginx)
- Определите разницу между контейнером и образом
- Вывод опишите в домашнем задании.
- Ответьте на вопрос: Можно ли в контейнере собрать ядро?


<details>
<summary> = Теория = </summary>
🧱 1. Что такое Docker
	
```bash	
Docker — это платформа для упаковки, доставки и запуска приложений в контейнерах.
Контейнер — это изолированная среда, где приложение работает вместе со всеми зависимостями
 (библиотеками, конфигами и т.д.), но при этом использует ядро операционной системы хоста.
👉 Проще говоря:
Docker позволяет запускать приложения «в коробке», одинаково на любой машине.
```
	
⚙️ 2. Почему Docker появился
```bash
До контейнеров разработчики страдали от классического:
“У меня работает, а у тебя — нет.”
Причины:
	•	Разные версии библиотек.
	•	Разные настройки ОС.
	•	Разные окружения (dev/test/prod).
Docker решает это, упаковывая приложение и всё, что ему нужно, в один образ (image),
который можно запустить в любом месте.
```
	
📦 3. Основные понятия Docker
```bash
Понятие							Описание		
Image (образ)					Шаблон (слепок) приложения. Из него создаются контейнеры.
Container (контейнер)			Запущенный экземпляр образа. Можно запускать, останавливать, удалять.
Dockerfile						Скрипт, описывающий, как собрать образ.
Docker Hub / Registry			Репозиторий для хранения и распространения образов.
Volume (том)					Место на хосте для сохранения данных контейнера.
Network (сеть)					Механизм связи между контейнерами и внешним миром.
```

🧩 4. Как работает Docker
```bash
Docker использует технологии ядра Linux:
	•	Namespaces — создают изоляцию (каждый контейнер видит только себя).
	•	cgroups — ограничивают ресурсы (CPU, RAM).
	•	UnionFS / OverlayFS — позволяют собирать образы слоями (экономия места).
Это позволяет запускать десятки контейнеров на одной машине — быстро и без виртуализации полного ядра.
```

🚀 5. Жизненный цикл контейнера

	1	Собираем образ
- docker build -t myapp .
(Docker читает Dockerfile и создаёт image)

	2	Запускаем контейнер

- docker run -d -p 8080:80 myapp
  
	3	Смотрим, что запущено

- docker ps

	4	Останавливаем контейнер

- docker stop <id>

🧰 6. Пример Dockerfile
```bash
FROM ubuntu:22.04
RUN apt-get update && apt-get install -y nginx
COPY ./index.html /var/www/html/
CMD ["nginx", "-g", "daemon off;"]
```
📦 Этот файл создаст образ с Ubuntu, установит Nginx и запустит веб-сервер.

🕸️ 7. Docker Compose
Когда нужно несколько контейнеров (например, веб-приложение + база данных), используют docker-compose.yml.
```bash
version: '3'
services:
  web:
    build: .
    ports:
      - "8080:80"
  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: example
```
🧠 8. Преимущества Docker
- ✅ Универсальность — работает одинаково на всех системах.
- ✅ Быстрая доставка — не надо ставить зависимости. 
- ✅ Изоляция — одно приложение не ломает другое.
- ✅ Лёгкость — контейнеры стартуют за секунды. 
- ✅ Масштабирование — легко разворачивать в облаках и кластерах.

⚠️ 9. Недостатки
- ⚙️ Требует понимания Linux. 
- 🐍 Неполная изоляция (в отличие от виртуальной машины).
- 🧩 Может быть сложно в больших микросервисных системах без оркестрации (например, Kubernetes).


</details>	

## Ответ на вопрос: "Можно ли в контейнере собрать ядро?"
**Из определения контейнера понятно, что "НЕТ": "Контейнер — это изолированная среда, где приложение работает вместе со всеми зависимостями
 (библиотеками, конфигами и т.д.), но при этом использует ядро операционной системы хоста.
👉 Проще говоря: Хостовая машина (ее ядро) является как бы гипервизором для контейнера.**

## Ответ на вопрос: "Определите разницу между контейнером и образом."
📀 Образ (Image) — это шаблон
**(не запущенное приложение, а готовый набор файлов и инструкций, из которого создаются контейнеры.)**

- неизменяемый (immutable)
- состоит из слоёв (layered filesystem)
- хранится в Docker Hub или локальном registry
- сам по себе ничего не запускает
- используется как шаблон для создания контейнеров

📦 Контейнер (Container) — это запущенный экземпляр образа
**(реальное выполнение образа: приложение, процессы, сервисы.)**

- изменяемый (может менять состояние)
- имеет свой файловый слой поверх образа
- можно запускать, останавливать, удалять
- работает изолированно: свои процессы, сеть, ФС

- **root@dockers:~# uname -a**
```bash
PRETTY_NAME="Ubuntu 24.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.3 LTS (Noble Numbat)"
```
```bash
root@dockers:~# apt-get install ca-certificates curl** # устанавливаем curl
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
ca-certificates is already the newest version (20240203).
ca-certificates set to manually installed.
curl is already the newest version (8.5.0-2ubuntu10.6).
curl set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 34 not upgraded.
```
- **добавляем официальный репозиторий Docker**
```bash
root@dockers:~# install -m 0755 -d /etc/apt/keyrings # даем права на папку для скачивания
root@dockers:~# curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc # скачиваем публичный GPG-ключ Docker
root@dockers:~# echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null**
root@dockers:~# apt-get update
 Get:9 https://download.docker.com/linux/ubuntu noble InRelease [48.5 kB]
```  
- **Устанавливаем Docker**
```bash
root@dockers:~# apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
root@dockers:~# systemctl status docker
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: enabled)
     Active: active (running) since Thu 2025-11-27 12:54:50 UTC; 1min 48s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 2540 (dockerd)
      Tasks: 9
     Memory: 25.7M (peak: 26.0M)
        CPU: 247ms
     CGroup: /system.slice/docker.service
             └─2540 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Nov 27 12:54:49 dockers dockerd[2540]: time="2025-11-27T12:54:49.749605663Z" level=info msg="Restoring containers: start."
Nov 27 12:54:49 dockers dockerd[2540]: time="2025-11-27T12:54:49.777785419Z" level=info msg="Deleting nftables IPv4 rules>
Nov 27 12:54:49 dockers dockerd[2540]: time="2025-11-27T12:54:49.781815965Z" level=info msg="Deleting nftables IPv6 rules>
Nov 27 12:54:50 dockers dockerd[2540]: time="2025-11-27T12:54:50.007050378Z" level=info msg="Loading containers: done."
Nov 27 12:54:50 dockers dockerd[2540]: time="2025-11-27T12:54:50.012753459Z" level=info msg="Docker daemon" commit=461269>
Nov 27 12:54:50 dockers dockerd[2540]: time="2025-11-27T12:54:50.012835626Z" level=info msg="Initializing buildkit"
Nov 27 12:54:50 dockers dockerd[2540]: time="2025-11-27T12:54:50.044034511Z" level=info msg="Completed buildkit initializ>
Nov 27 12:54:50 dockers dockerd[2540]: time="2025-11-27T12:54:50.051089113Z" level=info msg="Daemon has completed initial>
Nov 27 12:54:50 dockers dockerd[2540]: time="2025-11-27T12:54:50.051221457Z" level=info msg="API listen on /run/docker.so>
Nov 27 12:54:50 dockers systemd[1]: Started docker.service - Docker Application Container Engine.
```
- **root@dockers:~# docker compose version** # проверяем установлен ли докер compose и какой версии
- Docker Compose version v2.40.3 # все хорошо

- **root@dockers:~/docproject# ls**
Dockerfile  html  nginx.conf
- **root@dockers:~/docproject# vi Dockerfile**
```bash
FROM alpine:3.20

# Устанавливаем nginx
RUN apk add --no-cache nginx

# Создаем директорию для HTML
RUN mkdir -p /var/www/html

# Копируем свои файлы сайта
COPY ./html /var/www/html

# Копируем кастомный конфиг nginx
COPY ./nginx.conf /etc/nginx/nginx.conf

# Открываем порт
EXPOSE 80

# Запускаем nginx в foreground режиме
CMD ["nginx", "-g", "daemon off;"]
```
- **root@dockers:~/docproject# vi nginx.conf**
```bash
user nginx;
worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    sendfile on;
    keepalive_timeout 65;

    server {
        listen 80;
        server_name _;

        root /var/www/html;
        index index.html;

        location / {
            try_files $uri $uri/ =404;
        }
    }
}
```
- **root@dockers:~/docproject/html# vi index.html**
```bash
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Домашнее задание</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background: #f3faff;
            padding-top: 60px;
        }
        h1 {
            color: #0d63af;
            font-size: 48px;
        }
        img {
            width: 300px;
            margin-top: 30px;
        }
    </style>
</head>
<body>
    <h1>Домашнее задание</h1>
    <img src="https://www.docker.com/wp-content/uploads/2022/03/vertical-logo-monochromatic.png" alt="Docker Whale">
</body>
</html>
```

- **root@dockers:~/docproject# docker build -t my-nginx-alpine**
```bash
[+] Building 4.3s (10/10) FINISHED                                                                         docker:default
 => [internal] load build definition from Dockerfile                                                                 0.0s
 => => transferring dockerfile: 505B                                                                                 0.0s
 => [internal] load metadata for docker.io/library/alpine:3.20                                                       1.9s
 => [internal] load .dockerignore                                                                                    0.0s
 => => transferring context: 2B                                                                                      0.0s
 => [1/5] FROM docker.io/library/alpine:3.20@sha256:765942a4039992336de8dd5db680586e1a206607dd06170ff0a37267a9e0195  0.6s
 => => resolve docker.io/library/alpine:3.20@sha256:765942a4039992336de8dd5db680586e1a206607dd06170ff0a37267a9e0195  0.0s
 => => sha256:5311e7f182d02360a7194aa2995849bcdf04795c39a0ffdcf413eae625865970 3.63MB / 3.63MB                       0.5s
 => => extracting sha256:5311e7f182d02360a7194aa2995849bcdf04795c39a0ffdcf413eae625865970                            0.1s
 => [internal] load build context                                                                                    0.0s
 => => transferring context: 559B                                                                                    0.0s
 => [2/5] RUN apk add --no-cache nginx                                                                               1.2s
 => [3/5] RUN mkdir -p /var/www/html                                                                                 0.2s
 => [4/5] COPY ./html /var/www/html                                                                                  0.0s
 => [5/5] COPY ./nginx.conf /etc/nginx/nginx.conf                                                                    0.0s
 => exporting to image                                                                                               0.3s
 => => exporting layers                                                                                              0.2s
 => => exporting manifest sha256:e7016a019e6a1aee4cbfb1cd2ad06bc84067c095ec6df24b6202587c3ed65570                    0.0s
 => => exporting config sha256:62c963faa7e9046c91bd7c8213a6b97593b2ea4aa202b5f0fe13d3e249563e6d                      0.0s
 => => exporting attestation manifest sha256:3e626b399a02b7ce42cf2a9c83aeac582e337842115d058d60f2035e74f5043c        0.0s
 => => exporting manifest list sha256:86f7f8e4dc42f5c5e40c20398a3c99a20ae75b9fda33883f86882f474574a4fc               0.0s
 => => naming to docker.io/library/my-nginx-alpine:latest                                                            0.0s
 => => unpacking to docker.io/library/my-nginx-alpine:latest
```
- **root@dockers:~/docproject# docker run -d -p 8080:80 my-nginx-alpine**
- fbb79b0b9f651d05c95435b82a7641a0d958fd61be5441bc2c7e0b6d7b3b3cc5
- **root@dockers:~/docproject# docker ps**
```bash
CONTAINER ID   IMAGE             COMMAND                  CREATED          STATUS          PORTS                                     NAMES
fbb79b0b9f65   my-nginx-alpine   "nginx -g 'daemon of…"   12 seconds ago   Up 11 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   exciting_lewin
```
- **root@dockers:~/docproject# docker ps -a**
```bash
CONTAINER ID   IMAGE             COMMAND                  CREATED          STATUS                    PORTS                                     NAMES
fbb79b0b9f65   my-nginx-alpine   "nginx -g 'daemon of…"   23 seconds ago   Up 22 seconds             0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   exciting_lewin
9f52d28943c0   hello-world       "/hello"                 23 hours ago     Exited (0) 23 hours ago                                             great_keldysh
```
- **root@dockers:~/docproject# ip a**
```bash
...
2: ens192: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:50:56:b3:87:45 brd ff:ff:ff:ff:ff:ff
    altname enp11s0
    inet 10.0.77.182/24 metric 100 brd 10.0.77.255 scope global dynamic ens192
```
<img width="868" height="590" alt="Screenshot 2025-11-28 at 15 38 08" src="https://github.com/user-attachments/assets/658f719a-1424-420f-9ed6-0ea7638d71d0" />

- **root@dockers:~/docproject# docker tag my-nginx-alpine psibirenko/nginx-demo:latest**
- **root@dockers:~/docproject# docker images**
```bash                                                                                                                                                                                                                    i Info →   U  In Use
IMAGE                          ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest             f7931603f70e       20.3kB         3.96kB    U
my-nginx-alpine:latest         54fd5354770f       14.4MB         4.26MB    U
pavels/nginx-demo:latest       54fd5354770f       14.4MB         4.26MB    U
psibirenko/nginx-demo:latest   54fd5354770f       14.4MB         4.26MB    U
```
- **root@dockers:~/docproject# docker push psibirenko/nginx-demo:latest**
```bash
The push refers to repository [docker.io/psibirenko/nginx-demo]
ef88f82276c6: Pushed
56bbfe682db9: Pushed
68f000e86b74: Pushed
5311e7f182d0: Pushed
012202b96bd6: Pushed
4fa074e02d96: Pushed
latest: digest: sha256:54fd5354770f2fb49d02ea5e3806be2321d470262f67ac69fcba743c71d935ee size: 856
```
## https://hub.docker.com/r/psibirenko/nginx-demo/tags

## 23 урок ZABBIX
**Домашнее задание** <ins>"Настройка мониторинга в zabbix"</ins>

**Цель**: Научиться настраивать дашборд

🎯**Задание**
- Настроить дашборд с 4-мя графиками:
- память;
- процессор;
- диск;
- сеть.

✅ Выполнение.
- **Установка PostgreSQL** # Нужно для установки Zabbix
- **root@zabbixproject:~# systemctl status postgresql**
- Unit postgresql.service could not be found.
- **root@zabbixproject:~# apt update**
- **root@zabbixproject:~# apt install -y wget gnupg lsb-release # Устанавливаем зависимости**
- **root@zabbixproject:~# wget -qO - https://www.postgresql.org/media/keys/ACCC4CF8.asc | tee /etc/apt/trusted.gpg.d/postgresql.gpg > /dev/null** # добавляем официальный репозиторий PostgreSQL
- **root@zabbixproject:~# echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" \
  | sudo tee /etc/apt/sources.list.d/pgdg.list** # добавляем источник
- deb http://apt.postgresql.org/pub/repos/apt noble-pgdg main
- **root@zabbixproject:~# sudo apt install -y postgresql postgresql-contrib** # устанавливаем PostgreSQL
- **root@zabbixproject:~# systemctl status postgresql** # проверяем
```bash
● postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/usr/lib/systemd/system/postgresql.service; enabled; preset: enabled)
     Active: active (exited) since Mon 2025-12-01 07:20:21 UTC; 2min 40s ago
   Main PID: 3818 (code=exited, status=0/SUCCESS)
        CPU: 916us

Dec 01 07:20:21 zabbixproject systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
Dec 01 07:20:21 zabbixproject systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
```
- ## Установка и конфигураци ZABBIX для моей платформы на сервере: Ubuntu 24.04 Noble, Server frontend agent 2, PostgreSQL, Nginx
- ## a. Install Zabbix repository
- **root@zabbixproject:~# wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu24.04_all.deb**
```bash
--2025-12-01 07:36:10--  https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu24.04_all.deb
Resolving repo.zabbix.com (repo.zabbix.com)... 178.128.6.101, 2604:a880:2:d0::2062:d001
Connecting to repo.zabbix.com (repo.zabbix.com)|178.128.6.101|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 8092 (7.9K) [application/octet-stream]
Saving to: ‘zabbix-release_latest_7.0+ubuntu24.04_all.deb’

zabbix-release_latest_7.0+ubu 100%[===============================================>]   7.90K  --.-KB/s    in 0s

2025-12-01 07:36:11 (371 MB/s) - ‘zabbix-release_latest_7.0+ubuntu24.04_all.deb’ saved [8092/8092]
```
- **root@zabbixproject:~# dpkg -i zabbix-release_latest_7.0+ubuntu24.04_all.deb**
```bash
Selecting previously unselected package zabbix-release.
(Reading database ... 152523 files and directories currently installed.)
Preparing to unpack zabbix-release_latest_7.0+ubuntu24.04_all.deb ...
Unpacking zabbix-release (1:7.0-2+ubuntu24.04) ...
Setting up zabbix-release (1:7.0-2+ubuntu24.04) ...
```
- **root@zabbixproject:~# apt update**
- ## b. Install Zabbix server, frontend, agent2
- **root@zabbixproject:~# apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-nginx-conf zabbix-sql-scripts zabbix-agent2**
- ## c. Install Zabbix agent 2 plugins
- **root@zabbixproject:~# apt install zabbix-agent2-plugin-mongodb zabbix-agent2-plugin-mssql zabbix-agent2-plugin-postgresql**
- ## d. Create initial database
- **root@zabbixproject:~# sudo -u postgres createuser --pwprompt zabbix**
- Enter password for new role:
- Enter it again:
- **root@zabbixproject:~# sudo -u postgres createdb -O zabbix zabbix**
- **root@zabbixproject:~# zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix**
- ## f. Start Zabbix server and agent processes
- **root@zabbixproject:~# systemctl restart zabbix-server zabbix-agent2 nginx php8.3-fpm**
- **root@zabbixproject:~# systemctl enable zabbix-server zabbix-agent2 nginx php8.3-fpm**
- **root@zabbixproject:~# ss -tulpn | grep 10050** # слушает порт 10050
- tcp   LISTEN 0      4096                    *:10050            *:*    users:(("zabbix_agent2",pid=868,fd=8))
- **root@zabbixproject:~# vi /etc/zabbix/zabbix_server.conf** правим конфиг сервера:
- ListenPort=10051
- LogFile=/var/log/zabbix/zabbix_server.log
- LogFileSize=0
- DBUser=zabbix
- DBPassword=Zww57df32!
- 
- ## Установка и конфигураци клиента ZABBIX на Linux машине
- **root@ansibleclient:~# wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_7.0-2+ubuntu24.04_all.deb** # скачиваем пакет
- **root@ansibleclient:~# dpkg -i zabbix-release_7.0-2+ubuntu24.04_all.deb**
- **root@ansibleclient:~# apt update**
- **root@ansibleclient:~# apt install -y zabbix-agent2** # устанавливаем самого клиента
- **root@ansibleclient:~# vi /etc/zabbix/zabbix_agent2.conf** # правим конфиг агента:
- PidFile=/run/zabbix/zabbix_agent2.pid
- LogFile=/var/log/zabbix/zabbix_agent2.log
- LogFileSize=0
- Server=10.0.77.182
- ServerActive=10.0.77.182
- Hostname=Zabbix agen142
- PluginSocket=/run/zabbix/agent.plugin.sock
  
- **root@zabbixproject:~# zabbix_get -s 10.0.77.142 -p 10050 -k agent.ping** # проверка с сервера доступности клиента
- 1 # доступен!

## Настраиваем ZABBIX чез WEB: http://10.0.77.182:8080/zabbix.php?action=host.list

<img width="1404" height="804" alt="Screenshot 2025-12-01 at 16 14 23" src="https://github.com/user-attachments/assets/72263caa-a053-4072-bfad-cdaedaeae619" />

<img width="1252" height="708" alt="Screenshot 2025-12-01 at 16 15 15" src="https://github.com/user-attachments/assets/1e79880f-d52b-427a-819e-c1cbc9b1edf5" />

<img width="1435" height="959" alt="Screenshot 2025-12-01 at 16 16 35" src="https://github.com/user-attachments/assets/84463044-55eb-41ea-ae21-674fa63729bd" />

<img width="1455" height="682" alt="Screenshot 2025-12-01 at 16 17 04" src="https://github.com/user-attachments/assets/be314392-6443-49ae-a6a9-f1caf1487bf2" />

<img width="1438" height="961" alt="Screenshot 2025-12-01 at 16 17 57" src="https://github.com/user-attachments/assets/f8f66dba-29c4-4778-a57d-9fbdda775f6b" />

## Дальше можно мониторить проблемы и тенденции, настраивать карты сетей с контролем доступности узлов и пр.


<img width="1477" height="964" alt="Screenshot 2025-12-01 at 16 47 31" src="https://github.com/user-attachments/assets/b549fbbd-9fc2-4cee-949a-3a09e6b12a8e" />


## 24 урок 
## Пользователи и группы. Авторизация и аутентификация 

**Домашнее задание** <ins>"PAM"</ins>

**Цель**: научиться создавать пользователей и добавлять им ограничения;

🎯 Что нужно сделать?

- Ограничить доступ к системе для всех пользователей, кроме группы администраторов, в выходные дни (суббота и воскресенье), за исключением праздничных дней.


⭐️ Задание повышенной сложности

- Предоставить определённому пользователю доступ к Docker и право перезапускать Docker-сервис.

✅ Выполнение.
## Все попытки заставить работать pam_time.so в Ubuntu 24.04 не привели к желаемому результату.
Выводы:
- 🔥 В Ubuntu 24.04 есть БАГ: pam_time.so не срабатывает в sshd
Это зафиксировано в Launchpad и на форумах Ubuntu: Модуль вызывается, но sshd не применяет его корректно.
Появилось в 22.04, остаётся в 24.04. и 24.10 :(
- 🔥 systemd-logind перехватывает авторизацию
и не всегда передаёт PAM ограничения.
Поэтому pam_time.so не может запретить SSH вход, если systemd авторизует сессию до PAM-модуля.
 ## И на понимание этого ушло время... неделя между работой :( Видимо, прослушал на занятии или не догадался, что надо идти по предложенному в методичке пути...
## Рабочий вариант:
- **root@pamproject:~# vipw** # создали двух пользователей mouse и  dog для примера через adduser
- mouse:x:1001:1001:Mikky Mouse,00,01,02,Simple user 1:/home/mouse:/bin/bash
- dog:x:1002:1002:Jerry Dog,55,56,57,Simple user 2:/home/dog:/bin/bash
- **root@pamproject:~# usermod mouse -a -G sudo** # добавим пользователя mouse в группу sudo
- **root@pamproject:~# id mouse** # проверим
- uid=1001(mouse) gid=1001(mouse) groups=1001(mouse),27(sudo),100(users
- **root@pamproject:~# cat /etc/group | grep sudo** # проверим
- sudo:x:27:spg,mouse
- ### СКРИПТ
- **root@pamproject:~# cat /usr/local/bin/check_time2.sh** # скрипт из методички немного изменен
```bash
#!/bin/bash

DAY=$(date +%a)

# Если выходной
if [ "$DAY" = "Sat" ] || [ "$DAY" = "Sun" ]; then
    # Если пользователь входит в sudo — доступ разрешён
    if id -nG "$PAM_USER" | grep -qw "sudo"; then
        exit 0
    else
        exit 1
    fi
else
    # В будни всем разрешено
    exit 0
fi
```
- **root@pamproject:~# sudo chmod +x /usr/local/bin/check_time2.sh** делаем исполняемым
- **root@pamproject:~# vi /etc/pam.d/sshd** # Добавим исполнение скрипта перед @include common-account
```bash
# Standard Un*x authorization.
account required pam_exec.so /usr/local/bin/check_time.sh
@include common-account
```
- **root@pamproject:~# sudo systemctl restart ssh** # перезапустим ssh
- **root@pamproject:~# timedatectl set-ntp false** # отключим NTP
- **root@pamproject:~# timedatectl set-time "2025-12-06"** # поставим субботу в дату
-  **~ ssh spg@10.0.77.182** - Проверим пускают ли группу sudo? Да  
- spg@10.0.77.182's password: 
- Welcome to Ubuntu 24.04.3 LTS (GNU/Linux 6.8.0-88-generic x86_64)
- **~ ssh mouse@10.0.77.182** # Да
- mouse@10.0.77.182's password: 
- Welcome to Ubuntu 24.04.3 LTS (GNU/Linux 6.8.0-88-generic x86_64)
- **~ ssh dog@10.0.77.182** # Нет (dog - не в группе sudo)  
- dog@10.0.77.182's password: 
- /usr/local/bin/check_time2.sh failed: exit code 1
- Connection closed by 10.0.77.182 port 22
- **root@pamproject:~# timedatectl set-ntp true** # возвращаем дату к текущей
- **root@pamproject:~# timedatectl** # проверяем
```bash
               Local time: Wed 2025-12-10 13:47:38 MSK
           Universal time: Wed 2025-12-10 10:47:38 UTC
                 RTC time: Wed 2025-12-10 10:47:38
                Time zone: Europe/Moscow (MSK, +0300)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```
- **~ ssh dog@10.0.77.182** # Да (dog - не в группе sudo, но будни)
- dog@10.0.77.182's password: 
- Welcome to Ubuntu 24.04.3 LTS (GNU/Linux 6.8.0-88-generic x86_64)
- **root@pamproject:~# cat /usr/local/bin/check_time.sh** # скрипт c расписанием, которое можно менять, заменяет предыдущий
```bash
#!/bin/bash
#
# PAM time checker (users + groups + weekdays + time windows)
#
# Формат правил:
#   user_or_group:DAYS:HHMM-HHMM,HHMM-HHMM
#
# user_or_group:
#   - обычный пользователь:  spg
#   - группа:                @sudo
#
# Примеры:
#   @sudo:Mo-Fr:0000-2400
#   dog:Mo-Fr:0900-1800
#

RULES="
@sudo:Mo-Fr:0000-2400
dog:Mo-Fr:0900-1800
"

USER="$PAM_USER"
WEEKDAY=$(date +%a)   # Mo, Tu, We...
TIME=$(date +%H%M)    # HHMM
GROUPS=$(id -nG "$USER")

log() {
    logger "pam_exec_time: $1"
}

is_group_match() {
    local r="$1"

    if [[ "$r" =~ ^@(.*)$ ]]; then
        local grp="${BASH_REMATCH[1]}"
        for g in $GROUPS; do
            if [[ "$g" == "$grp" ]]; then
                return 0
            fi
        done
        return 1
    else
        [[ "$r" == "$USER" ]]
        return $?
    fi
}

match_day() {
    local day=$1
    local pattern=$2

    # простое совпадение дня
    [[ " $pattern " =~ " $day " ]] && return 0

    # диапазон Mo-Fr
    if [[ $pattern =~ ^([A-Za-z]{2})-([A-Za-z]{2})$ ]]; then
        local start=${BASH_REMATCH[1]}
        local end=${BASH_REMATCH[2]}
        local order="Mo Tu We Th Fr Sa Su"

        # индексы
        i_start=$(echo $order | awk -v d="$start" '{for(i=1;i<=NF;i++)if($i==d)print i}')
        i_end=$(echo $order | awk -v d="$end" '{for(i=1;i<=NF;i++)if($i==d)print i}')
        i_day=$(echo $order | awk -v d="$day" '{for(i=1;i<=NF;i++)if($i==d)print i}')

        [[ $i_day -ge $i_start && $i_day -le $i_end ]] && return 0
    fi

    return 1
}

# --- основной цикл правил ---
while IFS= read -r rule; do
    [[ -z "$rule" ]] && continue

    IFS=":" read rule_user rule_days rule_times <<< "$rule"

    # Проверяем пользователя или группу
    if ! is_group_match "$rule_user"; then
        continue
    fi

    # Проверяем дни
    for day_block in $rule_days; do
        if match_day "$WEEKDAY" "$day_block"; then

            # Проверяем интервалы времени
            IFS="," read -ra intervals <<< "$rule_times"
            for intv in "${intervals[@]}"; do
                start=${intv%-*}
                end=${intv#*-}

                if [[ $TIME -ge $start && $TIME -lt $end ]]; then
                    exit 0    # доступ разрешён
                fi
            done
        fi
    done

done <<< "$RULES"

log "доступ ЗАПРЕЩЕН: user=$USER groups=($GROUPS) weekday=$WEEKDAY time=$TIME"
exit 1

```
- **root@pamproject:~# sudo chmod +x /usr/local/bin/check_time.sh** # делаем исполняемым
- **root@pamproject:~# vi /etc/pam.d/sshd** # Добавим исполнение скрипта перед @include common-account
```bash
# Standard Un*x authorization.
account required pam_exec.so /usr/local/bin/check_time.sh
@include common-account
```
- **root@pamproject:~# sudo systemctl restart ssh** # перезапустим ssh
- ## Скрипт тоже рабочий

- ## ДОП. Предоставить определённому пользователю доступ к Docker и право перезапускать Docker-сервис.

- **root@pamproject:~# docker ps** # проверим, что docker установлен для задания
- CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
- **root@pamproject:~# su mouse** # перейдем в оболочку простого пользователя, которого создали заранее
- **mouse@pamproject:/root$ docker ps** # убедимся, что прав на docker у него нет
- **permission denied** while trying to connect to the docker API at unix:///var/run/docker.sock
- **mouse@pamproject:/root$ which docker** # посмотрим, где docker
- /usr/bin/docker
- **mouse@pamproject:/root$ which systemctl** # посмотрим, где systemctl
- /usr/bin/systemctl
- **mouse@pamproject:/root$ exit** # вернемся в root
- exit

- **root@pamproject:~# sudo usermod -aG docker mouse** # добавим пользователя mouse в группу docker
- **root@pamproject:~# su - mouse** # перейдем в оболочку простого пользователя mouse
- **mouse@pamproject:~$ docker ps** # проверим доступ к docker (есть)
- CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
- **mouse@pamproject:~$ id mouse** # проверим членство пользователя mouse в группе к docker (есть)
- uid=1001(mouse) gid=1001(mouse) groups=1001(mouse),100(users),**988(docker)**
- **mouse@pamproject:~$ exit** # первая часть выполнена
- logout
- **root@pamproject:~# visudo -f /etc/sudoers.d/mouse-docker** # создадим индивидуальный файл в sudoers для перезапуска doker из-под пользователя mouse
- mouse ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart docker # с одной строкой разрешающей mouse только перезапускать docker без запроса пароля
- **root@pamproject:~# visudo -c** # проверим конфигурацию sudoers
- /etc/sudoers: parsed OK
- /etc/sudoers.d/README: parsed OK
- /etc/sudoers.d/mouse-docker: bad permissions, should be mode 0440 # нужно подправить права доступа
- **root@pamproject:~# chmod 440 /etc/sudoers.d/mouse-docker** # поправим
- **root@pamproject:~# su - mouse** # перейдем в mouse
- **mouse@pamproject:~$ systemctl restart docker** # проверим права на перезапуск docker (есть)
- **mouse@pamproject:~$**
- **mouse@pamproject:~$ sudo systemctl stop docker** # а на stop, например, прав нет
- [sudo] password for mouse:
- Sorry, user mouse is not allowed to execute '/usr/bin/systemctl stop docker' as root on pamproject.
- ## вторая часть дополнительного задания выполнена

## 26 урок 
## Сбор и анализ логов 

**Домашнее задание** <ins>"Настраиваем центральный сервер для сбора логов"</ins>

**Цель**: научится проектировать централизованный сбор логов;
рассмотреть особенности разных платформ для сбора логов;

🎯 Что нужно сделать?
1. Поднимаем две машины — logclient и logserver.
2. На logclient поднимаем nginx.
3. Настраиваем центральный лог-сервер logserver на любой системе по выбору:
journald;
**rsyslog;**
elk.
4. Настраиваем аудит, который будет отслеживать изменения конфигураций nginx.
5. Все критичные логи с logclient должны собираться и локально и удаленно.
6. Все логи с nginx должны уходить на удаленный сервер logserver (локально только критичные).
7. Логи аудита должны также уходить на удаленную систему.

**Есть две машины с Linux Ubuntu 24.04: logclient и logserver
- **root@logclient:~# systemctl status nginx** # на клиент установлен nginx
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: active (running) since Wed 2025-12-10 12:14:09 UTC; 21s ago
  <img width="1071" height="324" alt="Screenshot 2025-12-10 at 15 30 42" src="https://github.com/user-attachments/assets/5e110db2-5896-4408-b88a-a01e95b9b27c" />

- **oot@pamproject:~# apt list rsyslog -a** # rsyslog должен быть установлен по умолчанию в нашей ОС, проверим это
- Listing... Done
- rsyslog/noble-updates,now 8.2312.0-3ubuntu9.1 amd64 [installed,automatic]
- rsyslog/noble 8.2312.0-3ubuntu9 amd64
- **root@pamproject:~# cat /etc/rsyslog.conf**
```bash
# provides UDP syslog reception
module(load="imudp")
input(type="imudp" port="514")

# provides TCP syslog reception
module(load="imtcp")
input(type="imtcp" port="514")
...
#Add remote logs # в конец файла добавлфем правила приема логов
$template RemoteLogs,"/var/log/rsyslog/%HOSTNAME%/%PROGRAMNAME%.log"
*.* ?RemoteLogs
& ~
```
 
- **root@pamproject:~# ss -tuln**
```bash
Netid     State      Recv-Q     Send-Q              Local Address:Port         Peer Address:Port    Process
udp       UNCONN     0          0                         0.0.0.0:514               0.0.0.0:*
udp       UNCONN     0          0                      127.0.0.54:53                0.0.0.0:*
udp       UNCONN     0          0                   127.0.0.53%lo:53                0.0.0.0:*
udp       UNCONN     0          0              10.0.77.182%ens192:68                0.0.0.0:*
udp       UNCONN     0          0                            [::]:514                  [::]:*
tcp       LISTEN     0          25                        0.0.0.0:514               0.0.0.0:*
tcp       LISTEN     0          4096                      0.0.0.0:22                0.0.0.0:*
tcp       LISTEN     0          4096                127.0.0.53%lo:53                0.0.0.0:*
tcp       LISTEN     0          4096                   127.0.0.54:53                0.0.0.0:*
tcp       LISTEN     0          25                           [::]:514                  [::]:*
tcp       LISTEN     0          4096                         [::]:22                   [::]:*
```
- **root@logclient:~# nginx -v**
- nginx version: nginx/1.24.0 (Ubuntu)
- **root@logclient:~# cat /etc/nginx/nginx.conf** # добавляем строки в конфиг nginx для логирования
- error_log /var/log/nginx/error.log;
- error_log  syslog:server=10.0.77.182:514,tag=nginx_error;
```bash
- ...
- http {
- ...
- access_log /var/log/nginx/access.log;
- access_log syslog:server=10.0.77.182:514,tag=nginx_access,severity=info combined;
- **root@logclient:~# nginx -t** # проверяем синтаксис
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
- **root@logserver:~# cat /var/log/rsyslog/logclient/nginx_access.log**
```bash
2025-12-11T14:22:40+03:00 logclient nginx_access: 10.0.77.13 - - [11/Dec/2025:14:22:40 +0000] "GET / HTTP/1.1" 200 409 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.1 Safari/605.1.15"
2025-12-11T14:22:41+03:00 logclient nginx_access: 10.0.77.13 - - [11/Dec/2025:14:22:41 +0000] "GET / HTTP/1.1" 200 409 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.1 Safari/605.1.15"
```
- **root@logserver:~# ail -f /var/log/rsyslog/logclient/nginx_error.log**
```bash
2025-12-12T11:36:01+03:00 logclient nginx_error: 2025/12/12 11:36:01 [error] 14294#14294: *15 directory index of "/var/www/html/" is forbidden, client: 10.0.77.13, server: _, request: "GET / HTTP/1.1", host: "10.0.77.142"
2025-12-12T11:36:12+03:00 logclient nginx_error: 2025/12/12 11:36:12 [error] 14294#14294: *15 directory index of "/var/www/html/" is forbidden, client: 10.0.77.13, server: _, request: "GET / HTTP/1.1", host: "10.0.77.142"
2025-12-12T11:36:16+03:00 logclient nginx_error: 2025/12/12 11:36:16 [error] 14294#14294: *15 directory index of "/var/www/html/" is forbidden, client: 10.0.77.13, server: _, request: "GET / HTTP/1.1", host: "10.0.77.142
```
- **root@logclient:~# tail -f  /var/log/nginx/error.log**
```bash
2025/12/12 11:36:01 [error] 14294#14294: *15 directory index of "/var/www/html/" is forbidden, client: 10.0.77.13, server: _, request: "GET / HTTP/1.1", host: "10.0.77.142"
2025/12/12 11:36:12 [error] 14294#14294: *15 directory index of "/var/www/html/" is forbidden, client: 10.0.77.13, server: _, request: "GET / HTTP/1.1", host: "10.0.77.142"
2025/12/12 11:36:16 [error] 14294#14294: *15 directory index of "/var/www/html/" is forbidden, client: 10.0.77.13, server: _, request: "GET / HTTP/1.1", host: "10.0.77.142"
```


🧠 
## Настройки audit лога на logclient, передача в rsyslog и на центральный сервер логирования logserver:

- 1	auditd собирает события → пишет в /var/log/audit/audit.log
- 2	rsyslog читает эти логи через imfile
- 3	rsyslog отправляет их на центральный сервер (UDP/TCP 514)
- 4	На сервере логирования — всё складывается в отдельные файлы по хостам
	
- **root@logclient:~# sudo apt install auditd audispd-plugins -y** # устанавливаем audit
- **root@logclient:~# sudo systemctl enable --now auditd** # стартуем audit
- Synchronizing state of auditd.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
- Executing: /usr/lib/systemd/systemd-sysv-install enable auditd
- ## Разрешаем auditd писать логи в rsyslog

- **root@logclient:~# sudo vi /etc/rsyslog.d/30-audit.conf**
- **oot@logclient:~# cat /etc/rsyslog.d/30-audit.conf** # В Ubuntu auditd обычно не передаёт логи напрямую, нужен модуль imfile.
```bash
module(load="imfile")

input(
  type="imfile"
  File="/var/log/audit/audit.log"
  Tag="auditd"
  Severity="info"
  Facility="local6"
  PersistStateInterval="200"
)
# Отправка на центральный сервер (TCP!)
action(
  type="omfwd"
  Target="10.0.77.182"
  Port="514"
  Protocol="tcp"
  Template="RSYSLOG_SyslogProtocol23Format"
  Action.ResumeRetryCount="-1"
  Queue.Type="LinkedList"
  Queue.Size="10000"
)
```
- **root@logclient:~# sudo vi /etc/rsyslog.d/90-central.conf**
```bash
local6.* @10.0.77.182:514 # UDP
local6.* @@10.0.77.182:514 # TCP
```
- **root@logclient:~# sudo systemctl restart rsyslog** # Перезапуск rsyslog
- **root@logclient:~# systemctl status rsyslog**

- **root@logclient:~# tail -f /var/log/audit/audit.log** # убедимся, что аудит лог пишется локально
```bash
type=CRED_DISP msg=audit(1765799991.855:5208): pid=23423 uid=0 auid=1000 ses=1 subj=unconfined msg='op=PAM:setcred grantors=pam_permit acct="root" exe="/usr/bin/sudo" hostname=? addr=? terminal=/dev/pts/1 res=success'UID="root" AUID="spg
```
- **root@logclient:~# systemctl restart auditd**
  
## Настроим сбор логов на центральном сервере
```bash
[Клиент] auditd → /var/log/audit/audit.log
        rsyslog → TCP/514
                ↓
[Центральный сервер логов] rsyslog → /var/log/remote/<host>/audit.log
```

- **root@logserver:/# mkdir -p /var/log/remote**
- **root@logserver:/# chown syslog:adm /var/log/remote**
- **root@logserver:/# chmod 750 /var/log/remote** # rsyslog сам создаст подкаталоги logclient/, если имеет право на /var/log/remote

- **root@logserver:/# vi /etc/rsyslog.d/20-audit-storage.conf** # создание каталогов и файлов в конфиге
```bash
template(name="RemoteAudit" type="string"
         string="/var/log/remote/%HOSTNAME%/audit.log") # разложение audit-логов по хостам

if ($programname == "audit") then {
    action(
        type="omfile"
        dynaFile="RemoteAudit"
        DirCreateMode="0750"
        FileCreateMode="0640"
        DirOwner="syslog"
        DirGroup="adm"
        FileOwner="syslog"
        FileGroup="adm"
    )
    stop
}
```
- **root@logserver:/var/log/rsyslog/logclient# tail -f /var/log/remote/logclient/audit.log** # смотрим полученный на центральном сервере лог аудита машины logclient и видим, что лог передается но время лога универсальное
```bash
- 2025-12-15T11:59:51+03:00 logclient auditd type=CRED_DISP msg=audit(1765799991.855:5208): pid=23423 uid=0 auid=1000 ses=1 subj=unconfined msg='op=PAM:setcred grantors=pam_permit acct="root" exe="/usr/bin/sudo" hostname=? addr=? terminal=/dev/pts/1 res=success'#035UID="root" AUID="spg"
```
- **root@logserver:/var/log/rsyslog/logclient# timedatectl** # время на сервере логов
```bash
               Local time: Mon 2025-12-15 15:08:20 MSK
           Universal time: Mon 2025-12-15 12:08:20 UTC
                 RTC time: Mon 2025-12-15 12:08:20
                Time zone: Europe/Moscow (MSK, +0300)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```
- **root@logclient:~# timedatectl** # время на клиенте логов локальное, но передается UTC
```bash
               Local time: Mon 2025-12-15 15:00:33 MSK
           Universal time: Mon 2025-12-15 12:00:33 UTC
                 RTC time: Mon 2025-12-15 12:00:33
                Time zone: Europe/Moscow (MSK, +0300)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```
## Можно оставить стандартное время логов в UTC и корректировать его уже при консолидации/визуализации/...Лучше хранить UTC, отображать в локальной TZ сервера, что делается автоматически в:

- 👉	•	ELK / OpenSearch
- 👉	•	Graylog
- 👉	•	Splunk

## 27 урок 
## Резервное копирование 

**Домашнее задание** <ins>"Настраиваем бэкапы"</ins>

**Цель**: Настроить бэкапы;

🎯 Что нужно сделать?
- Настроить удаленный бекап каталога /etc c сервера client при помощи borgbackup. Резервные копии должны соответствовать следующим критериям:

- директория для резервных копий /var/backup. Это должна быть отдельная точка монтирования. В данном случае для демонстрации размер не принципиален, достаточно будет и 2GB;
- репозиторий дле резервных копий должен быть зашифрован ключом или паролем - на ваше усмотрение;
- имя бекапа должно содержать информацию о времени снятия бекапа;
- глубина бекапа должна быть год, хранить можно по последней копии на конец месяца, кроме последних трех.
- Последние три месяца должны содержать копии на каждый день. Т.е. должна быть правильно настроена политика удаления старых бэкапов;
- резервная копия снимается каждые 5 минут. Такой частый запуск в целях демонстрации;
- написан скрипт для снятия резервных копий. Скрипт запускается из соответствующей Cron джобы, либо systemd timer-а - на ваше усмотрение;
- настроено логирование процесса бекапа. Для упрощения можно весь вывод перенаправлять в logger с соответствующим тегом. Если настроите не в syslog, то обязательна ротация логов.

- ## Выполнение
- **root@backup:~# lsblk** # в систему добавил новый диск sdb 4 ГБ
```bash
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   30G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0    2G  0 part /boot
└─sda3                      8:3    0   28G  0 part
  └─ubuntu--vg-ubuntu--lv 252:0    0   14G  0 lvm  /
sdb                         8:16   0    4G  0 disk
sr0                        11:0    1 1024M  0 rom
```
- **root@backup:~# mkfs.ext4 -L backup /dev/sdb** # создаем ФС ext4 (форматируем) с меткой "backup"
```bash
mke2fs 1.47.0 (5-Feb-2023)
Creating filesystem with 1048576 4k blocks and 262144 inodes
Filesystem UUID: 90a22b46-3f37-4470-acab-99280ffdea26
Superblock backups stored on blocks:
	32768, 98304, 163840, 229376, 294912, 819200, 884736

Allocating group tables: done
Writing inode tables: done
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done
```
- **root@backup:~# blkid /dev/sdb** # проверяем
```bash
/dev/sdb: LABEL="backup" UUID="551c3ca3-3897-4f76-bfdf-065838e6ba47" BLOCK_SIZE="4096" TYPE="ext4"
```
- **root@backup:~# mkdir -p /var/backup** # создаем точку монтирования
- **root@backup:~# mount /dev/sdb /var/backup** # монтируем диск
- **root@backup:~# df -h /var/backup** # проверяем
```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sdb        3.9G   24K  3.7G   1% /var/backup
```
- ### настраиваем автомонтирование при загрузке
- **root@backup:~# blkid /dev/sdb**
/dev/sdb: LABEL="backup" UUID="551c3ca3-3897-4f76-bfdf-065838e6ba47" BLOCK_SIZE="4096" TYPE="ext4"
- **root@backup:~# cat /etc/fstab** # прописываем монтирование
```bash
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/ubuntu-vg/ubuntu-lv during curtin installation
/dev/disk/by-id/dm-uuid-LVM-drsoih9oPfyXF1rYvUrehdJZ0QdOjlznwCWWWLAB3J982EVfSo8ZkpXhc5fc48Og / ext4 defaults 0 1
# /boot was on /dev/sda2 during curtin installation
/dev/disk/by-uuid/fdc7fdc6-f439-476a-ad4f-1f8e60b9727c /boot ext4 defaults 0 1
# /var/backup was on /dev/sdb during booting
UUID=551c3ca3-3897-4f76-bfdf-065838e6ba47 /var/backup  ext4  defaults  0  2
```
- **root@backup:~# reboot** # перегружаем и проверяем
- **root@backup:~# mount**
```bash
...
- /dev/sdb on /var/backup type ext4 (rw,relatime)
...
```
- **root@backup:~# apt install borgbackup** #
- **root@backup:~# borg --version** #
- borg 1.2.8
- **root@client:~# apt install -y borgbackup** #
- **root@client:~# borg --version** #
- borg 1.2.8
- **root@backup:~# adduser --disabled-password --gecos "" borg** # создаем пользователя сервиса borgbackup
```bash
info: Adding user `borg' ...
info: Selecting UID/GID from range 1000 to 59999 ...
info: Adding new group `borg' (1003) ...
info: Adding new user `borg' (1003) with group `borg (1003)' ...
info: Creating home directory `/home/borg' ...
info: Copying files from `/etc/skel' ...
info: Adding new user `borg' to supplemental / extra groups `users' ...
info: Adding user `borg' to group `users' ...
```
- **root@backup:~# id borg** #  проверяем
```bash
uid=1003(borg) gid=1003(borg) groups=1003(borg),100(users)
```
- **root@backup:~# chown borg:borg /var/backup** # даем права пользователю borg на папку BACKUP
- **root@backup:~# su - borg** # переходим в оболочку пользователя borg
- **borg@backup:~$ pwd** # проверяем, где мы
- /home/borg
- **borg@backup:~$ mkdir .ssh** # настраиваем доступ по ключам
- **borg@backup:~$ touch .ssh/authorized_keys**
- **borg@backup:~$ chmod 700 .ssh**
- **borg@backup:~$ chmod 600 .ssh/authorized_keys**
- **root@client:~# ssh-keygen**
```bash
Generating public/private ed25519 key pair.
Enter file in which to save the key (/root/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /root/.ssh/id_ed25519
Your public key has been saved in /root/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:gNgRE4w+kv+f01jTNlRTEvXjzYA9pkajIjgW2/HOIPo root@client
The key's randomart image is:
+--[ED25519 256]--+
|   o=o      o+o  |
|  .o.+      o+ . |
| o. + o    .+.=..|
|o o  = +  .o +.+o|
| o .* + So. o  .o|
|  .o o =o.+.     |
|  ..   +oo .     |
|   .. o..        |
|    E.o.         |
+----[SHA256]-----+
```
- **root@client:~# borg init --encryption=repokey borg@10.0.77.182:/var/backup** # Инициализируем репозиторий borg на backup сервере с client сервера. Директорий должен быть пустой, иначе его надо вычистить rm
- **root@client:~# borg key export borg@10.0.77.182:/var/backup repo-key.borg** # экспорт открытого ключа на сервер
- **root@client:~# ssh-copy-id borg@10.0.77.182** # Не помешает положить ключ и в домашний каталог пользователя borg на сервере бэкапа
- **root@backup:/home/borg/.ssh# cat /home/borg/.ssh/authorized_keys** # проверим, что ключ появился
- ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOGBaTq4WoCJFmAba9JAnTCnhaRwsSLzL1+CbNhBwFoq root@client
-  **root@backup:/home/borg/.ssh# vi /home/borg/.ssh/authorized_keys** # ограничим использование ключа ... 
- command="borg serve --restrict-to-path /var/backup",no-port-forwarding,no-agent-forwarding,no-pty ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOGBaTq4WoCJFmAba9JAnTCnhaRwsSLzL1+CbNhBwFoq root@client
- **root@client:~# borg create --stats --list borg@10.0.77.182:/var/backup/::"etc-{now:%Y-%m-%d_%H:%M:%S}" /etc** # Запускаем для проверки создания бэкапа
```bash
A /etc/hostname
s /etc/localtime
A /etc/gshadow
A /etc/subgid
A /etc/passwd
A /etc/ld.so.cache
A /etc/hosts
A /etc/group
d /etc
------------------------------------------------------------------------------
Repository: ssh://borg@10.0.77.182/var/backup
Archive name: etc-2025-12-17_15:09:37
```
- **root@client:~# borg list borg@10.0.77.182:/var/backup/**
```bash
etc-2025-12-17_15:09:37              Wed, 2025-12-17 15:09:44 [c50f540b6a164961b5c702f5eed67c670a57fb1f801bcec3c6197d5666cebe24]
```
- **root@client:~# borg list borg@10.0.77.182:/var/backup/::etc-2025-12-17_15:09:37** # смотрим список файлов в бэкапе
```bash
- ...
-rw-r--r-- root   root       1854 Mon, 2025-12-15 09:09:34 etc/passwd
-rw-r--r-- root   root      22499 Fri, 2025-12-12 16:03:42 etc/ld.so.cache
-rw-r--r-- root   root        221 Wed, 2025-12-17 10:24:07 etc/hosts
-rw-r--r-- root   root        802 Mon, 2025-12-15 09:09:36 etc/group
```
- **root@client:~# borg extract borg@10.0.77.182:/var/backup/::etc-2025-12-17_15:09:37 etc/hostname**
- **root@client:~# pwd**
- /root
- **root@client:~# ls ./etc/**
- **root@client:~# ls -hal ./etc/***
```bash
-rw-r--r-- 1 root root 7 Dec 17 10:23 ./etc/hostname
```
- **root@client:~# df -kh ./etc/***
```bash
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv   14G  3.0G   11G  23% /
```

### Автоматизируем создание бэкапов с помощью systemd (глубина бекапа должна быть год, хранить можно по последней копии на конец месяца, кроме последних трех.Последние три месяца должны содержать копии на каждый день, резервная копия снимается каждые 5 минут)
- **root@client:~# vim /etc/systemd/system/borg-backup.service** # создаем сервис
```bash
[Unit]
Description=Borg Backup

[Service]
Type=oneshot

# Парольная фраза
Environment="BORG_PASSPHRASE=Otus1234"
# Репозиторий
Environment=REPO=borg@10.0.77.182:/var/backup/
# Что бэкапим
Environment=BACKUP_TARGET=/etc

# Создание бэкапа
ExecStart=/usr/bin/borg create \
    --stats                \
    ${REPO}::etc-{now:%%Y-%%m-%%d_%%H:%%M:%%S} ${BACKUP_TARGET}

# Проверка бэкапа
ExecStart=/usr/bin/borg check ${REPO}

# Очистка старых бэкапов
ExecStart=/usr/bin/borg prune \
    --keep-daily  90      \
    --keep-monthly 12     \
    --keep-yearly  1       \
    ${REPO}
```

- **root@client:~# vim /etc/systemd/system/borg-backup.timer** # создаем таймер
```bash
[Unit]
Description=Borg Backup

[Timer]
OnUnitActiveSec=5min

[Install]
WantedBy=timers.target
```
- **root@client:~# systemctl enable borg-backup.timer** # Включаем и 
```bash
Created symlink /etc/systemd/system/timers.target.wants/borg-backup.timer → /etc/systemd/system/borg-backup.timer.
```
- **root@client:~# systemctl start borg-backup.timer** # запускаем службу таймера

- **root@client:~# systemctl list-timers | grep borg** # НЕ работает!
```bash
-                                  - -                                      - borg-backup.timer              borg-backup.service
```
- **root@client:~# systemctl stop borg-backup.timer**
- **root@client:~# systemctl daemon-reexec**
- **root@client:~# systemctl daemon-reexec**
- **root@client:~# systemctl daemon-reload**
- **root@client:~# systemctl start borg-backup.timer**
- **root@client:~# systemctl status borg-backup.timer**
```bash
systemctl list-timers | grep borg
● borg-backup.timer - Borg Backup every 5 minutes
     Loaded: loaded (/etc/systemd/system/borg-backup.timer; enabled; preset: enabled)
     Active: active (waiting)
```
- **root@client:~# systemctl list-timers | grep borg** # Работает!
```bash
Thu 2025-12-18 11:56:11 MSK 4min 4s Thu 2025-12-18 11:51:11 MSK      55s ago borg-backup.timer              borg-backup.service
```
- **root@client:~# borg list borg@10.0.77.182:/var/backup/** # Просмотрим архивы
```bash
etc-2025-12-17_15:09:37              Wed, 2025-12-17 15:09:44 [c50f540b6a164961b5c702f5eed67c670a57fb1f801bcec3c6197d5666cebe24]
etc-2025-12-18_15-29-12              Thu, 2025-12-18 15:29:14 [b6c13f983e92d9336d3b978faa8a5016c94175a58e25087a8c042ec8e449dbea]
etc-2025-12-18_15:36:43              Thu, 2025-12-18 15:36:44 [9eb71341c2b8ef113b0403ea660f72a74a100a2f8be0f550d03b7ef3b1136eba]
```
- **root@backup:/home/borg/.ssh# borg list /var/backup** # Посмотрим на самом сервере бэкапов
```bash
Warning: Attempting to access a previously unknown unencrypted repository!
Do you want to continue? [yN] y
etc-2025-12-17_15:09:37              Wed, 2025-12-17 15:09:44 [c50f540b6a164961b5c702f5eed67c670a57fb1f801bcec3c6197d5666cebe24]
etc-2025-12-18_15-29-12              Thu, 2025-12-18 15:29:14 [b6c13f983e92d9336d3b978faa8a5016c94175a58e25087a8c042ec8e449dbea]
etc-2025-12-18_15:36:43              Thu, 2025-12-18 15:36:44 [9eb71341c2b8ef113b0403ea660f72a74a100a2f8be0f550d03b7ef3b11
```

## 28 урок 
## Сетевая лаборатория

**Домашнее задание** <ins>"Разворачиваем сетевую лабораторию"</ins>

**Цель**: Научиться менять базовые сетевые настройки в Linux-based системах;;

🎯 Что нужно сделать?

### Задание состоит из 2-х частей: теоретической и практической.
### 1. В теоретической части требуется: 
- Найти свободные подсети
- Посчитать количество узлов в каждой подсети, включая свободные
- Указать Broadcast-адрес для каждой подсети
- Проверить, нет ли ошибок при разбиении

### 2. В практической части требуется: 
- Соединить офисы в сеть согласно логической схеме и настроить роутинг
- Интернет-трафик со всех серверов должен ходить через inetRouter
- Все сервера должны видеть друг друга (должен проходить ping)
- У всех новых серверов отключить дефолт на NAT (eth0), который vagrant поднимает для связи
- Добавить дополнительные сетевые интерфейсы, если потребуется

### ВЫПОЛНЕНИЕ

- Дана схема сети:
<img width="785" height="891" alt="Screenshot 2026-01-05 at 11 06 55" src="https://github.com/user-attachments/assets/2dba85d1-969b-4917-bf40-4cea137d4c43" />

### 1. Разберем ее:
- 10  сетей для хостов
- 4 сети для интерфейсов, через которые связаны маршрутизаторы (условно, так как маршрутизация будет строится на серверах Linux). Четвертая сеть на схеме - Интернет.
- Посчитаем сети:
<img width="945" height="927" alt="Screenshot 2026-01-13 at 09 58 52" src="https://github.com/user-attachments/assets/a8c32466-fd2e-4d0c-869a-ef923264b885" />

### 2. Настроим сетевой стенд
- Создадим 7 ВМ с минимальным колличеством сетевых интерфейсов в одной "Distributed port group" (разделим сетями) для тестов по ДЗ (3 ВМ - по 1 сетевому интерфейсу; 3 ВМ - по 2 и 1 ВМ - с 4-мя): 
<img width="1339" height="491" alt="Screenshot 2026-01-05 at 15 04 36" src="https://github.com/user-attachments/assets/92eb33c9-23b0-4fa8-8f5f-b1eaf2e3d9e8" />
- установил на все машины Linux Ubuntu 24.04
- настройки интерфейсов на всех машинах (Скриншоты использованы потому что после установки VMware Remote Console все равно сложности с "copy/paste"):
<img width="587" height="390" alt="Screenshot 2026-01-06 at 13 54 58" src="https://github.com/user-attachments/assets/05b2f522-1e79-43da-878a-e86fcb6635c2" />
<img width="599" height="560" alt="Screenshot 2026-01-06 at 13 55 18" src="https://github.com/user-attachments/assets/b35504b7-3bbb-4b1b-9fe2-c2c897c03228" />
<img width="601" height="318" alt="Screenshot 2026-01-06 at 13 55 36" src="https://github.com/user-attachments/assets/78f9591b-e13c-4a04-b5ed-0ec18c1bbc2d" />
<img width="540" height="359" alt="Screenshot 2026-01-06 at 13 55 51" src="https://github.com/user-attachments/assets/7e1a064c-fe80-4bbd-bebd-9d3cb80d3df2" />
<img width="542" height="390" alt="Screenshot 2026-01-06 at 13 56 07" src="https://github.com/user-attachments/assets/b2ac5a94-9cae-42f0-9f99-1fac0364d0da" />
<img width="536" height="314" alt="Screenshot 2026-01-06 at 13 56 19" src="https://github.com/user-attachments/assets/08c74225-645b-4491-99e7-aa44fe0e6a58" />
<img width="534" height="313" alt="Screenshot 2026-01-06 at 13 56 31" src="https://github.com/user-attachments/assets/b4d135a7-8b5e-46c2-9b75-4df2fd506f85" />

- добавил дополнительные адреса на хостовую машину под Windows в том же VLAN что и 7 тестовых ВМ:
- 
<img width="393" height="209" alt="Screenshot 2026-01-13 at 10 13 53" src="https://github.com/user-attachments/assets/93bc1c29-0911-47ea-b99f-1f3a3a7c4e78" />

- и подключился ко всем по ssh:

<img width="1021" height="472" alt="Screenshot 2026-01-13 at 10 16 32" src="https://github.com/user-attachments/assets/1292433e-9795-44ae-ae44-9926933c8483" />

### нужно настроить маршрутизацию и NAT таким образом, чтобы доступ в Интернет со всех хостов был через inetRouter и каждый сервер должен быть доступен с любого из 7 хостов
- **Открываем форвардинг на всех роутерах:**
- **root@inetRouter:/etc# cat /etc/sysctl.conf** # раскомментируем форвардинг на уровне ядра 
```bash
# Uncomment the next line to enable packet forwarding for IPv4
net.ipv4.ip_forward=1
```
- **root@inetRouter:/etc# sudo sysctl -p** # перечитывает параметры из /etc/sysctl.conf и применяет их сразу, без перезагрузки
- net.ipv4.ip_forward = 1
- **root@inetRouter:/etc# cat /proc/sys/net/ipv4/ip_forward** # показывает текущее значение параметра форвардинга
- 1
- **Проверил связь с соседями (13 команд ping со всех машин по соседям). Все доступны.**
- **Настраиваем iptables на NAT (inetRouter)**
- **root@inetRouter:~# iptables-save**
```bash
# Generated by iptables-save v1.8.10 (nf_tables) on Tue Jan  6 12:06:06 2026
*filter
:INPUT ACCEPT [5015:355494]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A FORWARD -i ens224 -o ens192 -j ACCEPT
-A FORWARD -i ens192 -o ens224 -m state --state RELATED,ESTABLISHED -j ACCEPT
COMMIT
# Completed on Tue Jan  6 12:06:06 2026
# Generated by iptables-save v1.8.10 (nf_tables) on Tue Jan  6 12:06:06 2026
*nat
:PREROUTING ACCEPT [5:469]
:INPUT ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:POSTROUTING ACCEPT [39:2460]
-A PREROUTING -p tcp -m tcp --dport 1022 -j DNAT --to-destination 192.168.255.2:22
-A POSTROUTING -o ens192 -j MASQUERADE
COMMIT
# Completed on Tue Jan  6 12:06:06 2026
```
- **~ ssh -p 1022 spg@10.0.77.182**
- **spg@centralrouter:~$** # получили доступ к CentralRouter за NAT-ом по ssh
- **Дальше настроим маршрутизацию на оставшихся роутерах и серверах через netplan (конфигурация серверов без изменений, но удобно для копирования стало)**
- **0. InetRouter**
```bash
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: no
      addresses:
        - 10.0.77.182/24
      routes:
        - to: default
          via: 10.0.77.1
      nameservers:
        addresses: [10.0.1.167, 10.0.1.194]

    ens224:
      dhcp4: no
      addresses:
        - 192.168.255.1/30
      routes:
        - to: 192.168.0.0/16
          via: 192.168.255.2
```
- **1. CentralRouter**
```bash
root@centralrouter:~# cat /etc/netplan/50-cloud-init.yaml
network:
  version: 2
  renderer: networkd

  ethernets:

    ens161:
      dhcp4: no
      addresses:
        - 192.168.255.2/30
      routes:
        - to: default
          via: 192.168.255.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]

    ens192:
      dhcp4: no
      addresses:
        - 192.168.0.1/28

    ens224:
      dhcp4: no
      addresses:
        - 192.168.255.9/30
      routes:
        - to: 192.168.2.0/24
          via: 192.168.255.10

    ens256:
      dhcp4: no
      addresses:
        - 192.168.255.5/30
      routes:
        - to: 192.168.1.0/24
          via: 192.168.255.6

```
- **2. CentralServer**
```bash
root@centralServer:~# cat /etc/netplan/00-installer-config.yaml
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: no
      addresses:
        - 192.168.0.2/28
      routes:
        - to: default
          via: 192.168.0.1
      nameservers:
        addresses: [ 8.8.8.8, 10.0.1.167]
```
- **3. office1Router**
```bash
root@office1router:~# cat /etc/netplan/50-cloud-init.yaml
network:
  version: 2
  ethernets:
    ens192:
      dhcp4: no
      addresses:
        - 192.168.255.10/30
      routes:
        - to: default
          via: 192.168.255.9
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]

    ens224:
      dhcp4: no
      addresses:
        - 192.168.2.129/26
```
- **4. office2Router**
```bash
root@office2router:~# cat /etc/netplan/50-cloud-init.yaml
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: no
      addresses:
        - 192.168.255.6/30
      routes:
        - to: default
          via: 192.168.255.5
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]

    ens224:
      dhcp4: no
      addresses:
        - 192.168.1.1/25
```
- **5. office1Server**
```bash
root@office1server:~# cat /etc/netplan/50-cloud-init.yaml
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: no
      addresses:
        - 192.168.2.130/26
      routes:
        - to: default
          via: 192.168.2.129
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```
- **6. office2Server**
```bash
root@office2server:~# cat /etc/netplan/50-cloud-init.yaml
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: no
      addresses:
        - 192.168.1.2/25
      routes:
        - to: default
          via: 192.168.1.1/25
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```
### Результаты конфигурации маршрутов в netplan проверялись в "ip route show"
- **root@inetRouter:~# apt install -y traceroute** # устанавливаем утилиту traceroute на все машины для проверки ДЗ
- **root@inetRouter:~# traceroute 192.168.2.130** # проверяем доступность и прохождение с inetRouter на office1Server
```bash
traceroute to 192.168.2.130 (192.168.2.130), 30 hops max, 60 byte packets
 1  192.168.255.2 (192.168.255.2)  0.109 ms  0.073 ms  0.071 ms
 2  192.168.255.10 (192.168.255.10)  0.165 ms  0.127 ms  0.113 ms
 3  192.168.2.130 (192.168.2.130)  0.235 ms  0.216 ms  0.203 ms
```
- **root@inetRouter:~# traceroute 192.168.1.2** # проверяем доступность и прохождение с inetRouter на office2Server
```bash
traceroute to 192.168.1.2 (192.168.1.2), 30 hops max, 60 byte packets
 1  192.168.255.2 (192.168.255.2)  0.151 ms  0.108 ms  0.114 ms
 2  192.168.255.6 (192.168.255.6)  0.305 ms  0.288 ms  0.277 ms
 3  192.168.1.2 (192.168.1.2)  0.396 ms  0.383 ms  0.370 ms
```
- **root@inetRouter:~# traceroute 192.168.0.2** # проверяем доступность и прохождение с inetRouter на CentralServer
```bash
traceroute to 192.168.0.2 (192.168.0.2), 30 hops max, 60 byte packets
 1  192.168.255.2 (192.168.255.2)  0.103 ms  0.088 ms  0.065 ms
 2  192.168.0.2 (192.168.0.2)  0.150 ms  0.132 ms  0.125 ms
```
- **root@centralServer:~# traceroute 192.168.2.130** # проверяем доступность и прохождение с CentralServer на office1Server
```bash
traceroute to 192.168.2.130 (192.168.2.130), 30 hops max, 60 byte packets
 1  _gateway (192.168.0.1)  0.116 ms  0.093 ms  0.080 ms
 2  192.168.255.10 (192.168.255.10)  0.193 ms  0.200 ms  0.195 ms
 3  192.168.2.130 (192.168.2.130)  0.336 ms  0.306 ms  0.288 ms**
```
- **root@centralServer:~# traceroute 192.168.1.2** # проверяем доступность и прохождение с CentralServer на office2Server
```bash
traceroute to 192.168.1.2 (192.168.1.2), 30 hops max, 60 byte packets
 1  _gateway (192.168.0.1)  0.115 ms  0.104 ms  0.090 ms
 2  192.168.255.6 (192.168.255.6)  0.212 ms  0.212 ms  0.199 ms
 3  192.168.1.2 (192.168.1.2)  0.332 ms  0.320 ms  0.283 ms
```
- **root@centralServer:~# traceroute 8.8.8.8** # проверяем доступность и прохождение с CentralServer на 8.8.8.8
```bash
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  _gateway (192.168.0.1)  0.154 ms  0.123 ms  0.106 ms
 2  192.168.255.1 (192.168.255.1)  0.291 ms  0.279 ms  0.262 ms
 3  10.0.77.1 (10.0.77.1)  2.656 ms  1.816 ms  2.834 ms
 4  asr1002-x-1-po7.garant.ru (80.253.4.64)  1.174 ms  0.942 ms  1.343 ms
 5  17-229-9-185.host.cirex.ru (185.9.229.17)  17.516 ms  17.365 ms  17.670 ms
 6  10.10.11.17 (10.10.11.17)  2.374 ms  1.910 ms  2.066 ms
 7  msk-ix-gw3.google.com (195.208.208.250)  4.453 ms  2.057 ms  9.362 ms
 8  * 192.178.241.119 (192.178.241.119)  2.435 ms  2.616 ms
 9  * 192.178.241.66 (192.178.241.66)  1.952 ms 192.178.243.132 (192.178.243.132)  1.916 ms
10  * * *
```
- **root@office1server:~# traceroute 192.168.0.2** # проверяем доступность и прохождение с office1Server на CentralServer
```bash
traceroute to 192.168.0.2 (192.168.0.2), 30 hops max, 60 byte packets
 1  _gateway (192.168.2.129)  0.124 ms  0.121 ms  0.100 ms
 2  192.168.255.9 (192.168.255.9)  0.260 ms  0.243 ms  0.238 ms
 3  192.168.0.2 (192.168.0.2)  0.380 ms  0.365 ms  0.354 ms
```
- **root@office1server:~# traceroute 192.168.1.2** # проверяем доступность и прохождение с office1Server на office2Server
```bash
traceroute to 192.168.1.2 (192.168.1.2), 30 hops max, 60 byte packets
 1  _gateway (192.168.2.129)  0.115 ms  0.084 ms  0.068 ms
 2  192.168.255.9 (192.168.255.9)  0.216 ms  0.213 ms  0.198 ms
 3  192.168.255.6 (192.168.255.6)  0.310 ms  0.295 ms  0.281 ms
 4  192.168.1.2 (192.168.1.2)  0.404 ms  0.407 ms  0.392 ms
```
- **root@office1server:~# traceroute 8.8.8.8** # проверяем доступность и прохождение с office1Server на 8.8.8.8
```bash
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  _gateway (192.168.2.129)  0.128 ms  0.106 ms  0.095 ms
 2  192.168.255.9 (192.168.255.9)  0.238 ms  0.227 ms  0.220 ms
 3  192.168.255.1 (192.168.255.1)  0.420 ms  0.409 ms  0.398 ms
 4  10.0.77.1 (10.0.77.1)  2.024 ms  2.605 ms  2.806 ms
 5  asr1002-x-1-po7.garant.ru (80.253.4.64)  1.022 ms  1.194 ms  1.386 ms
 6  17-229-9-185.host.cirex.ru (185.9.229.17)  1.554 ms  1.310 ms  1.481 ms
 7  10.10.11.17 (10.10.11.17)  1.754 ms  2.432 ms  2.243 ms
 8  msk-ix-gw3.google.com (195.208.208.250)  3.120 ms  4.514 ms  2.912 ms
 9  192.178.241.65 (192.178.241.65)  2.700 ms *  3.030 ms
10  209.85.143.20 (209.85.143.20)  2.752 ms 192.178.241.70 (192.178.241.70)  2.585 ms 192.178.241.148 (192.178.241.148)  2.574 ms
11  * * *
```
- **root@office2server:~# traceroute 192.168.0.2** # проверяем доступность и прохождение с office2Server на CentralServer
```bash
traceroute to 192.168.0.2 (192.168.0.2), 30 hops max, 60 byte packets
 1  _gateway (192.168.1.1)  0.119 ms  0.097 ms  0.104 ms
 2  192.168.255.5 (192.168.255.5)  0.245 ms  0.234 ms  0.214 ms
 3  192.168.0.2 (192.168.0.2)  0.352 ms  0.335 ms  0.302 ms
```
- **root@office2server:~# traceroute 192.168.2.130** # проверяем доступность и прохождение с office2Server на office1Server
```bash
traceroute to 192.168.2.130 (192.168.2.130), 30 hops max, 60 byte packets
 1  _gateway (192.168.1.1)  0.120 ms  0.098 ms  0.098 ms
 2  192.168.255.5 (192.168.255.5)  0.233 ms  0.212 ms  0.197 ms
 3  192.168.255.10 (192.168.255.10)  0.309 ms  0.291 ms  0.276 ms
 4  192.168.2.130 (192.168.2.130)  0.417 ms  0.407 ms  0.410 ms
```
- **root@office2server:~# traceroute 8.8.8.8** # проверяем доступность и прохождение с office2Server на 8.8.8.8
```bash
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  _gateway (192.168.1.1)  0.122 ms  0.097 ms  0.085 ms
 2  192.168.255.5 (192.168.255.5)  0.209 ms  0.197 ms  0.190 ms
 3  192.168.255.1 (192.168.255.1)  0.284 ms  0.269 ms  0.235 ms
 4  10.0.77.1 (10.0.77.1)  2.227 ms  2.379 ms  2.122 ms
 5  asr1002-x-1-po7.garant.ru (80.253.4.64)  1.095 ms  1.283 ms  0.891 ms
 6  17-229-9-185.host.cirex.ru (185.9.229.17)  1.716 ms  1.375 ms  1.531 ms
 7  10.10.11.17 (10.10.11.17)  1.943 ms  2.366 ms  2.163 ms
 8  msk-ix-gw3.google.com (195.208.208.250)  2.146 ms * *
 9  * * 192.178.241.65 (192.178.241.65)  2.653 ms
10  209.85.143.20 (209.85.143.20)  2.648 ms 192.178.241.148 (192.178.241.148)  2.493 ms 192.178.241.70 (192.178.241.70)  2.415 ms
11  * * *
```
###  🎄 На этом это красивое ДЗ завершено 
 
## 29 урок 
## DHCP, PXE

**Домашнее задание** <ins>"Настройка PXE сервера для автоматической установки"</ins>

**Цель**: Отработать навыки установки и настройки DHCP, TFTP, PXE загрузчика и автоматической загрузки;

🎯 Что нужно сделать?
- Настроить загрузку по сети дистрибутива Ubuntu 24
Установка должна проходить из HTTP-репозитория.
- Настроить автоматическую установку c помощью файла user-data
<details>
<summary> = 🧠 Теория 🧠= </summary>
	
## PXE (Preboot eXecution Environment)
### Описание
```bash
PXE (Preboot eXecution Environment) — это спецификация сетевой загрузки, разработанная Intel,
позволяющая компьютеру загружать операционную систему по сети, без использования локальных носителей (HDD/SSD/USB).
PXE широко применяется для:
	•	массовой установки ОС;
	•	автоматизации развёртывания серверов;
	•	diskless-клиентов;
	•	recovery / rescue-сред;
	•	CI/CD и bare-metal provisioning.
```

### Участники PXE-загрузки
```bash
Компонент													Назначение
PXE-клиент													Компьютер с поддержкой PXE (BIOS/UEFI)
DHCP-сервер													Выдаёт IP-адрес и параметры загрузки
TFTP / HTTP сервер											Передаёт загрузчик и образы
Bootloader													pxelinux / GRUB / iPXE
ОС / Инсталлятор											Linux kernel + initrd
```

### Общая схема PXE-загрузки
```bash
[ PXE CLIENT ]
      |
      | 1. DHCP DISCOVER (PXE)
      v
[ DHCP SERVER ]
      |
      | 2. IP + bootfile + server
      v
[ TFTP / HTTP SERVER ]
      |
      | 3. Bootloader
      v
[ BOOTLOADER ]
      |
      | 4. kernel + initrd
      v
[ OS / INSTALLER ]
```
### Пошаговый процесс загрузки
1. Инициализация PXE
```bash
	•	BIOS/UEFI передаёт управление PXE ROM сетевой карты
	•	Клиент инициализирует сеть
	•	Отправляется DHCPDISCOVER с PXE-опциями
```

2. DHCP-ответ
```bash
DHCP-сервер возвращает DHCPOFFER, содержащий:
DHCP option						Описание
IP address						IP-адрес клиента
option 66						Адрес TFTP/HTTP сервера
option 67						Имя загрузочного файла

Пояснения опций:
🔹 DHCP option 66
Boot Server Name
	•	передаёт IP-адрес или DNS-имя сервера, где лежит загрузчик
	•	обычно это TFTP-сервер, иногда HTTP
Пример:
option 66 192.168.1.10;
или:
next-server 192.168.1.10;
🔹 DHCP option 67
Bootfile Name
	•	передаёт имя файла загрузчика
	Пример:
option 67 "pxelinux.0";
или:
filename "grubx64.efi";

Пример DHCP-конфигурации:

next-server 192.168.1.10;
filename "pxelinux.0";
```
3. Загрузка загрузчика
```bash
Клиент загружает загрузчик по сети:
	•	BIOS PXE → TFTP
	•	UEFI PXE → TFTP или HTTP

Примеры загрузчиков:
	•	pxelinux.0 (Legacy BIOS)
	•	grubx64.efi (UEFI)
	•	ipxe.efi
```

4. Загрузка ядра и initrd
```bash
Bootloader:
	•	читает конфигурацию
	•	загружает vmlinuz и initrd.img
	•	передаёт параметры ядру

Пример:
linux vmlinuz ip=dhcp inst.repo=http://server/repo
initrd initrd.img
```bash

5. Запуск ОС или установщика
```bash
Возможные сценарии:
	•	запуск Live Linux;
	•	установка ОС;
	•	автоматическая установка (Kickstart / Preseed / Autoinstall);
	•	загрузка recovery-среды.

PXE завершает работу после передачи управления ядру ОС.
```

### BIOS PXE vs UEFI PXE
```bash
Параметр								BIOS PXE							UEFI PXE
Загрузчик								pxelinux.0							grubx64.efi
Протокол								TFTP								TFTP / HTTP
Secure Boot								❌									✅
Скорость								ниже								выше
```

### iPXE
```bash
iPXE — расширенная реализация PXE:
	•	поддержка HTTP / HTTPS;
	•	скрипты и меню;
	•	chainloading;
	•	авторизация;
	•	высокая скорость загрузки.
Часто используется вместо классического PXE в production-средах.
```

### Минимальная инфраструктура PXE
```bash
PXE Server:
- DHCP
- TFTP
- HTTP (опционально)

Client:
- PXE-enabled NIC
```

### Ограничения PXE
```bash	
	•	требуется DHCP;
	•	TFTP медленный (решается iPXE + HTTP);
	•	зависит от сетевой инфраструктуры.
```

### Кратко
- PXE — это технология сетевой загрузки, при которой клиент получает параметры по DHCP, загружает загрузчик по сети, затем ядро и initrd, и запускает ОС или установщик без использования локальных носителей.

### Полезные сценарии применения
```bash
	•	массовая установка серверов;
	•	bare-metal provisioning;
	•	diskless рабочие станции;
	•	recovery и диагностика.
```
</details>

- ## Выполнение
- **root@pxeserver:~# systemctl stop ufw** # останавливаем фаервол
- **root@pxeserver:~# systemctl disable ufw** #
```bash
Synchronizing state of ufw.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install disable ufw
Removed "/etc/systemd/system/multi-user.target.wants/ufw.service".
```
- **root@pxeserver:~# systemctl status ufw** # проверяем
```bash
○ ufw.service - Uncomplicated firewall
     Loaded: loaded (/usr/lib/systemd/system/ufw.service; disabled; preset: enabled)
     Active: inactive (dead)
       Docs: man:ufw(8)

Dec 19 12:23:20 pxeserver systemd[1]: Starting ufw.service - Uncomplicated firewall...
Dec 19 12:23:20 pxeserver systemd[1]: Finished ufw.service - Uncomplicated firewall.
Dec 22 08:11:46 pxeserver systemd[1]: Stopping ufw.service - Uncomplicated firewall...
Dec 22 08:11:46 pxeserver ufw-init[8914]: Skip stopping firewall: ufw (not enabled)
Dec 22 08:11:46 pxeserver systemd[1]: ufw.service: Deactivated successfully.
Dec 22 08:11:46 pxeserver systemd[1]: Stopped ufw.service - Uncomplicated firewall.
```
- **root@pxeserver:~# sudo apt update** # обновляем кэш
- **root@pxeserver:~# sudo apt install dnsmasq** # устанавливаем утилиту dnsmasq
- **root@pxeserver:~# cat /etc/dnsmasq.d/pxe.conf** # создаем файл конфигурации PXE
```bash
#Указываем интерфейс в на котором будет работать DHCP/TFTP
interface=eth1
bind-interfaces
#Также указаваем интерфейс и range адресов которые будут выдаваться по DHCP
dhcp-range=eth1,10.0.77.186,10.0.77.190
#Имя файла, с которого надо начинать загрузку для Legacy boot (этот пример рассматривается в методичке)
dhcp-boot=pxelinux.0
#Имена файлов, для UEFI-загрузки (не обязательно добавлять)
dhcp-match=set:efi-x86_64,option:client-arch,7
dhcp-boot=tag:efi-x86_64,bootx64.efi
#Включаем TFTP-сервер
enable-tftp
#Указываем каталог для TFTP-сервера
tftp-root=/srv/tftp/amd64
```
- **root@pxeserver:~# mkdir -p /srv/tftp** # создаем каталог для файлов TFTP-сервера
- **root@pxeserver:~# wget http://cdimage.ubuntu.com/ubuntu-server/daily-live/current/noble-netboot-amd64.tar.gz
tar -xzvf noble-netboot-amd64.tar.gz -C /srv/tftp** # скачиваем файлы для сетевой установки Ubuntu 24.04
```bash
--2025-12-22 08:29:52--  http://cdimage.ubuntu.com/ubuntu-server/daily-live/current/noble-netboot-amd64.tar.gz
Resolving cdimage.ubuntu.com (cdimage.ubuntu.com)... 91.189.91.124, 185.125.190.37, 2620:2d:4000:1::17, ...
Connecting to cdimage.ubuntu.com (cdimage.ubuntu.com)|91.189.91.124|:80... connected.
HTTP request sent, awaiting response... 404 Not Found
2025-12-22 08:29:53 ERROR 404: Not Found. 

tar (child): noble-netboot-amd64.tar.gz: Cannot open: No such file or directory
tar (child): Error is not recoverable: exiting now
tar: Child returned status 2
tar: Error is not recoverable: exiting now
```
### но его там уже нет... 
- **root@pxeserver:~# wget http://cdimage.ubuntu.com/ubuntu-server/daily-live/current/resolute-netboot-amd64.tar.gz** # но есть другой
```bash
--2025-12-22 08:42:17--  http://cdimage.ubuntu.com/ubuntu-server/daily-live/current/resolute-netboot-amd64.tar.gz
Resolving cdimage.ubuntu.com (cdimage.ubuntu.com)... 91.189.91.124, 185.125.190.37, 2620:2d:4000:1::17, ...
Connecting to cdimage.ubuntu.com (cdimage.ubuntu.com)|91.189.91.124|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 112038753 (107M) [application/x-gzip]
Saving to: ‘resolute-netboot-amd64.tar.gz’

resolute-netboot-amd64.tar.gz  100%[==================================================>] 106.85M  12.0MB/s    in 9.9s

2025-12-22 08:42:27 (10.8 MB/s) - ‘resolute-netboot-amd64.tar.gz’ saved [112038753/112038753]
```
- **root@pxeserver:~# tar -xzvf resolute-netboot-amd64.tar.gz -C /srv/tftp** # распакуем
```bash
./
./amd64/
./amd64/grub/
./amd64/grub/grub.cfg
./amd64/initrd
./amd64/grubx64.efi
./amd64/linux
./amd64/pxelinux.0
./amd64/bootx64.efi
./amd64/pxelinux.cfg/
./amd64/pxelinux.cfg/default
./amd64/ldlinux.c32
```
-**root@pxeserver:~# systemctl restart dnsmasq** # перезапускаем службу dnsmasq

##  Настройка Web-сервера
- Для того, чтобы отдавать файлы по HTTP нам потребуется настроенный веб-сервер.
- **root@pxeserver:~# sudo apt install apache2**
- **root@pxeserver:~# mkdir -p /srv/images**
- **root@pxeserver:~# cd /srv/images/**
- **root@pxeserver:/srv/images# wget http://cdimage.ubuntu.com/ubuntu-server/daily-live/current/resolute-live-server-amd64.iso**
```bash
--2025-12-22 12:54:54--  http://cdimage.ubuntu.com/ubuntu-server/daily-live/current/resolute-live-server-amd64.iso
Resolving cdimage.ubuntu.com (cdimage.ubuntu.com)... 185.125.190.37, 91.189.91.124, 2620:2d:4000:1::17, ...
Connecting to cdimage.ubuntu.com (cdimage.ubuntu.com)|185.125.190.37|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2417293312 (2.3G) [application/x-iso9660-image]
Saving to: ‘resolute-live-server-amd64.iso’

resolute-live-server-amd64.iso   100%[========================================================>]   2.25G  26.7MB/s    in 2m 2s

2025-12-22 12:56:57 (18.9 MB/s) - ‘resolute-live-server-amd64.iso’ saved [2417293312/2417293312]
```  
- **root@pxeserver:/srv/images# cat /etc/apache2/sites-available/ks-server.conf** #создали файл 
```bash
#Указываем IP-адрес хоста и порт на котором будет работать Web-сервер
<VirtualHost 10.0.77.182:80>
DocumentRoot /
# Указываем директорию /srv/images из которой будет загружаться iso-образ
<Directory /srv/images>
Options Indexes MultiViews
AllowOverride All
Require all granted
</Directory>
</VirtualHost>
```
- **root@pxeserver:/srv/images# sudo a2ensite ks-server.conf** # активируем конфигурацию ks-server в apache
```bash
Enabling site ks-server.
To activate the new configuration, you need to run:
  systemctl reload apache2 #перезагрузим позже
```
- **cat /srv/tftp/amd64/pxelinux.cfg/default** # вносим изменения в файл
```bash
DEFAULT install
LABEL install
  KERNEL linux
  INITRD initrd
  APPEND root=/dev/ram0 ramdisk_size=3000000 ip=dhcp iso-url=http://10.0.77.182/srv/images/resolute-live-server-amd64.iso ---
```
### В данном файле мы указываем что файлы linux и initrd будут забираться по tftp, а сам iso-образ ubuntu 24.04
### будет скачиваться из нашего веб-сервера http://10.0.0.20/srv/images/noble-live-server-amd64.iso
### Из-за того, что образ достаточно большой (2.6G) и он сначала загружается в ОЗУ, необходимо указать
### размер ОЗУ до 3 гигабайт (root=/dev/ram0 ramdisk_size=3000000)

- **root@pxeserver:/srv/images# systemctl restart apache2** # перегружаем apache2

### Запускаем подготовленную машину-клиента

### Адрес получил

- <img width="1197" height="494" alt="Screenshot 2025-12-22 at 16 27 45" src="https://github.com/user-attachments/assets/8032617f-ccc0-4139-9ddf-22de3757be6c" />

### Пошла установка
<img width="1054" height="525" alt="Screenshot 2025-12-22 at 16 55 21" src="https://github.com/user-attachments/assets/36f9026b-b020-41d3-9cd6-83cd62abf755" />


## Настройка автоматической установки Ubuntu 24.04
cоздаём каталог для файлов с автоматической установкой
- **root@pxeserver:/srv/images# mkdir /srv/ks** # создаём файл /srv/ks/user-data и 

- **root@pxeserver:/srv/images# vim /srv/ks/user-data** # добавляем в него следующее содержимое
```bash
autoinstall:
apt:
disable_components: []
geoip: true
preserve_sources_list: false
primary:
- arches:
- amd64
- i386
uri: http://us.archive.ubuntu.com/ubuntu
- arches:
- default
uri: http://ports.ubuntu.com/ubuntu-ports
drivers:
install: false
identity:
hostname: linux
password: $6$sJgo6Hg5zXBwkkI8$btrEoWAb5FxKhajagWR49XM4EAOfO/
Dr5bMrLOkGe3KkMYdsh7T3MU5mYwY2TIMJpVKckAwnZFs2ltUJ1abOZ.
realname: otus
username: otus
kernel:
package: linux-generic
keyboard:
layout: us
toggle: null
variant: ''
locale: en_US.UTF-8
network:
ethernets:
enp0s3:
dhcp4: true
enp0s8:
dhcp4: true
version: 2
ssh:
allow-pw: true
authorized-keys: []
install-server: true
updates: security
version: 1
```
- В данном файле указываются следующие настройки:
• устанавливается apt-репозиторий http://us.archive.ubuntu.com/ubuntu
• отключена автоматическая загрузка драйверов
• задаётся hostname linux
• создаётся пользователь otus c паролем 123 (пароль зашифрован в SHA512)
• использование английской раскладки
• добавлена настройка получения адресов по DHCP (для обоих портов)
• устанавливается openssh-сервер с доступом по логину и паролю

- **root@pxeserver:/srv/images# touch /srv/ks/meta-data** # создаем файл с иетаданными (хранит дополнительную информацию о хосте),не будем пока
- **root@pxeserver:/srv/images# cat /etc/apache2/sites-available/ks-server.conf** # в конфигурации веб-сервера добавим каталог /srv/ks идёнтично каталогу /srv/images
```bash
#Указываем IP-адрес хоста и порт на котором будет работать Web-сервер
<VirtualHost 10.0.77.182:80>
DocumentRoot /srv
Alias /ks /srv/ks
# Указываем директорию /srv/ks из которой будет загружаться параметры автоматической установки
<Directory /srv/ks>
Options Indexes MultiViews
AllowOverride All
Require all granted
</Directory>
Alias /images /srv/images
# Указываем директорию /srv/images из которой будет загружаться iso-образ
<Directory /srv/images>
Options Indexes MultiViews
AllowOverride All
Require all granted
</Directory>
</VirtualHost>
```
- **root@pxeserver:/srv/images# cat /srv/tftp/amd64/pxelinux.cfg/default** # добавляем параметры автоматической установки
```bash
DEFAULT install
LABEL install
  KERNEL linux
  INITRD initrd
  APPEND root=/dev/ram0 ramdisk_size=3000000 ip=dhcp iso-url=http://10.0.77.182/images/resolute-live-server-amd64.iso autoinstall ds=nocloud-net;s=http://10.0.77.182/ks/
```
- **root@pxeserver:/srv/images# systemctl restart dnsmasq** # перезагружаем dnsmasq
- **root@pxeserver:/srv/images# systemctl restart apache2** # перезагружаем apache2

### Проверяем автоматическую установку. Если в BIOS стоял первым HD (пустой, без boot) до PXE, то просто перезагрузка.
<img width="930" height="686" alt="Screenshot 2025-12-23 at 12 43 44" src="https://github.com/user-attachments/assets/ea40c6c0-7447-4519-ad9e-ccd217dd7a65" />

## 30-32 уроки 
## Фильтрация трафика - iptables/firewalld/nftable

**Домашнее задание** <ins>"Сценарии iptables"</ins>

**Цель**: Написать сценарии iptables;

🎯 Что нужно сделать?
- 1. реализовать knocking port (centralRouter может попасть на ssh inetrRouter через knock скрипт. Пример в материалах.)
- 2. добавить inetRouter2, который виден(маршрутизируется (host-only тип сети для виртуалки)) с хоста или форвардится порт через локалхост.
- запустить nginx на centralServer.
- пробросить 80й порт на inetRouter2 8080.
- дефолт в инет оставить через inetRouter.


Debian / Ubuntu
```bash
sudo apt update
sudo apt install knockd
```


```bash

```

</details>

- ## Выполнение
🔐 Что такое Port Knocking
- Port knocking — это способ скрыть открытый порт (например, SSH 22). Порт закрыт всегда, и открывается только после правильной последовательности обращений к другим портам.
- Пример: Клиент стучится: 7000 → 8000 → 9000  → сервер открывает порт 22 на 30 секунд

📦 Что понадобится
-	•	Linux-сервер
-	•	iptables или nftables
-	•	knockd (демон port knocking)
- ## 1.	
- **root@inetRouter:~# iptables -nvL** # чисто, ну и просмотрим другие таблицы (nat,raw..)
```bash
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
```
- **root@inetRouter:~# iptables -A INPUT -i lo -j ACCEPT** # регламентируем входной траффик, разрешим прохождение 
- **root@inetRouter:~# iptables -nvL** # проверим
```bash
Chain INPUT (policy ACCEPT 476 packets, 33958 bytes)
 pkts bytes target     prot opt in     out     source               destination
    0     0 ACCEPT     0    --  lo     *       0.0.0.0/0            0.0.0.0/0

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
```

- **root@inetRouter:~# iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT** # Разрешить только те пакеты, которые мы запросили
- **root@inetRouter:~# sudo apt update**
- **root@inetRouter:~# sudo apt install knockd** # Установка knockd
- **root@inetRouter:~# cat /etc/knockd.conf** # конфигурационный файл knockd
```bash
[options]
    logfile = /var/log/knockd.log

[openSSH]
    sequence    = 7000,8000,9000
    seq_timeout = 10
    command     = /sbin/iptables -I INPUT -s %IP% -p tcp --dport 22 -j ACCEPT
    timeout     = 30

[closeSSH]
    sequence    = 9000,8000,7000
    command     = /sbin/iptables -D INPUT -s %IP% -p tcp --dport 22 -j ACCEPT
```
-**root@inetRouter:~# ip -br a** # имена сетевых интерфейсов
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.182/24 metric 100 fe80::250:56ff:feb3:8745/64
```
- **oot@inetRouter:~# cat /etc/default/knockd** # настраиваем knock на интерфейс смотрящий в сеть откуда будем заходить
```bash 
# control if we start knockd at init or not
# 1 = start
# anything else = don't start
# PLEASE EDIT /etc/knockd.conf BEFORE ENABLING
START_KNOCKD=1

# command line options
KNOCKD_OPTS="-i ens192"
```
- **root@inetRouter:~# systemctl start knockd** #
- **root@inetRouter:~# systemctl status knockd** #
- **root@centralRouter:~# apt install knockd** #
- **root@inetRouter:~# iptables -nvL --line**
```bash
Chain INPUT (policy ACCEPT 4 packets, 1104 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        4   444 ACCEPT     0    --  lo     *       0.0.0.0/0            0.0.0.0/0
2        0     0 ACCEPT     1    --  *      *       0.0.0.0/0            0.0.0.0/0
3    64936 4665K ACCEPT     0    --  *      *       0.0.0.0/0            0.0.0.0/0            ctstate RELATED,ESTABLISHED

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 35458 packets, 3311K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        4   444 ACCEPT     0    --  *      lo      0.0.0.0/0            0.0.0.0/0
2       12   576 ACCEPT     1    --  *      *       0.0.0.0/0            0.0.0.0/0 
```
- **root@inetRouter:~# iptables -P INPUT DROP** # меняем политику INPUT на DROP
- **root@inetRouter:~# iptables-save** # сохраняеми видим результат
```bash
# Generated by iptables-save v1.8.10 (nf_tables) on Fri Dec 26 12:45:42 2025
*filter
:INPUT DROP [12:2873]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [36489:3403498]
-A INPUT -i lo -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A OUTPUT -o lo -j ACCEPT
-A OUTPUT -p icmp -j ACCEPT
COMMIT
# Completed on Fri Dec 26 12:45:42 2025
```
- **root@centralRouter:~# ssh spg@10.0.77.182** # ответа НЕТ (DROP)
- ^C
- **root@centralRouter:~# knock 10.0.77.182 7000 8000 9000** #  передаем через knock кодовую последовательность
- **root@centralRouter:~# ssh spg@10.0.77.182** # доступ открыт на время указанное в конфиге knock, закрыть можно обратной посл. указанной там же
```bash
spg@10.0.77.182's password:
Welcome to Ubuntu 24.04.3 LTS (GNU/Linux 6.8.0-90-generic x86_64
...
Last login: Fri Dec 26 12:27:42 2025 from 10.0.77.13
spg@inetRouter:~$
```
- **root@inetRouter:~# iptables -nvL --line**
```bash
Chain INPUT (policy DROP 151 packets, 30269 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1       23  5208 ACCEPT     6    --  *      *       10.0.77.186          0.0.0.0/0            tcp dpt:22
2        4   444 ACCEPT     0    --  lo     *       0.0.0.0/0            0.0.0.0/0
3        0     0 ACCEPT     1    --  *      *       0.0.0.0/0            0.0.0.0/0
4    67559 4849K ACCEPT     0    --  *      *       0.0.0.0/0            0.0.0.0/0            ctstate RELATED,ESTABLISHED
```
⚠️ Минусы port knocking
	•	Не шифрует трафик
	•	Возможны replay-атаки
	•	Может не работать за NAT (в редких случаях)

- ## 2.
- **root@inetRouter2:/etc# cat /etc/netplan/50-cloud-init.yaml** # сетевые настройки inetRouter2
```bash
network:
  version: 2
  ethernets:
    ens192:
      dhcp4: no
      addresses:
        - 10.0.77.182/24
      routes:
        - to: default
          via: 10.0.77.1
      nameservers:
        addresses: [10.0.1.167, 10.0.1.194]

    ens224:
      dhcp4: no
      addresses:
        - 192.168.0.1/28
```  
- **root@inetRouter2:/etc# iptables -nvL** # конфигурация чиста, Firewall-а тоже нет (systemctl status ufw)
```bash
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
```
- **root@inetRouter2:/etc# cat /etc/sysctl.conf** # раскомментируем форвардинг на уровне ядра 
```bash
# Uncomment the next line to enable packet forwarding for IPv4
net.ipv4.ip_forward=1
```
- **root@inetRouter2:/etc# sudo sysctl -p** # перечитывает параметры из /etc/sysctl.conf и применяет их сразу, без перезагрузки
- net.ipv4.ip_forward = 1
- **root@inetRouter2:/etc# cat /proc/sys/net/ipv4/ip_forward** # показывает текущее значение параметра форвардинга
- 1

- **root@CentralServer:~# cat /etc/netplan/00-installer-config.yaml** # сетевые настройки на CentralServer
```bash
network:
  version: 2
  ethernets:
    ens192:
      dhcp4: no
      addresses:
        - 192.168.0.2/28
      routes:
        - to: default
          via: 192.168.0.1
      nameservers:
        addresses: [192.168.0.1, 8.8.8.8]
```
- **root@CentralServer:~# netplan generate** # проверка и генерация конфигурации
- **root@CentralServer:~# netplan apply** # применение конфигурации
- **root@CentralServer:~# ping ya.ru** # проверка неудачная
ping: ya.ru: Temporary failure in name resolution
- **oot@CentralServer:~# ping 8.8.8.8** # проверка неудачная
ping: connect: Network is unreachable
- **root@CentralServer:~# ping 192.168.0.1** # связь с роутером есть
```bash
PING 192.168.0.1 (192.168.0.1) 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=64 time=0.059 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=64 time=0.052 ms
```
- **root@inetRouter2:/etc# sudo iptables -t nat -A PREROUTING -p tcp --dport 9022 -j DNAT --to 192.168.0.2:22** # настраиваем проброс порта роутера (9022)  на порт сервера (22)
- **~ ssh -p 9022 spg@10.0.77.182** # Пока не можем подключться
```bash
ssh: connect to host 10.0.77.182 port 9022: Operation timed out
```
- **root@inetRouter2:/etc# iptables -t nat -A POSTROUTING -o ens224 -j MASQUERADE** # настраиваем NAT
- **root@inetRouter2:/etc# sudo iptables -A FORWARD -i ens224 -o ens192 -j ACCEPT** # команда нужна для маршрутизации трафика из LAN в WAN
- **root@inetRouter2:/etc# sudo iptables -A FORWARD -i ens192 -o ens224 -m state --state RELATED,ESTABLISHED -j ACCEPT** # Разрешает пакеты, которые относятся к уже установленным соединениям (ответы из интернета)
- **~ssh -p 9022 spg@10.0.77.182** # Удачная попытка соединения с хостовой машины по ssh с сервером через роутер (9022)
```bash
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[10.0.77.182]:9022' (ED25519) to the list of known hosts.
spg@10.0.77.182's password:
```
- **root@CentralServer:~# ping ya.ru** # # и трафик пошел наружу
```bash
PING ya.ru (77.88.44.242) 56(84) bytes of data.
64 bytes from ya.ru (77.88.44.242): icmp_seq=1 ttl=56 time=3.60 ms
64 bytes from ya.ru (77.88.44.242): icmp_seq=2 ttl=56 time=3.34 ms
```
- **root@CentralServer:~# sudo apt update** #
- **sudo apt install -y nginx** #
- **root@CentralServer:~# sudo systemctl status nginx**
```bash
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: active (running) since Mon 2025-12-29 12:42:28 UTC; 9s ago
```
- **root@CentralServer:~# cat /var/www/html/index.nginx-debian.html** # Для наглядности изменим корневую страничку на "Welcome to CentralServer"
```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CentralServer</title>
</head>
<body>
    <h1>Welcome to CentralServer</h1>
</body>
</html>
```
- **root@inetRouter2:/etc# sudo iptables -t nat -A PREROUTING -p tcp --dport 8080 -j DNAT --to 192.168.0.2:80** # настраиваем проброс порта роутера (8080)  на порт сервера (80)
- **root@inetRouter2:/etc# iptables-save** # сохраняем и проверяем конфигурацию iptables
```bash
# Generated by iptables-save v1.8.10 (nf_tables) on Mon Dec 29 12:46:20 2025
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [1:64]
:OUTPUT ACCEPT [0:0]
-A FORWARD -i ens224 -o ens192 -j ACCEPT
-A FORWARD -i ens192 -o ens224 -m state --state RELATED,ESTABLISHED -j ACCEPT
COMMIT
# Completed on Mon Dec 29 12:46:20 2025
# Generated by iptables-save v1.8.10 (nf_tables) on Mon Dec 29 12:46:20 2025
*nat
:PREROUTING ACCEPT [5666:1202021]
:INPUT ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:POSTROUTING ACCEPT [72:9196]
-A PREROUTING -p tcp -m tcp --dport 9022 -j DNAT --to-destination 192.168.0.2:22
-A PREROUTING -p tcp -m tcp --dport 8080 -j DNAT --to-destination 192.168.0.2:80
-A POSTROUTING -o ens192 -j MASQUERADE
COMMIT
# Completed on Mon Dec 29 12:46:20 2025
```
### Проверяем доступность страницы центрального сервера через проброс порта (8080 -> 80) с маршрутизатора inetRouter2
<img width="1091" height="228" alt="Screenshot 2025-12-29 at 15 48 44" src="https://github.com/user-attachments/assets/380f0197-cad0-43db-bf6b-9b1a808acc2f" />

## 33 урок 
## Статическая и динамическая маршрутизация, OSPF

**Домашнее задание** <ins>"OSPF"</ins>

**Цель**: отличать unicast, broadcast и multicast;
понять принцип работы протокола динамической маршрутизации OSPF;
настроить роутинг на хосте с помощью FRR;

🎯 Что нужно сделать?
- **Создать домашнюю сетевую лабораторию. Научится настраивать протокол OSPF в Linux-based системах.**
- 1. Развернуть 3 виртуальные машины
- 2. Объединить их разными vlan
- настроить OSPF между машинами на базе FRR;
- изобразить ассиметричный роутинг;
- сделать один из линков "дорогим", но что бы при этом роутинг был симметричным.
- **Развернем три машины linux c OC Ubuntu 24.04 c 3-мя сетевыми интерфейсами**
<img width="888" height="663" alt="Screenshot 2026-01-21 at 09 03 10" src="https://github.com/user-attachments/assets/e8745723-6571-4d4b-90f4-b6c480462820" />

- **Router1 DZ33**
- **root@router1:~# cat /etc/netplan/50-cloud-init.yaml**
```bash
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: no
      addresses:
        - 192.168.10.1/24

    ens224:
      dhcp4: no
      addresses:
        - 10.0.10.1/30

    ens256:
      dhcp4: no
      addresses:
        - 10.0.12.1/30
```
- **Router2 DZ33**
- **root@router2:~# cat /etc/netplan/50-cloud-init.yaml**
```bash
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: no
      addresses:
        - 192.168.20.1/24

    ens224:
      dhcp4: no
      addresses:
        - 10.0.10.2/30

    ens256:
      dhcp4: no
      addresses:
        - 10.0.11.2/30
```
- **Router3 DZ33**
- **root@router3:~# cat /etc/netplan/50-cloud-init.yaml**
```bash
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: no
      addresses:
        - 192.168.30.1/24

    ens224:
      dhcp4: no
      addresses:
        - 10.0.12.2/30

    ens256:
      dhcp4: no
      addresses:
        - 10.0.11.1/30
```
- **Для установки  пакетов для тестирования и настройки OSPF на всех роутерах добавил один интерфейс смотрящий в Инет**

- **Поставил базовые программы для изменения конфигурационных файлов (vim) и изучения сети (traceroute, tcpdump, net-tools):**
- **root@router123# apt update**
- **root@router123# apt install vim traceroute tcpdump net-tools**

- **Убрал у всех четвертый интерфейс** # ens161
- **root@router123# systemctl stop ufw** 
- **root@router123# systemctl disable ufw** # отключил на всех роутерах firewall
- **root@router123# curl -s https://deb.frrouting.org/frr/keys.asc | sudo apt-key add -** #добавляем gpg ключ
- **root@router123# echo deb https://deb.frrouting.org/frr $(lsb_release -s -c) frr-stable > /etc/apt/sources.list.d/frr.list**
- **root@router123# sudo apt update** 
- **root@router123# sudo apt install frr frr-pythontools** # Обновляем пакеты и устанавливаем FRR
- **root@router123# sysctl net.ipv4.conf.all.forwarding=1** # Разрешаем (включаем) маршрутизацию транзитных пакетов
- **root@router123:~# cat /etc/frr/daemons** # Включаем демон ospfd в FRR
```bash
bgpd=no
zebra=yes
ospfd=yes
ospf6d=no
ripd=no
ripngd=no
isisd=no
pimd=no
pim6d=no
ldpd=no
nhrpd=no
eigrpd=no
babeld=no
sharpd=no
pbrd=no
bfdd=no
fabricd=no
vrrpd=no
pathd=no

#
# If this option is set the /etc/init.d/frr script automatically loads
# the config via "vtysh -b" when the servers are started.
# Check /etc/pam.d/frr if you intend to use "vtysh"!
#
vtysh_enable=yes
```

- ###Настройка OSPF
- **Узнать имена интерфейсов и их адреса**
- **root@router1:~# ip -br a**
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             192.168.10.1/24 fe80::250:56ff:feb3:7658/64
ens224           UP             10.0.10.1/30 fe80::250:56ff:feb3:a17f/64
ens256           UP             10.0.12.1/30 fe80::250:56ff:feb3:8cca/64
```
**root@router1:~# ip a | grep "inet"** 
```bash
    inet 127.0.0.1/8 scope host lo
    inet6 ::1/128 scope host noprefixroute
    inet 192.168.10.1/24 brd 192.168.10.255 scope global ens192
    inet6 fe80::250:56ff:feb3:7658/64 scope link
    inet 10.0.10.1/30 brd 10.0.10.3 scope global ens224
    inet6 fe80::250:56ff:feb3:a17f/64 scope link
    inet 10.0.12.1/30 brd 10.0.12.3 scope global ens256
    inet6 fe80::250:56ff:feb3:8cca/64 scope link
```
- **Из интерфейса FRR**
- **root@router1:~# vtysh**
```bash
Hello, this is FRRouting (version 10.5.1).
Copyright 1996-2005 Kunihiro Ishiguro, et al.
```
- **router1# show interface brief**
```bash
Interface       Status  VRF             Addresses
---------       ------  ---             ---------
ens192          up      default         192.168.10.1/24
                                        fe80::250:56ff:feb3:7658/64
ens224          up      default         10.0.10.1/30
                                        fe80::250:56ff:feb3:a17f/64
ens256          up      default         10.0.12.1/30
                                        fe80::250:56ff:feb3:8cca/64
lo              up      default
```
- **router1# exit** # выходим
- **root@router1:~#**
- 
- **root@router1:~# cat /etc/frr/frr.conf** # Правим конфиг frr
```bash
# default to using syslog. /etc/rsyslog.d/45-frr.conf places the log in
# /var/log/frr/frr.log
#
# Note:
# FRR's configuration shell, vtysh, dynamically edits the live, in-memory
# configuration while FRR is running. When instructed, vtysh will persist the
# live configuration to this file, overwriting its contents. If you want to
# avoid this, you can edit this file manually before starting FRR, or instruct
# vtysh to write configuration to a different file.
!Указание версии FRR
frr version 10.5.1
frr defaults traditional
!Указываем имя машины
hostname router1
log syslog informational
no ipv6 forwarding
service integrated-vtysh-config
!
!Добавляем информацию об интерфейсе enp0s8
interface ens224
 !Указываем имя интерфейса
 description r1-r2
 !Указываем ip-aдрес и маску (эту информацию мы получили в прошлом шаге)
 ip address 10.0.10.1/30
 !Указываем параметр игнорирования MTU
 ip ospf mtu-ignore
 !Если потребуется, можно указать «стоимость» интерфейса
 !ip ospf cost 1000
 !Указываем параметры hello-интервала для OSPF пакетов
 ip ospf hello-interval 10
 !Указываем параметры dead-интервала для OSPF пакетов
 !Должно быть кратно предыдущему значению
 ip ospf dead-interval 30
!
interface ens256
 description r1-r3
 ip address 10.0.12.1/30
 ip ospf mtu-ignore
 !ip ospf cost 45
 ip ospf hello-interval 10
 ip ospf dead-interval 30

interface ens192
 description net_router1
 ip address 192.168.10.1/24
 ip ospf mtu-ignore
 !ip ospf cost 45
 ip ospf hello-interval 10
 ip ospf dead-interval 30
!
!Начало настройки OSPF
router ospf
 !Указываем router-id
 router-id 1.1.1.1
 !Указываем сети, которые хотим анонсировать соседним роутерам
 network 10.0.10.0/30 area 0
 network 10.0.12.0/30 area 0
 network 192.168.10.0/24 area 0
 !Указываем адреса соседних роутеров
 neighbor 10.0.10.2
 neighbor 10.0.12.2

!Указываем адрес log-файла
log file /var/log/frr/frr.log
default-information originate always

log syslog informational
```
- **root@router2:~# cat /etc/frr/frr.conf** # Правим конфиг frr
```bash
# default to using syslog. /etc/rsyslog.d/45-frr.conf places the log in
# /var/log/frr/frr.log
#
# Note:
# FRR's configuration shell, vtysh, dynamically edits the live, in-memory
# configuration while FRR is running. When instructed, vtysh will persist the
# live configuration to this file, overwriting its contents. If you want to
# avoid this, you can edit this file manually before starting FRR, or instruct
# vtysh to write configuration to a different file.
!Указание версии FRR
frr version 10.5.1
frr defaults traditional
!Указываем имя машины
hostname router2
log syslog informational
no ipv6 forwarding
service integrated-vtysh-config
!
!Добавляем информацию об интерфейсе enp0s8
interface ens224
 !Указываем имя интерфейса
 description r2-r1
 !Указываем ip-aдрес и маску (эту информацию мы получили в прошлом шаге)
 ip address 10.0.10.2/30
 !Указываем параметр игнорирования MTU
 ip ospf mtu-ignore
 !Если потребуется, можно указать «стоимость» интерфейса
 !ip ospf cost 1000
 !Указываем параметры hello-интервала для OSPF пакетов
 ip ospf hello-interval 10
 !Указываем параметры dead-интервала для OSPF пакетов
 !Должно быть кратно предыдущему значению
 ip ospf dead-interval 30
!
interface ens256
 description r2-r3
 ip address 10.0.11.2/30
 ip ospf mtu-ignore
 !ip ospf cost 45
 ip ospf hello-interval 10
 ip ospf dead-interval 30

interface ens192
 description net_router2
 ip address 192.168.20.1/24
 ip ospf mtu-ignore
 !ip ospf cost 45
 ip ospf hello-interval 10
 ip ospf dead-interval 30
!
!Начало настройки OSPF
router ospf
 !Указываем router-id
 router-id 2.2.2.2
 !Указываем сети, которые хотим анонсировать соседним роутерам
 network 10.0.10.0/30 area 0
 network 10.0.11.0/30 area 0
 network 192.168.20.0/24 area 0
 !Указываем адреса соседних роутеров
 neighbor 10.0.10.1
 neighbor 10.0.11.1

!Указываем адрес log-файла
log file /var/log/frr/frr.log
default-information originate always

log syslog informational
```
- **root@router3:~# cat /etc/frr/frr.conf** # Правим конфиг frr
```bash
# default to using syslog. /etc/rsyslog.d/45-frr.conf places the log in
# /var/log/frr/frr.log
#
# Note:
# FRR's configuration shell, vtysh, dynamically edits the live, in-memory
# configuration while FRR is running. When instructed, vtysh will persist the
# live configuration to this file, overwriting its contents. If you want to
# avoid this, you can edit this file manually before starting FRR, or instruct
# vtysh to write configuration to a different file.
!Указание версии FRR
frr version 10.5.1
frr defaults traditional
!Указываем имя машины
hostname router3
log syslog informational
no ipv6 forwarding
service integrated-vtysh-config
!
!Добавляем информацию об интерфейсе enp0s8
interface ens224
 !Указываем имя интерфейса
 description r3-r1
 !Указываем ip-aдрес и маску (эту информацию мы получили в прошлом шаге)
 ip address 10.0.12.2/30
 !Указываем параметр игнорирования MTU
 ip ospf mtu-ignore
 !Если потребуется, можно указать «стоимость» интерфейса
 !ip ospf cost 1000
 !Указываем параметры hello-интервала для OSPF пакетов
 ip ospf hello-interval 10
 !Указываем параметры dead-интервала для OSPF пакетов
 !Должно быть кратно предыдущему значению
 ip ospf dead-interval 30
!
interface ens256
 description r3-r2
 ip address 10.0.11.1/30
 ip ospf mtu-ignore
 !ip ospf cost 45
 ip ospf hello-interval 10
 ip ospf dead-interval 30

interface ens192
 description net_router3
 ip address 192.168.30.1/24
 ip ospf mtu-ignore
 !ip ospf cost 45
 ip ospf hello-interval 10
 ip ospf dead-interval 30
!
!Начало настройки OSPF
router ospf
 !Указываем router-id
 router-id 3.3.3.3
 !Указываем сети, которые хотим анонсировать соседним роутерам
 network 10.0.12.0/30 area 0
 network 10.0.11.0/30 area 0
 network 192.168.30.0/24 area 0
 !Указываем адреса соседних роутеров
 neighbor 10.0.12.1
 neighbor 10.0.11.2

!Указываем адрес log-файла
log file /var/log/frr/frr.log
default-information originate always

log syslog informational
```
- **root@router123:~# ls -l /etc/frr** # проверяем права
```bash
total 28
-rw-r----- 1 frr frr 4138 Jan 16 13:36 daemons
-rw-r----- 1 frr frr 2389 Jan 20 11:09 frr.conf
-rw-r----- 1 frr frr 8667 Jan  6 14:40 support_bundle_commands.conf
-rw-r----- 1 frr frr   32 Jan  6 14:40 vtysh.conf
```

- **root@router123:~# systemctl restart frr** # Перезапускаем FRR и 
- **root@router123:~# systemctl enable  frr** # добавляем его в автозагрузку
- **root@router123:~# systemctl status  frr** # проверяем
```bash
● frr.service - FRRouting
     Loaded: loaded (/usr/lib/systemd/system/frr.service; enabled; preset: enabled)
     Active: active (running) since Mon 2026-01-19 13:22:19 UTC; 6min ago
```
### Проверим как работает...

```bash
root@router1:~# ping 192.168.10.1
PING 192.168.10.1 (192.168.10.1) 56(84) bytes of data.
64 bytes from 192.168.10.1: icmp_seq=1 ttl=64 time=0.017 ms
64 bytes from 192.168.10.1: icmp_seq=2 ttl=64 time=0.015 ms
^C
--- 192.168.10.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1048ms
rtt min/avg/max/mdev = 0.015/0.016/0.017/0.001 ms
root@router1:~# ping 192.168.20.1
PING 192.168.20.1 (192.168.20.1) 56(84) bytes of data.
64 bytes from 192.168.20.1: icmp_seq=1 ttl=64 time=0.080 ms
^C
--- 192.168.20.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.080/0.080/0.080/0.000 ms
root@router1:~# ping 192.168.30.1
PING 192.168.30.1 (192.168.30.1) 56(84) bytes of data.
64 bytes from 192.168.30.1: icmp_seq=1 ttl=64 time=0.099 ms
64 bytes from 192.168.30.1: icmp_seq=2 ttl=64 time=0.105 ms
^C
--- 192.168.30.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1042ms
rtt min/avg/max/mdev = 0.099/0.102/0.105/0.003 ms
```
```bash
root@router2:~# ping 192.168.10.1
PING 192.168.10.1 (192.168.10.1) 56(84) bytes of data.
64 bytes from 192.168.10.1: icmp_seq=1 ttl=64 time=0.093 ms
^C
--- 192.168.10.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.093/0.093/0.093/0.000 ms
root@router2:~# ping 192.168.20.1
PING 192.168.20.1 (192.168.20.1) 56(84) bytes of data.
64 bytes from 192.168.20.1: icmp_seq=1 ttl=64 time=0.013 ms
64 bytes from 192.168.20.1: icmp_seq=2 ttl=64 time=0.012 ms
^C
--- 192.168.20.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1006ms
rtt min/avg/max/mdev = 0.012/0.012/0.013/0.000 ms
root@router2:~# ping 192.168.30.1
PING 192.168.30.1 (192.168.30.1) 56(84) bytes of data.
64 bytes from 192.168.30.1: icmp_seq=1 ttl=64 time=0.111 ms
^C
--- 192.168.30.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.111/0.111/0.111/0.000 ms
```
```bash
root@router3:~# ping 192.168.30.1
PING 192.168.30.1 (192.168.30.1) 56(84) bytes of data.
64 bytes from 192.168.30.1: icmp_seq=1 ttl=64 time=0.016 ms
64 bytes from 192.168.30.1: icmp_seq=2 ttl=64 time=0.020 ms
^C
--- 192.168.30.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1037ms
rtt min/avg/max/mdev = 0.016/0.018/0.020/0.002 ms
root@router3:~# ping 192.168.20.1
PING 192.168.20.1 (192.168.20.1) 56(84) bytes of data.
64 bytes from 192.168.20.1: icmp_seq=1 ttl=64 time=0.076 ms
64 bytes from 192.168.20.1: icmp_seq=2 ttl=64 time=0.085 ms
^C
--- 192.168.20.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1006ms
rtt min/avg/max/mdev = 0.076/0.080/0.085/0.004 ms
root@router3:~# ping 192.168.10.1
PING 192.168.10.1 (192.168.10.1) 56(84) bytes of data.
64 bytes from 192.168.10.1: icmp_seq=1 ttl=64 time=0.094 ms
64 bytes from 192.168.10.1: icmp_seq=2 ttl=64 time=0.089 ms
^C
--- 192.168.10.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1038ms
rtt min/avg/max/mdev = 0.089/0.091/0.094/0.002 ms
```
- **root@router1:~# traceroute  192.168.30.1** # трассировка с роутера1 во внутреннюю сеть роутера3
```bash
traceroute to 192.168.30.1 (192.168.30.1), 30 hops max, 60 byte packets
 1  192.168.30.1 (192.168.30.1)  0.096 ms  0.093 ms  0.079 ms
```
- **root@router1:~# vtysh**
- **router1# sh ip route ospf** # посмотрим маршруты OSPF
```bash
Codes: K - kernel route, C - connected, L - local, S - static,
       R - RIP, O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
       T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
       f - OpenFabric, t - Table-Direct,
       > - selected route, * - FIB route, q - queued, r - rejected, b - backup
       t - trapped, o - offload failure

IPv4 unicast VRF default:
O   10.0.10.0/30 [110/10] is directly connected, ens224, weight 1, 00:26:58
O>* 10.0.11.0/30 [110/20] via 10.0.10.2, ens224, weight 1, 00:24:38
  *                       via 10.0.12.2, ens256, weight 1, 00:24:38
O   10.0.12.0/30 [110/10] is directly connected, ens256, weight 1, 00:24:49
O   192.168.10.0/24 [110/10] is directly connected, ens192, weight 1, 00:27:29
O>* 192.168.20.0/24 [110/20] via 10.0.10.2, ens224, weight 1, 00:26:56
O>* 192.168.30.0/24 [110/20] via 10.0.12.2, ens256, weight 1, 00:24:38
```
- **root@router1:~# ifconfig ens256 down** # выключим интерфейс на роутере1 смотрящий на роутер3
-  ### и повторим проверку доступности внутренней сети роутера 3
```bash
root@router1:~# ping 192.168.30.1
PING 192.168.30.1 (192.168.30.1) 56(84) bytes of data.
64 bytes from 192.168.30.1: icmp_seq=1 ttl=63 time=0.168 ms
64 bytes from 192.168.30.1: icmp_seq=2 ttl=63 time=0.151 ms
^C
--- 192.168.30.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1058ms
rtt min/avg/max/mdev = 0.151/0.159/0.168/0.008 ms
root@router1:~# traceroute 192.168.30.1
traceroute to 192.168.30.1 (192.168.30.1), 30 hops max, 60 byte packets
 1  10.0.10.2 (10.0.10.2)  0.098 ms  0.072 ms  0.065 ms
 2  192.168.30.1 (192.168.30.1)  0.149 ms  0.159 ms  0.146 ms
root@router1:~# vtysh

Hello, this is FRRouting (version 10.5.1).
Copyright 1996-2005 Kunihiro Ishiguro, et al.

router1# sh ip route ospf
Codes: K - kernel route, C - connected, L - local, S - static,
       R - RIP, O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
       T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
       f - OpenFabric, t - Table-Direct,
       > - selected route, * - FIB route, q - queued, r - rejected, b - backup
       t - trapped, o - offload failure

IPv4 unicast VRF default:
O   10.0.10.0/30 [110/10] is directly connected, ens224, weight 1, 00:35:11
O>* 10.0.11.0/30 [110/20] via 10.0.10.2, ens224, weight 1, 00:03:32
                          via 10.0.12.2, ens256 inactive, weight 1, 00:03:32
O>* 10.0.12.0/30 [110/30] via 10.0.10.2, ens224, weight 1, 00:03:12
O   192.168.10.0/24 [110/10] is directly connected, ens192, weight 1, 00:35:42
O>* 192.168.20.0/24 [110/20] via 10.0.10.2, ens224, weight 1, 00:35:09
O>* 192.168.30.0/24 [110/30] via 10.0.10.2, ens224, weight 1, 00:03:32
```
- **root@router1:~# ifconfig ens256 up**

  
- ## Настройка ассиметричного роутинга
- **root@router123:~# sysctl net.ipv4.conf.all.rp_filter=0** # для реализации ассиметричного роутинга отключаем rp_filter — защита от IP-spoofing
- net.ipv4.conf.all.rp_filter = 0
- ### поменяем стоимость интерфейса ens224 на router1
```bash
root@router1:~# vtysh

Hello, this is FRRouting (version 10.5.1).
Copyright 1996-2005 Kunihiro Ishiguro, et al.

router1# conf t
router1(config)# int ens224
router1(config-if)# ip ospf cost 1000
router1(config-if)# exit
router1(config)# exit
router1# sh ip route ospf
Codes: K - kernel route, C - connected, L - local, S - static,
       R - RIP, O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
       T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
       f - OpenFabric, t - Table-Direct,
       > - selected route, * - FIB route, q - queued, r - rejected, b - backup
       t - trapped, o - offload failure

IPv4 unicast VRF default:
O   10.0.10.0/30 [110/30] via 10.0.12.2, ens256, weight 1, 00:01:08
O>* 10.0.11.0/30 [110/20] via 10.0.12.2, ens256, weight 1, 00:01:08
O   10.0.12.0/30 [110/10] is directly connected, ens256, weight 1, 1d16h58m
O   192.168.10.0/24 [110/10] is directly connected, ens192, weight 1, 1d17h39m
O>* 192.168.20.0/24 [110/30] via 10.0.12.2, ens256, weight 1, 00:01:08
O>* 192.168.30.0/24 [110/20] via 10.0.12.2, ens256, weight 1, 1d16h58m
```
```bash
root@router2:~# vtysh

Hello, this is FRRouting (version 10.5.1).
Copyright 1996-2005 Kunihiro Ishiguro, et al.

router2# show ip route ospf
Codes: K - kernel route, C - connected, L - local, S - static,
       R - RIP, O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
       T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
       f - OpenFabric, t - Table-Direct,
       > - selected route, * - FIB route, q - queued, r - rejected, b - backup
       t - trapped, o - offload failure

IPv4 unicast VRF default:
O   10.0.10.0/30 [110/10] is directly connected, ens224, weight 1, 1d17h43m
O   10.0.11.0/30 [110/10] is directly connected, ens256, weight 1, 1d17h40m
O>* 10.0.12.0/30 [110/20] via 10.0.10.1, ens224, weight 1, 1d17h02m
  *                       via 10.0.11.1, ens256, weight 1, 1d17h02m
O>* 192.168.10.0/24 [110/20] via 10.0.10.1, ens224, weight 1, 1d17h42m
O   192.168.20.0/24 [110/10] is directly connected, ens192, weight 1, 1d17h43m
O>* 192.168.30.0/24 [110/20] via 10.0.11.1, ens256, weight 1, 1d17h40m
```
- ### Видим, что маршрут от Router1 до сети 192.168.20.0/24 теперь пойдет через Router3 (via 10.0.12.2, ens256), но маршрут от Router2 в сеть 192.168.10.0/24 пойдет сразу на Router1 (via 10.0.10.1, ens224)
- **root@router1:~# ping -I 192.168.10.1192.168.20.1** # запускаем ping от интерфейса внутренней сети Router1  на адрес интерфейса внутренней сети Riuter2
```bash
PING 192.168.20.1 (192.168.20.1) from 192.168.10.1 : 56(84) bytes of data.
64 bytes from 192.168.20.1: icmp_seq=1 ttl=64 time=0.114 ms
64 bytes from 192.168.20.1: icmp_seq=2 ttl=64 time=0.116 ms
...
```
- **root@router2:~# tcpdump -i ens256** # Видим, что пакеты ICMP приходят на интерфейс Router2 смотрящего на Router3 (то есть по более длинному, но менее дорогому для Router1 маршруту)
```bash
...
06:42:20.094800 IP 192.168.10.1 > router2: ICMP echo request, id 18317, seq 44, length 64
06:42:21.118789 IP 192.168.10.1 > router2: ICMP echo request, id 18317, seq 45, length 64
06:42:22.142742 IP 192.168.10.1 > router2: ICMP echo request, id 18317, seq 46, length 64
```
- **root@router2:~# tcpdump -i ens224** # Видим, что  ответные пакеты ICMP выходят с интерфейс Router2 смотрящего на Router1 (то есть по кратчайшему до Router1 маршруту)
```bash
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on ens224, link-type EN10MB (Ethernet), snapshot length 262144 bytes
06:41:44.255895 IP router2 > 192.168.10.1: ICMP echo reply, id 18317, seq 9, length 64
```

- ## Настройка симметичного роутинга
- ### Чтобы сделать симитричный роутинг для нашего примера, сделаем ответный маршрут Router2 -> Router1  из предыдущего пункта дорогим и заставим его отправлять пакетв по тому же маршруту, по которому он их получает от Router1 (через Router3):
```bash
root@router2:~# tvysh
Command 'tvysh' not found, did you mean:
  command 'vtysh' from deb frr (8.4.4-1.1ubuntu6.3)
Try: apt install <deb name>
root@router2:~# vtysh

Hello, this is FRRouting (version 10.5.1).
Copyright 1996-2005 Kunihiro Ishiguro, et al.

router2# conf t
router2(config)# int ens224
router2(config-if)# ip ospf cost 1000
router2(config-if)# exit
router2(config)# exit
router2# show ip route ospf
Codes: K - kernel route, C - connected, L - local, S - static,
       R - RIP, O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
       T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
       f - OpenFabric, t - Table-Direct,
       > - selected route, * - FIB route, q - queued, r - rejected, b - backup
       t - trapped, o - offload failure

IPv4 unicast VRF default:
O   10.0.10.0/30 [110/1000] is directly connected, ens224, weight 1, 00:00:25
O   10.0.11.0/30 [110/10] is directly connected, ens256, weight 1, 1d21h58m
O>* 10.0.12.0/30 [110/20] via 10.0.11.1, ens256, weight 1, 00:00:25
O>* 192.168.10.0/24 [110/30] via 10.0.11.1, ens256, weight 1, 00:00:25
O   192.168.20.0/24 [110/10] is directly connected, ens192, weight 1, 1d22h00m
O>* 192.168.30.0/24 [110/20] via 10.0.11.1, ens256, weight 1, 1d21h57m
```
### видим, что маршрут до внутренней сети Router1 (192.168.10.0/24) теперь идет через Router3 (10.0.1.11)
### Проверка:
- **root@router1:~# ping -I 192.168.10.1 192.168.20.1**
```bash
PING 192.168.20.1 (192.168.20.1) from 192.168.10.1 : 56(84) bytes of data.
64 bytes from 192.168.20.1: icmp_seq=1 ttl=63 time=0.154 ms
64 bytes from 192.168.20.1: icmp_seq=2 ttl=63 time=0.134 ms
```
- **root@router2:~# tcpdump -i ens256** # Теперь и запрос и ответ идут через один маршрут
```bash
10:28:17.259046 IP 192.168.10.1 > router2: ICMP echo request, id 20201, seq 24, length 64
10:28:17.259055 IP router2 > 192.168.10.1: ICMP echo reply, id 20201, seq 24, length 64
10:28:18.283037 IP 192.168.10.1 > router2: ICMP echo request, id 20201, seq 25, length 64
10:28:18.283049 IP router2 > 192.168.10.1: ICMP echo reply, id 20201, seq 25, length 64
```
## 33 урок 
## Сетевые пакеты. VLAN'ы. LACP


**Домашнее задание** <ins>"Строим бонды и вланы"</ins>

**Цель**: Научиться настраивать VLAN и LACP;

🎯 Что нужно сделать?
- **Создать домашнюю сетевую лабораторию. Научится настраивать протокол OSPF в Linux-based системах.**
- Что нужно сделать?
- в Office1 в тестовой подсети появляется сервера с доп интерфейсами и адресами
в internal сети testLAN:

- testClient1 - 10.10.10.254
- testClient2 - 10.10.10.254
- testServer1- 10.10.10.1
- testServer2- 10.10.10.1
- Равести вланами:
- testClient1 <-> testServer1
- testClient2 <-> testServer2

- Между centralRouter и inetRouter "пробросить" 2 линка (общая inernal сеть) и объединить их в бонд, проверить работу c отключением интерфейсов
- ## Выполнение
- Развернем на Vcenter 7 машин:
  <img width="1093" height="497" alt="Screenshot 2026-01-27 at 16 32 29" src="https://github.com/user-attachments/assets/5b508ec9-a222-4b7d-9e52-156575369886" />
- ### Дана следующая схема для ДЗ:

<img width="824" height="810" alt="image" src="https://github.com/user-attachments/assets/5fe8e4e4-9338-4ced-9703-9703b49c4277" />

- ### Топология представленной сети  и ДЗ не предпологают vlan фильтрацию на хосте office1Router. Поэтому я заменю его на виртуальный коммутатор portgroup trunking в "VMware vSphere" (с помощью которой делаю ДЗ) для того, чтобы пропускать VLAN-теги (разрешен весь диапазон VLAN-ов). К нему подключу только интерфейсы ens224. Интерфейсы ens192 подключены через коммутатор в режиме access к моей рабочей сети, стобы легче было получить доступ к каждой ВМ по ssh (не через консоль, откуда сложно копировать резeльтаты работы в Github)
- ### Схема теперь выглядит так:
<img width="819" height="800" alt="Screenshot 2026-01-28 at 10 48 30" src="https://github.com/user-attachments/assets/30521413-33d1-413b-a9e4-b41515808365" />



- **root@*******:~# apt install -y vim traceroute tcpdump net-tools**
- **root@*******:~# cat /etc/netplan/50-cloud-init.yaml**
```bash
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: true 

    ens224:
      dhcp4: no
      addresses:
        - 10.10.10.1/24 # для testServer1 testServer2
    или
        - 10.10.10.254/24 # для testClient1 testClient2
```
- **root@*******:~# ip -br a** # на всех 4-х машинах пока одинаково за исключением адреса управления
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.*/24 metric 100 fe80::250:56ff:feb3:7658/64
ens224           DOWN             10.10.10.254/24 fe80::250:56ff:feb3:1666/64
```

- **root@*******:~# ip link set dev ens224 up**  # на всех 4-х машинах пока одинаково
- 
- ### Создание VLAN-интерфейсов
- 
- **root@testclient1:~# ip link add link ens224 name ens224.10 type vlan id 10**
- **root@testclient1:~# ip addr add 10.10.10.254/24 dev ens224.10**
- **root@testclient1:~# ip link set dev ens224.10 up**
- 
- **root@testserver1:~# ip link add link ens224 name ens224.10 type vlan id 10**
- **root@testserver1:~# ip addr add 10.10.10.1/24 dev ens224.10**
- **root@testserver1:~# ip link set dev ens224.10 up**
- 
- **root@testclient2:~# ip link add link ens224 name ens224.20 type vlan id 20**
- **root@testclient2:~# ip addr add 10.10.10.254/24 dev ens224.20**
- **root@testclient2:~# ip link set dev ens224.20 up**
- 
- **root@testserver2:~# ip link add link ens224 name ens224.20 type vlan id 20**
- **root@testserver2:~# ip addr add 10.10.10.1/24 dev ens224.20**
- **root@testserver2:~# ip link set dev ens224.20 up**


- **root@testclient1:~# ip -br a**
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.156/24 metric 100 fe80::250:56ff:feb3:8557/64
ens224           UP
ens224.10@ens224 UP             10.10.10.254/24 fe80::250:56ff:feb3:42a3/64
```
- **root@testserver1:~# ip -br a**
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.186/24 metric 100 fe80::250:56ff:feb3:7ee8/64
ens224           UP             fe80::250:56ff:feb3:a62/64
ens224.10@ens224 UP             10.10.10.1/24 fe80::250:56ff:feb3:a62/64
```
- **root@testclient2:~# ip -br a**
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.170/24 metric 100 fe80::250:56ff:feb3:7658/64
ens224           UP
ens224.20@ens224 UP             10.10.10.254/24 fe80::250:56ff:feb3:1666/64
```
- **root@testserver2:~# ip -br a**
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.182/24 metric 100 fe80::250:56ff:feb3:8745/64
ens224           UP             fe80::250:56ff:feb3:b7c7/64
ens224.20@ens224 UP             10.10.10.1/24 fe80::250:56ff:feb3:b7c7/64
```
- ### Проверим
- **root@testclient1:~# ping 10.10.10.1**
```bash
PING 10.10.10.1 (10.10.10.1) 56(84) bytes of data.
64 bytes from 10.10.10.1: icmp_seq=1 ttl=64 time=0.095 ms
```
- **root@testserver1:~# tcpdump -i ens224 -e vlan**
```bash
08:37:21.982580 00:50:56:b3:0a:62 (oui Unknown) > 00:50:56:b3:42:a3 (oui Unknown), ethertype 802.1Q (0x8100), length 102: vlan 10, p 0, ethertype IPv4 (0x0800), testserver1 > 10.10.10.254: ICMP echo reply, id 5939, seq 5, length 64
```
- **root@testclient2:~# ping 10.10.10.1**
```bash
PING 10.10.10.1 (10.10.10.1) 56(84) bytes of data.
64 bytes from 10.10.10.1: icmp_seq=1 ttl=64 time=0.081 ms
64 bytes from 10.10.10.1: icmp_seq=2 ttl=64 time=0.064 m
```
- **root@testserver2:~# tcpdump -i ens224 -e vlan | grep 10.10.10.254**
```bash
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on ens224, link-type EN10MB (Ethernet), snapshot length 262144 bytes
08:43:51.810187 00:50:56:b3:16:66 (oui Unknown) > 00:50:56:b3:b7:c7 (oui Unknown), ethertype 802.1Q (0x8100), length 102: vlan 20, p 0, ethertype IPv4 (0x0800), 10.10.10.254 > testserver2: ICMP echo request, id 5946, seq 28, length 64
```
- ### Между ВМ testclient1 и testclient2, testserver1 и testserver2 конфликтов из-за одинаковых адресов нет, машины testclient1 и testclient2, testserver1 и testserver2 находятся в изолированных сетях (VLAN10 | VLAN20)
- ###  Пример настройки через netplan:
```bash
root@testclient1:~# cat /etc/netplan/50-cloud-init.yaml
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: true

    ens224:
      dhcp4: no

  vlans:
    ens224.10:
      id: 10
      link: ens224
      addresses:
        - 10.10.10.254/24
```
- ### Для работы с VLAN trunk сетевых интерфейсов inetRouter и centralRouter создадим для них специальный виртуальный коммутатор Post binding на VMWare vShere и подключим к нему их пары интерфейсов (ens256 ens224), один интерфейс (ens192) подключен через коммутатор в режиме access к моей рабочей сети
<img width="823" height="799" alt="Screenshot 2026-01-28 at 15 35 57" src="https://github.com/user-attachments/assets/6b3104ab-d7b6-4f14-a11a-4f62cf63819d" />

- **root@*******:~# ip -br a**
```bash 
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.148/24 metric 100 fe80::250:56ff:feb3:e85a/64
ens224           DOWN
ens256           DOWN
```
- **root@inetlrouter:~# vi /etc/netplan/50-cloud-init.yaml**
```bash
 network:
  version: 2
  renderer: networkd

  ethernets:
    ens224:
      dhcp4: no
    ens225:
      dhcp4: no

  bonds:
    bond0:
      interfaces:
        - ens224
        - ens225
      parameters:
        mode: 802.3ad
        lacp-rate: fast
        transmit-hash-policy: layer3+4
        mii-monitor-interval: 100
      addresses:
        - 192.168.255.1/30
```
- **root@centralrouter:~# vi /etc/netplan/50-cloud-init.yaml**
```bash
network:
  version: 2
  renderer: networkd

  ethernets:
    ens224:
      dhcp4: no
    ens225:
      dhcp4: no

  bonds:
    bond0:
      interfaces:
        - ens224
        - ens225
      parameters:
        mode: 802.3ad
        lacp-rate: fast
        transmit-hash-policy: layer3+4
        mii-monitor-interval: 100
      addresses:
        - 192.168.255.2/30
```
- **root@*******:~# netplan generate**
- **root@*******:~# netplan apply**
- ###  Проверяем работу транка Bond через ping
- **root@centralrouter:~# ping 192.168.255.1** # работает
```bash
PING 192.168.255.1 (192.168.255.1) 56(84) bytes of data.
64 bytes from 192.168.255.1: icmp_seq=1 ttl=64 time=0.101 ms
64 bytes from 192.168.255.1: icmp_seq=2 ttl=64 time=0.104 ms
64 bytes from 192.168.255.1: icmp_seq=3 ttl=64 time=0.140 ms
```
- **root@inetrouter:~# ping 192.168.255.2** # в обратную сторону тоже работает
```bash
PING 192.168.255.2 (192.168.255.2) 56(84) bytes of data.
64 bytes from 192.168.255.2: icmp_seq=1 ttl=64 time=0.117 ms
64 bytes from 192.168.255.2: icmp_seq=2 ttl=64 time=0.101 ms
64 bytes from 192.168.255.2: icmp_seq=3 ttl=64 time=0.112 ms
```
- **root@centralrouter:~# ip -br a** # состояние интерфейсов
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.148/24 metric 100 fe80::250:56ff:feb3:e85a/64
ens224           UP
ens256           UP             fe80::250:56ff:feb3:e65b/64
bond0            UP             192.168.255.2/30 fe80::4cfe:38ff:fe69:9604/64
```
- **root@centralrouter:~# ip link set ens224 down** # кладем один интерфейс 
- **root@centralrouter:~# ip -br a** 
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.148/24 metric 100 fe80::250:56ff:feb3:e85a/64
ens224           DOWN
ens256           UP             fe80::250:56ff:feb3:e65b/64
bond0            DOWN           192.168.255.2/30 fe80::4cfe:38ff:fe69:9604/64
```
- **root@inetrouter:~# ping 192.168.255.2** # ping не прервался
```bash
PING 192.168.255.2 (192.168.255.2) 56(84) bytes of data.
64 bytes from 192.168.255.2: icmp_seq=1 ttl=64 time=0.117 ms
64 bytes from 192.168.255.2: icmp_seq=2 ttl=64 time=0.101 ms
64 bytes from 192.168.255.2: icmp_seq=3 ttl=64 time=0.112 ms
```  
- **root@centralrouter:~# ip link set ens256 down** # кладем второй интерфейс
- **root@centralrouter:~# ip -br a**
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.148/24 metric 100 fe80::250:56ff:feb3:e85a/64
ens224           DOWN
ens256           DOWN
bond0            DOWN           192.168.255.2/30 fe80::4cfe:38ff:fe69:9604/64
```
- **root@inetrouter:~# ping 192.168.255.2** # ping прервался
```bash
64 bytes from 192.168.255.2: icmp_seq=45 ttl=64 time=0.076 ms
From 192.168.255.1 icmp_seq=50 Destination Host Unreachable
From 192.168.255.1 icmp_seq=51 Destination Host Unreachable
From 192.168.255.1 icmp_seq=52 Destination Host Unreachable**
```
- **root@centralrouter:~# ip link set ens256 up** # поднимаем один интерфейс
- **root@centralrouter:~# ip link set ens224 up** # поднимаем второй интерфейс
- **root@centralrouter:~# ip -br a**
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.148/24 metric 100 fe80::250:56ff:feb3:e85a/64
ens224           UP
ens256           UP             fe80::250:56ff:feb3:e65b/64
bond0            UP             192.168.255.2/30 fe80::4cfe:38ff:fe69:9604/64
```
- **root@inetrouter:~# ping 192.168.255.2** # Пошло! Bond работает
```bash
From 192.168.255.1 icmp_seq=30 Destination Host Unreachable
From 192.168.255.1 icmp_seq=31 Destination Host Unreachable
64 bytes from 192.168.255.2: icmp_seq=35 ttl=64 time=1024 ms
64 bytes from 192.168.255.2: icmp_seq=36 ttl=64 time=0.190 ms
```


## 35 урок Мосты, туннели и VPN  

**Домашнее задание** <ins>"VPN"</ins>

**Цель**: Научится настраивать VPN-сервер в Linux-based системах.;

🎯 Что нужно сделать?

- **1)Настроить VPN между двумя ВМ в tun/tap режимах, замерить скорость в туннелях, сделать вывод об отличающихся показателях**
- **2)Поднять RAS на базе OpenVPN с клиентскими сертификатами, подключиться с локальной машины на ВМ**
- ### Развернул две ВМ под ОС Ubuntu 24.04: serverloc, clientloc
## Потрачено много времени на выполнение, поэтому немного теории
<details>
<summary> = 🧠 Теория 🧠= </summary>
	
- 🔹 TUN — маршрутизируемый VPN (L3)￼
￼
- ### TUN работает на 3 уровне OSI (IP). VPN поднимает виртуальный IP-интерфейс, и через него гоняется только IP-трафик.
- Как это выглядит
-		•	У клиента: tun0 с IP, например 10.8.0.2
-		•	У сервера: tun0 с IP, например 10.8.0.1
-		•	Дальше обычная маршрутизация
-		
- 🔹 Плюсы
- 	✅ Экономичный по трафику
- 	✅ Работает быстрее 
- 	✅ Легко масштабируется 
- 	✅ Лучший выбор для site-to-site и road warrior
- 	✅ Отлично дружит с NAT

- 🔹 Минусы
- 	❌ Не работает broadcast/multicast 
- 	❌ Не увидишь «соседей» по сети 
- 	❌ Не подходит для legacy-протоколов
  
- 🔹 Где использовать
-		•	Сервер ↔ сервер
-		•	Офис ↔ офис
-		•	Клиент ↔ офис
-		•	Когда нужна маршрутизация, а не «как будто в одном свиче»
- 👉 99% всех VPN — это TUN

- 🔹 TAP — мостовой VPN (L2)
- 
- ### TAP работает на 2 уровне OSI (Ethernet). VPN передаёт кадры Ethernet целиком — включая ARP, broadcast, NetBIOS и т.д.
- Как это выглядит
-	•	Клиент получает интерфейс tap0
-	•	Он в одном сегменте L2 с удалённой сетью
-	•	Часто используется bridge (br0)
- 🔹 Плюсы
- 	✅ Работает broadcast
- 	✅ Можно получить IP по DHCP из удалённой сети
- 	 ✅ Прозрачная сеть «как дома»

- 🔹 Минусы
- 	❌ Сильно больше трафика
- 	 ❌ Хуже масштабируется
- 	❌ Медленнее
- 	❌ Плохо через интернет
- 	❌ Требует bridge (часто боль)

- 🔹 Где использовать
-		•	Старые приложения
-		•	Протоколы, которым нужен L2
-		•	Виртуалки, тестовые стенды
-		•	Когда очень надо “как будто в одной локалке”

- 🔸 Короткое сравнение
```bash
- Критерий							TUN							TAP
- Уровень OSI						L3 (IP)						L2 (Ethernet)
- Тип трафика						IP							Ethernet
- Broadcast							❌							✅
- DHCP								❌							✅
- Производительность				⭐⭐⭐⭐					⭐⭐
- Масштабируемость					⭐⭐⭐⭐					⭐
- Рекомендован						✅ Да						❌ Только при необходимости
```
- 🔥 Практическая рекомендация
- Если ты не знаешь, нужен ли тебе TAP — значит, тебе нужен TUN.
- TAP выбирают осознанно, когда:
-	•	приложение не работает без broadcast
-	•	нужен DHCP из удалённой сети
-	•	ты точно понимаешь, зачем тебе L2
</details>

- ### # Устанавливаем нужные пакеты и отключаем SELinux
- **root@clientloc:~# apt update** 
- **root@clientloc:~# apt install openvpn iperf3 selinux-utils** # подключения к VPN, организации site-to-site или remote-access VPN, шифрования трафика; iperf3 - утилита для измерения пропускной способности сети
- **root@clientloc:~# setenforce 0** # отключаем SELinux
- setenforce: SELinux is disabled
- **root@serverloc:~# apt update**
- **root@serverloc:~# apt install openvpn iperf3 selinux-utils** 
- **root@serverloc:~# setenforce 0** # отключаем SELinux
- setenforce: SELinux is disabled
- 
- **root@serverloc:~# openvpn --genkey secret /etc/openvpn/static.key** # создаем файл-ключ
- **root@serverloc:~# cat /etc/openvpn/static.key** # проверим
```bash
#
# 2048 bit OpenVPN static key
#
-----BEGIN OpenVPN Static key V1-----
cfc17ce39235e19e37829bb48d33e733
2953bf84e8c76f54f10df52c53402490
07d51cbbf01ee9af049094b741cd431d
8f04d072f4e6d5df40032d90d8bf2a82
fde19d2e46820feff51ed19d272fc3ec
b06cc1121b46dcf8fc6a38b867ac199d
6ccc961f577f67fababa37014f01271b
6954a62c6eaba22f5b99658ec9c5ced0
d012f6a5c7ba28290da55beaa9f8d7f6
5118173eb516573b804cf152af66608d
c184c92c670daa987edce6e9949048a6
bb0a96f6a8ccfd76c8a1fe96296db4e4
b195c30b73a096ccabf1e6d2f181df86
271f179f48014abd558544e27b4c3309
9e801158dcdc3f62a650a1fca515b6ea
15f08c49c48770ba4e4e17ef484d960e
-----END OpenVPN Static key V1-----
```
- **root@serverloc:~# cd /etc/openvpn/**
- **root@serverloc:/etc/openvpn# scp ./static.key spg@10.0.77.136:/tmp/** # передадим ключ клиенту
```bash
The authenticity of host '10.0.77.136 (10.0.77.136)' can't be established.
ED25519 key fingerprint is SHA256:DofXG5ZW1tvwsu9egtoM42fRDVKzLzd5Ahn0Ig3Tjzk.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.0.77.136' (ED25519) to the list of known hosts.
spg@10.0.77.136's password:
static.key
```
- **root@clientloc:/tmp# ls** # gпроверил на клиенте
```bash
snap-private-tmp
static.key
```
- **root@clientloc:/tmp# sudo mv /tmp/static.key /etc/openvpn/ 
 chmod 600 /etc/openvpn/static.key** # переношу ключ в правильное место и даю права
- **root@clientloc:/tmp# ls -hal /etc/openvpn/** # проверка
```bash
total 24K
drwxr-xr-x   4 root root 4.0K Feb  6 08:12 .
drwxr-xr-x 109 root root 4.0K Feb  6 07:31 ..
drwxr-xr-x   2 root root 4.0K Nov 24 22:32 client
drwxr-xr-x   2 root root 4.0K Nov 24 22:32 server
-rw-------   1 spg  spg   636 Feb  6 08:07 static.key
-rwxr-xr-x   1 root root 1.5K Nov 24 22:32 update-resolv-conf
```
- **root@serverloc:/etc/openvpn# cat /etc/openvpn/server-tap.conf** # конфигурационный файл OpenVPN
```bash
dev tap0
proto udp
port 1194
ifconfig 10.10.10.1 255.255.255.0
topology subnet
secret /etc/openvpn/static.key
cipher AES-256-CBC
comp-lzo
status /var/log/openvpn-status.log
log /var/log/openvpn-tap.log
verb 3
```
- **root@serverloc:/etc/openvpn# cat /etc/systemd/system/openvpn@.service** # service unit для запуска OpenVPN
```bash
Description=OpenVPN Tunneling Application On %I
After=network.target
[Service]
Type=notify
PrivateTmp=true
ExecStart=/usr/sbin/openvpn --cd /etc/openvpn/ --config %i.conf
[Install]
WantedBy=multi-user.target
```
- **root@clientloc:/tmp# cat /etc/openvpn/client-tap.conf**
```bash
dev tap
remote 10.0.77.148
ifconfig 10.10.10.2 255.255.255.0
topology subnet
route 10.0.77.0 255.255.255.0
secret /etc/openvpn/static.key
cipher AES-256-CBC
comp-lzo
status /var/log/openvpn-status.log
log /var/log/openvpn.log
verb 3
```
- **root@clientloc:/tmp# cat /etc/systemd/system/openvpn@.service** # для клиента такой же
```bash
[Unit]
Description=OpenVPN Tunneling Application On %I
After=network.target
[Service]
Type=notify
PrivateTmp=true
ExecStart=/usr/sbin/openvpn --cd /etc/openvpn/ --config %i.conf
[Install]
WantedBy=multi-user.target
```
### После многих ошибок добавляю файлы для для режима работы tun (правки внесены и в файлы для tab, чтобы можно было запустить одновременно)
- **root@serverloc:/etc/openvpn# cat /etc/openvpn/server-tun.conf** # конфигурационный файл OpenVPN
```bash
dev tun
proto udp
port 1195

ifconfig 10.10.20.1 10.10.20.2

secret /etc/openvpn/static.key
cipher AES-256-CBC
comp-lzo

status /var/log/openvpn-status-tun.log
log /var/log/openvpn-tun.log
verb 3
```
- **root@clientloc:/etc/openvpn# cat client-tun.conf**
```bash
dev tun

proto udp
remote 10.0.77.148 1195

nobind

ifconfig 10.10.20.2 10.10.20.1
#route 10.0.77.0 255.255.255.0

secret /etc/openvpn/static.key
cipher AES-256-CBC
comp-lzo

status /var/log/openvpn-status-tun.log
log /var/log/openvpn-tun.log
verb 3
```

- **root@serverloc:~# systemctl start openvpn@server-tap**
- **root@serverloc:~# systemctl start openvpn@server-tun**
- **root@clientloc:~#systemctl start openvpn@client-tap**
- **root@clientloc:~#systemctl start openvpn@client-tun**

- **root@serverloc:/etc/openvpn# ip a | grep -E "tap0|tun0"**
```bash
10: tap0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 1000
    inet 10.10.10.1/24 scope global tap0
11: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 500
    inet 10.10.20.1 peer 10.10.20.2/32 scope global tun0
```
- **root@clientloc:/etc/openvpn# ip a | grep -E "tap0|tun0"**
```bash
16: tap0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 1000
    inet 10.10.10.2/24 scope global tap0
17: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 500
    inet 10.10.20.2 peer 10.10.20.1/32 scope global tun0
```

### Проверим работу VPN между двумя ВМ в tun/tap режимах:

- **root@serverloc:~# ping 10.10.10.2**
```bash
PING 10.10.10.2 (10.10.10.2) 56(84) bytes of data.
64 bytes from 10.10.10.2: icmp_seq=1 ttl=64 time=0.433 ms
64 bytes from 10.10.10.2: icmp_seq=2 ttl=64 time=0.399 ms
^C
```
- **root@serverloc:~# ping 10.10.20.2**
```bash
PING 10.10.20.2 (10.10.20.2) 56(84) bytes of data.
64 bytes from 10.10.20.2: icmp_seq=1 ttl=64 time=0.385 ms
64 bytes from 10.10.20.2: icmp_seq=2 ttl=64 time=0.324 ms
^C
```
- **root@clientloc:~# ping 10.10.10.1**
```bash
PING 10.10.10.1 (10.10.10.1) 56(84) bytes of data.
64 bytes from 10.10.10.1: icmp_seq=1 ttl=64 time=0.361 ms
64 bytes from 10.10.10.1: icmp_seq=2 ttl=64 time=0.328 ms
^C
```
- **root@clientloc:~# ping 10.10.20.1**
```bash
PING 10.10.20.1 (10.10.20.1) 56(84) bytes of data.
64 bytes from 10.10.20.1: icmp_seq=1 ttl=64 time=0.317 ms
64 bytes from 10.10.20.1: icmp_seq=2 ttl=64 time=0.317 ms
^C
```

### Далее необходимо замерить скорость в туннеле. Попробуем замерить одновременно...
```bash
root@serverloc:~# iperf3 -s -B 10.10.10.1 -p 5201 &   # TAP
[1] 2847
root@serverloc:~# -----------------------------------------------------------
Server listening on 5201 (test #1)
-----------------------------------------------------------
iperf3 -s -B 10.10iperf3 -s -B 10.10.20.1 -p 5202 &   # TUN
[2] 2850
root@serverloc:~# -----------------------------------------------------------
Server listening on 5202 (test #1)
-----------------------------------------------------------
Accepted connection from 10.10.20.2, port 42139
Accepted connection from 10.10.10.2, port 56623
```
```bash
root@clientloc:~# iperf3 -c 10.10.10.1 -p 5201 -P 4 -t 30 --bind 10.10.10.2 &   # TAP
iperf3 -c 10.10.20.1 -p 5202 -P 4 -t 30 --bind 10.10.20.2 &   # TUN
wait
[1] 3495
[2] 3496
Connecting to host 10.10.10.1, port 5201
Connecting to host 10.10.20.1, port 5202
.......
.......
[  5]  29.00-30.00  sec  13.4 MBytes   112 Mbits/sec  115   61.8 KBytes
[  7]  29.00-30.00  sec  15.8 MBytes   132 Mbits/sec  131   40.7 KBytes
[  9]  29.00-30.00  sec  13.4 MBytes   112 Mbits/sec  110   56.5 KBytes
[ 11]  29.00-30.00  sec  15.0 MBytes   126 Mbits/sec  125   63.1 KBytes
[SUM]  29.00-30.00  sec  57.5 MBytes   482 Mbits/sec  481
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.00  sec   437 MBytes   122 Mbits/sec  2419             sender
[  5]   0.00-30.00  sec   436 MBytes   122 Mbits/sec                  receiver
[  7]   0.00-30.00  sec   438 MBytes   122 Mbits/sec  2541             sender
[  7]   0.00-30.00  sec   437 MBytes   122 Mbits/sec                  receiver
[  9]   0.00-30.00  sec   395 MBytes   110 Mbits/sec  2619             sender
[  9]   0.00-30.00  sec   394 MBytes   110 Mbits/sec                  receiver
[ 11]   0.00-30.00  sec   448 MBytes   125 Mbits/sec  2674             sender
[ 11]   0.00-30.00  sec   448 MBytes   125 Mbits/sec                  receiver
[SUM]   0.00-30.00  sec  1.68 GBytes   480 Mbits/sec  10253             sender
[SUM]   0.00-30.00  sec  1.67 GBytes   480 Mbits/sec                  receiver

iperf Done.
- - - - - - - - - - - - - - - - - - - - - - - - -
[  5]  29.00-30.00  sec  13.2 MBytes   111 Mbits/sec   67   78.3 KBytes
[  7]  29.00-30.00  sec  15.4 MBytes   129 Mbits/sec   64   61.6 KBytes
[  9]  29.00-30.00  sec  15.6 MBytes   131 Mbits/sec   38   97.5 KBytes
[ 11]  29.00-30.00  sec  12.4 MBytes   104 Mbits/sec   51   57.7 KBytes
[SUM]  29.00-30.00  sec  56.6 MBytes   475 Mbits/sec  220
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.00  sec   443 MBytes   124 Mbits/sec  2260             sender
[  5]   0.00-30.01  sec   442 MBytes   124 Mbits/sec                  receiver
[  7]   0.00-30.00  sec   444 MBytes   124 Mbits/sec  2320             sender
[  7]   0.00-30.01  sec   443 MBytes   124 Mbits/sec                  receiver
[  9]   0.00-30.00  sec   427 MBytes   119 Mbits/sec  2711             sender
[  9]   0.00-30.01  sec   426 MBytes   119 Mbits/sec                  receiver
[ 11]   0.00-30.00  sec   424 MBytes   118 Mbits/sec  2696             sender
[ 11]   0.00-30.01  sec   423 MBytes   118 Mbits/sec                  receiver
[SUM]   0.00-30.00  sec  1.70 GBytes   486 Mbits/sec  9987             sender
[SUM]   0.00-30.01  sec  1.69 GBytes   485 Mbits/sec                  receiver

iperf Done.
[1]-  Done                    iperf3 -c 10.10.10.1 -p 5201 -P 4 -t 30 --bind 10.10.10.2
[2]+  Done                    iperf3 -c 10.10.20.1 -p 5202 -P 4 -t 30 --bind 10.10.20.2
root@clientloc:~#
```
- **два параллельных TCP-теста:**
-	•	TAP (10.10.10.x)
-	•	TUN (10.10.20.x) оба по 4 потока, 30 сек, одновременно.
### TAP - 480–486 Mbit/s Retr ~10 200; TUP - 475–485 Mbit/s Retr ~9 900 примерно одинаково делят один поток ≈ 480 Mbit/s (оба туннеля упираются в один и тот же CPU ?)
### Выводы выше в ТЕОРИИ

## 2. RAS на базе OpenVPN
- **root@serverloc:~# apt update**
- **root@serverloc:~# apt install openvpn easy-rsa**
- **root@serverloc:~# cd /etc/openvpn/** # Переходим в директорию /etc/openvpn

- **root@serverloc:/etc/openvpn# /usr/share/easy-rsa/easyrsa init-pki** # и инициализируем PKI

```bash
Notice
------
'init-pki' complete; you may now create a CA or requests.

Your newly created PKI dir is:
* /etc/openvpn/pki

Using Easy-RSA configuration:
* undefined
```
### Генерируем необходимые ключи и сертификаты для сервера
- **root@serverloc:/etc/openvpn# echo 'rasvpn' | /usr/share/easy-rsa/easyrsa gen-req server nopass**
```bash
No Easy-RSA 'vars' configuration file exists!

Using SSL:
* openssl OpenSSL 3.0.13 30 Jan 2024 (Library: OpenSSL 3.0.13 30 Jan 2024)
........+......+.+........+......+.........+...+.......+...+.....+.......+..+...+..........+..+....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*...+.+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*......+...+..+......+....+..+.+........+.+......+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
...+....+.....+.......+.....+...+.......+.....+.+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*......+...+.......+...+..+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.......+..+...............+....+..............+...+.......+...+...+..+.......+......+.....+.......+........+...............+....+..+.........+....+...+.........+.....+....+............+.....+....+...+..+.........+.+........+.+............+........+.+...+........+.......+.....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Common Name (eg: your user, host, or server name) [server]:
Notice
------
Private-Key and Public-Certificate-Request files created.
Your files are:
* req: /etc/openvpn/pki/reqs/server.req
* key: /etc/openvpn/pki/private/server.key
```
- **root@serverloc:/etc/openvpn# /usr/share/easy-rsa/easyrsa build-ca** 
```bash
No Easy-RSA 'vars' configuration file exists!

Using SSL:
* openssl OpenSSL 3.0.13 30 Jan 2024 (Library: OpenSSL 3.0.13 30 Jan 2024)

Enter New CA Key Passphrase:

Confirm New CA Key Passphrase:
.......+..+...+...+.......+.......................+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.................+.+......+.....+....+..+...+.......+..+...+...+....+.................+....+......+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.+...........+...+......+.......+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
.............+.........+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.+......+......+.....+...+.+.....+...+.......+.....+.+........+....+......+.........+..+...+...............+...+...+.........+......+.+.....+.........+....+..+......+...+....+......+.........+.....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.....+............+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Common Name (eg: your user, host, or server name) [Easy-RSA CA]:

Notice
------
CA creation complete. Your new CA certificate is at:
* /etc/openvpn/pki/ca.crt
```
- **root@serverloc:/etc/openvpn# echo 'yes' | /usr/share/easy-rsa/easyrsa sign-req server servre**
```bash
No Easy-RSA 'vars' configuration file exists!

Using SSL:
* openssl OpenSSL 3.0.13 30 Jan 2024 (Library: OpenSSL 3.0.13 30 Jan 2024)
You are about to sign the following certificate:
Please check over the details shown below for accuracy. Note that this request
has not been cryptographically verified. Please be sure it came from a trusted
source or that you have verified the request checksum with the sender.
Request subject, to be signed as a server certificate
for '825' days:

subject=
    commonName                = rasvpn

Type the word 'yes' to continue, or any other input to abort.
  Confirm request details:
Using configuration from /etc/openvpn/pki/openssl-easyrsa.cnf
Enter pass phrase for /etc/openvpn/pki/private/ca.key:
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
commonName            :ASN.1 12:'rasvpn'
Certificate is to be certified until May 15 09:20:15 2028 GMT (825 days)

Write out database with 1 new entries
Database updated

Notice
------
Certificate created at:
* /etc/openvpn/pki/issued/server.crt
```
- **root@serverloc:/etc/openvpn# /usr/share/easy-rsa/easyrsa gen-dh openvpn --genkey secret ca.key**
```bash
No Easy-RSA 'vars' configuration file exists!

Using SSL:
* openssl OpenSSL 3.0.13 30 Jan 2024 (Library: OpenSSL 3.0.13 30 Jan 2024)
Generating DH parameters, 2048 bit long safe prime
....+...............................................................................+........+..................................
...........++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*++*
DH parameters appear to be ok.

Notice
------

DH parameters of size 2048 created at:
* /etc/openvpn/pki/dh.pem
```



### Генерируем необходимые ключи и сертификаты для клиента
- **root@serverloc:/etc/openvpn# echo 'client' | /usr/share/easy-rsa/easyrsa gen-req client nopass**
```bash
Private-Key and Public-Certificate-Request files created.
Your files are:
* req: /etc/openvpn/pki/reqs/client.req
* key: /etc/openvpn/pki/private/client.key
```
- **root@serverloc:/etc/openvpn# echo 'yes' | /usr/share/easy-rsa/easyrsa sign-req client client**
```bash
No Easy-RSA 'vars' configuration file exists!

Using SSL:
* openssl OpenSSL 3.0.13 30 Jan 2024 (Library: OpenSSL 3.0.13 30 Jan 2024)
You are about to sign the following certificate:
Please check over the details shown below for accuracy. Note that this request
has not been cryptographically verified. Please be sure it came from a trusted
source or that you have verified the request checksum with the sender.
Request subject, to be signed as a client certificate
for '825' days:

subject=
    commonName                = client

Type the word 'yes' to continue, or any other input to abort.
  Confirm request details:
Using configuration from /etc/openvpn/pki/openssl-easyrsa.cnf
Enter pass phrase for /etc/openvpn/pki/private/ca.key:
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
commonName            :ASN.1 12:'client'
Certificate is to be certified until May 15 08:50:50 2028 GMT (825 days)

Write out database with 1 new entries
Database updated

Notice
------
Certificate created at:
* /etc/openvpn/pki/issued/client.crt
```
- **root@serverloc:/etc/openvpn# echo 'iroute 10.10.10.0 255.255.255.0' > /etc/openvpn/client/client** # Зададим параметр iroute для клиента
- **root@serverloc:/etc/openvpn# cat /etc/openvpn/server.conf** # Создаем конфигурационный файл сервера
```bash
port 1207
proto udp
dev tun
ca /etc/openvpn/pki/ca.crt
cert /etc/openvpn/pki/issued/server.crt
key /etc/openvpn/pki/private/server.key
dh /etc/openvpn/pki/dh.pem
server 10.10.10.0 255.255.255.0
ifconfig-pool-persist ipp.txt
client-to-client
#client-config-dir /etc/openvpn/client
keepalive 10 120
comp-lzo
persist-key
persist-tun
status /var/log/openvpn-status.log
log /var/log/openvpn.log
verb 3
```
- **root@clientloc:/etc/openvpn# cat client.conf** # Необходимо создать файл client.conf
```bash
dev tun
proto udp
remote 10.0.77.148 1207
client
resolv-retry infinite
remote-cert-tls server
ca /etc/openvpn/ca.crt
cert /etc/openvpn/client.crt
key /etc/openvpn/client.key
data-ciphers AES-256-GCM
persist-key
persist-tun
comp-lzo
verb 3
```
### Скопировать в одну директорию с client.conf файлы с сервера:
```bash
root@serverloc:/etc/openvpn/pki# scp ./ca.crt spg@10.0.77.136:/tmp
spg@10.0.77.136's password:
ca.crt                                                                        100% 1204     4.0MB/s   00:00
root@serverloc:/etc/openvpn/pki# scp ./issued/client.crt spg@10.0.77.136:/tmp
spg@10.0.77.136's password:
client.crt                                                                    100% 4493    12.6MB/s   00:00
root@serverloc:/etc/openvpn/pki# scp ./private/client.key spg@10.0.77.136:/tmp
spg@10.0.77.136's password:
client.key
root@clientloc:/tmp# mv ./c* /etc/openvpn/
root@clientloc:/tmp# ls /etc/openvpn/
ca.crt  client.conf  client.key       client-tun.conf  server.conf  update-resolv-conf
client  client.crt   client-tap.conf  server           static.key                                                                 100% 1704     5.8MB/s   00:00
```
- **root@clientloc:/etc/openvpn# ping -c 4 10.10.10.1** # заработало, когда закоментировал #client-config-dir /etc/openvpn/client в /etc/openvpn/server.conf
```bash
PING 10.10.10.1 (10.10.10.1) 56(84) bytes of data.
64 bytes from 10.10.10.1: icmp_seq=1 ttl=64 time=0.289 ms
64 bytes from 10.10.10.1: icmp_seq=2 ttl=64 time=0.318 ms
64 bytes from 10.10.10.1: icmp_seq=3 ttl=64 time=0.295 ms
64 bytes from 10.10.10.1: icmp_seq=4 ttl=64 time=0.262 ms

--- 10.10.10.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3076ms
rtt min/avg/max/mdev = 0.262/0.291/0.318/0.019 ms
```
- **root@clientloc:/etc/openvpn# ip r**
```bash
root@clientloc:/etc/openvpn# ip r
default via 10.0.77.1 dev ens192 proto dhcp src 10.0.77.136 metric 100
10.0.1.167 via 10.0.77.1 dev ens192 proto dhcp src 10.0.77.136 metric 100
10.0.1.194 via 10.0.77.1 dev ens192 proto dhcp src 10.0.77.136 metric 100
10.0.1.216 via 10.0.77.1 dev ens192 proto dhcp src 10.0.77.136 metric 100
10.0.77.0/24 dev ens192 proto kernel scope link src 10.0.77.136 metric 100
10.0.77.1 dev ens192 proto dhcp scope link src 10.0.77.136 metric 100
10.10.10.0/24 via 10.10.10.5 dev tun0
10.10.10.5 dev tun0 proto kernel scope link src 10.10.10.6
```
## 37 урок DNS - настройка и обслуживание 

**Домашнее задание** <ins>"Настраиваем split-dns"</ins>

**Цель**: 
- Создать домашнюю сетевую лабораторию;
- Изучить основы DNS;
- Научиться работать с технологией Split-DNS в Linux-based системах.;

🎯 Что нужно сделать?
```bash
1. взять стенд https://github.com/erlong15/vagrant-bind 
добавить еще один сервер client2
завести в зоне dns.lab имена:
web1 - смотрит на клиент1
web2  смотрит на клиент2
завести еще одну зону newdns.lab
завести в ней запись
www - смотрит на обоих клиентов

2. настроить split-dns
клиент1 - видит обе зоны, но в зоне dns.lab только web1
клиент2 видит только dns.lab
```
### Выполнение
- **Развернул 4 ВМ под "vSpere":**
<img width="1045" height="309" alt="Screenshot 2026-02-18 at 11 54 40" src="https://github.com/user-attachments/assets/9ad76e61-fe0e-4086-97bb-dfef5dc80395" />
<img width="849" height="709" alt="Screenshot 2026-02-18 at 11 56 10" src="https://github.com/user-attachments/assets/415a73a3-3b5f-49d1-89ca-d68444679de8" />

### На macOS установлен Ansible, сконфигурированны все файлы для запуска:
```bash
➜  provisioning git:(master) ✗ tree
.
├── client-motd
├── client-resolv.conf
├── inventory
├── master-named.conf
├── named.ddns.lab
├── named.dns.lab
├── named.dns.lab.rev
├── named.zonetransfer.key
├── playbook.yml
├── rndc.conf
├── servers-resolv.conf
├── slave-named.conf
└── zonetransfer.key

1 directory, 13 files
```

➜  provisioning git:(master) ✗ cat inventory 
```bash
[ns]
ns01 ansible_host=192.168.50.10 ansible_python_interpreter=/usr/libexec/platform-python
ns02 ansible_host=192.168.50.11 ansible_python_interpreter=/usr/libexec/platform-python

[clients]
client ansible_host=192.168.50.15 ansible_python_interpreter=/usr/libexec/platform-python
client2 ansible_host=192.168.50.16 ansible_python_interpreter=/usr/libexec/platform-python

[all:vars]
ansible_user=spg
```
### Python установить из репозиториев не удалось (недоступны для этой ОС) Переустановлены все ВМ в минимальной конфигурации с Development tools (python 3)
- Выяснилось, что нет python3-pip :))
- удалось решить проблему с репозиториями неподдерживаемой ОС (методичке много лет):
### https://www.veeble.com/kb/centos-stream-repo-list-working-urls/
- **[root@ns01 ~]# cat /etc/yum.repos.d/CentOS-Stream-BaseOS.repo**
```bash
[baseos]
#mirrorlist=http://mirrorlist.centos.org/?release=$stream&arch=$basearch&repo=BaseOS&infra=$infra
baseurl=http://vault.centos.org/$contentdir/$stream/BaseOS/$basearch/os/
``` 
- **[root@ns01 ~]# cat /etc/yum.repos.d/CentOS-Stream-Extras.repo**
```bash
#mirrorlist=http://mirrorlist.centos.org/?release=$stream&arch=$basearch&repo=extras&infra=$infra
baseurl=http://vault.centos.org/$contentdir/$stream/extras/$basearch/os/
```
- **[root@ns01 ~]# cat /etc/yum.repos.d/CentOS-Stream-AppStream.repo**
```bash
#mirrorlist=http://mirrorlist.centos.org/?release=$stream&arch=$basearch&repo=AppStream&infra=$infra
baseurl=http://vault.centos.org/$contentdir/$stream/AppStream/$basearch/os/
```
- **[root@ns01 ~]# cat /etc/yum.repos.d/CentOS-Stream-Extras-common.repo**
```bash
#mirrorlist=http://mirrorlist.centos.org/?release=$stream&arch=$basearch&repo=extras-extras-common
baseurl=http://vault.centos.org/$contentdir/$stream/extras/$basearch/extras-common/
```
- **[root@ns01 ~]# dnf install -y python3-pip** # Устанавливаю необходимые пакеты

```bash
Installed:
  python3-pip-9.0.3-24.el8.noarch                 python3-setuptools-39.2.0-7.el8.noarch                 python36-3.6.8-39.module_el8+762+77bd8591.x86_64

Complete!
```
- **[root@ns01 ~]# dnf install python39 python39-pip -y** # Предыдущего оказалось недостаточно

```bash
Installed:
  python39-3.9.19-1.module_el8+1051+5bea6413.x86_64                                python39-libs-3.9.19-1.module_el8+1051+5bea6413.x86_64
  python39-pip-20.2.4-9.module_el8+963+a9c12c76.noarch                             python39-pip-wheel-20.2.4-9.module_el8+963+a9c12c76.noarch
  python39-setuptools-50.3.2-5.module_el8+695+192a31a9.noarch                      python39-setuptools-wheel-50.3.2-5.module_el8+695+192a31a9.noarch

Complete!
```
- **➜  provisioning git:(master) ✗ cat inventory.ini** # Правим инвентори в соотвествии с установленным на ВМ python3.9
```bash
[ns]
ns01 ansible_host=192.168.50.10 ansible_python_interpreter=/bin/python3.9
ns02 ansible_host=192.168.50.11 ansible_python_interpreter=/bin/python3.9

[clients]
client ansible_host=192.168.50.15 ansible_python_interpreter=/bin/python3.9
client2 ansible_host=192.168.50.16 ansible_python_interpreter=/bin/python3.9

[all:vars]
ansible_user=spg
```
- **➜  provisioning git:(master) ✗ ansible all -i inventory.ini -m ping -k** # Проверяем доступность (все хорошо)
```bash
SSH password: 
ns01 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
client | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
ns02 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
client2 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
### В результате не заработало из-за старого python... Принял решение переписать playbook и пр. под Ubuntu 24.04 :(из-за малого опыта показалось, что "руками" настроил бы быстрее). Что получилось:
- **➜  provisioning git:(master) ✗ pwd**
- /Users/spg/Ansible/vagrant-bind/provisioning
- **➜  provisioning git:(master) ✗ tree**
```bash
.
├── ansible.cfg
├── client-motd
├── client-resolv.conf
├── files
│   ├── master-named.conf
│   ├── named.ddns.lab
│   ├── named.dns.lab
│   ├── named.dns.lab.rev
│   └── named.zonetransfer.key
├── inventory.ini
├── master-named.conf.old
├── playbook.all
├── playbook.bkp
├── playbook.last
├── playbook.ns2
├── playbook.yml
├── rndc.conf
├── servers-resolv.conf
├── slave-named.conf
├── slave-named.conf.old
└── zonetransfer.key

2 directories, 19 files
```
- **➜  provisioning git:(master) ✗ cat ansible.cfg** 
```bash
[defaults]
inventory = inventory.ini
host_key_checking = False
retry_files_enabled = False
stdout_callback = default
result_format = yaml
```
- **➜  provisioning git:(master) ✗ cat inventory.ini** 
```bash
[ns]
ns01 ansible_host=192.168.50.10
ns02 ansible_host=192.168.50.11

[clients]
client ansible_host=192.168.50.15
client2 ansible_host=192.168.50.16

[all:vars]
ansible_python_interpreter=/usr/bin/python3.12
ansible_user=spg
```
- **➜  provisioning git:(master) ✗ cat playbook.yml** 
```bash
---
############################################
# Install base packages
############################################

- hosts: all
  become: yes

  vars:
      ntp_server: "pool.ntp.org"
      timezone: "Europe/Moscow"

  tasks:

    - name: Temporary DNS
      copy:
        dest: /etc/resolv.conf
        content: |
          nameserver 8.8.8.8

    - name: Wait for dpkg lock
      shell: |
        while fuser /var/lib/dpkg/lock >/dev/null 2>&1; do
          sleep 1
        done

    - name: Update apt cache
      apt:
        update_cache: yes
        cache_valid_time: 3600

############################################
# INSTALL NTP
############################################

    - name: Set timezone
      timezone:
        name: "{{ timezone }}"

    - name: Install chrony
      apt:
        name: chrony
        state: present
        update_cache: yes

    - name: Configure chrony to use custom NTP server
      lineinfile:
        path: /etc/chrony/chrony.conf
        regexp: '^server '
        line: "server {{ ntp_server }} iburst"
        state: present
        backup: yes

    - name: Enable and start chrony service
      service:
        name: chrony
        state: started
        enabled: yes

    - name: Wait for chrony to sync
      shell: |
        until chronyc sources | grep -q '\*'; do
          sleep 1
        done
      retries: 10
      delay: 5
      register: sync_status
      until: sync_status.rc == 0

    - name: Make a one-time time correction
      command: chronyc makestep
      ignore_errors: yes

    - name: Show chrony tracking status
      command: chronyc tracking
      register: chrony_status

    - name: Show NTP sources
      command: chronyc sources -v
      register: chrony_sources

    - name: Display chrony status
      debug:
        var: chrony_status.stdout_lines

############################################
# INSTALL BIND
############################################

    - name: Install packages
      apt:
        name:
          - bind9
          - bind9utils
          - dnsutils
        state: present

    - name: Copy transfer key
      copy:
        src: named.zonetransfer.key
        dest: /etc/bind/named.zonetransfer.key
        owner: root
        group: bind
        mode: '0640'

############################################
# MASTER DNS
############################################

- hosts: ns01
  become: yes

  tasks:

    - name: Install master config
      copy:
        src: master-named.conf
        dest: /etc/bind/named.conf
        owner: root
        group: bind
        mode: '0644'
      notify: restart bind

    - name: Copy zone files
      copy:
        src: "{{ item }}"
        dest: /etc/bind/
        owner: root
        group: bind
        mode: '0664'
      loop:
        - named.dns.lab
        - named.dns.lab.rev
        - named.ddns.lab
      notify: restart bind

    - name: Create DNSSEC directory
      file:
        path: /var/cache/bind/dynamic
        state: directory
        owner: bind
        group: bind
        mode: '0775'

    - name: Check bind config
      command: named-checkconf /etc/bind/named.conf

    - name: Check forward zone
      command: named-checkzone dns.lab /etc/bind/named.dns.lab

    - name: Check reverse zone
      command: named-checkzone 50.168.192.in-addr.arpa /etc/bind/named.dns.lab.rev

    - name: Configure resolv.conf
      copy:
        src: servers-resolv.conf
        dest: /etc/resolv.conf
        mode: '0644'

  handlers:

    - name: restart bind
      service:
        name: bind9
        state: restarted
        enabled: yes

############################################
# SLAVE DNS
############################################

- hosts: ns02
  become: yes

  tasks:

    - name: Configure resolv.conf for slave
      copy:
        dest: /etc/resolv.conf
        content: |
          nameserver 192.168.50.11
          search lab
        mode: '0644'

    - name: Install slave config
      copy:
        src: slave-named.conf
        dest: /etc/bind/named.conf
        owner: root
        group: bind
        mode: '0644'
      notify: restart bind

    - name: Ensure bind directory permissions
      file:
        path: /etc/bind
        owner: root
        group: bind
        mode: '0775'

    - name: Ensure cache directory exists for slave zones
      file:
        path: /var/cache/bind/slaves
        state: directory
        owner: bind
        group: bind
        mode: '0775'

    - name: Create DNSSEC directory
      file:
        path: /var/cache/bind/dynamic
        state: directory
        owner: bind
        group: bind
        mode: '0775'

    - name: Check bind config
      command: named-checkconf /etc/bind/named.conf

    - name: Check zone from slave
      command: dig @192.168.50.11 dns.lab SOA

    - name: Configure resolv.conf
      copy:
        src: servers-resolv.conf
        dest: /etc/resolv.conf
        mode: '0644'

  handlers:

    - name: restart bind
      service:
        name: bind9
        state: restarted
        enabled: yes

############################################
# CLIENTS
############################################

- hosts: clients
  become: yes

  tasks:

    - name: Configure DNS resolver
      copy:
        src: client-resolv.conf
        dest: /etc/resolv.conf
        mode: '0644'

    - name: Install MOTD
      copy:
        src: client-motd
        dest: /etc/motd
        mode: '0644'
```      
- **➜  provisioning git:(master) ✗ cat ./files/master-named.conf** 
```bash
options {

    // network 
	listen-on port 53 { 127.0.0.1; 192.168.50.10; };
	listen-on-v6 port 53 { ::1; };

    // data
	directory 	"/var/cache/bind/";
	dump-file 	"/var/cache/bind/data/cache_dump.db";
	statistics-file "/var/cache/bind/data/named_stats.txt";
	memstatistics-file "/var/cache/bind/data/named_mem_stats.txt";

    // server
	recursion yes;
	allow-query     { any; };
        allow-transfer { any; };
    
    // dnssec
	dnssec-validation auto;

    // others
	bindkeys-file "/etc/bind/bind.key";
	managed-keys-directory "/var/cache/bind";
	pid-file "/run/named/named.pid";
	session-keyfile "/run/named/session.key";
};

logging {
        channel default_debug {
                file "/var/log/named/named.log";
                severity dynamic;
        };
};

// RNDC Control for client
key "rndc-key" {
    algorithm hmac-md5;
    secret "GrtiE9kz16GK+OKKU/qJvQ==";
};
controls {
        inet 192.168.50.10 allow { 192.168.50.11; } keys { "rndc-key"; }; 
};

// ZONE TRANSFER WITH TSIG
include "/etc/bind/named.zonetransfer.key"; 
server 192.168.50.11 {
    keys { "zonetransfer.key"; };
};

// root zone
zone "." IN {
	type hint;
	file "/usr/share/dns/root.hints";
};


// lab's zone
zone "dns.lab" {
    type master;
    allow-transfer { key "zonetransfer.key"; };
    file "/etc/bind/named.dns.lab";
};

// lab's zone reverse
zone "50.168.192.in-addr.arpa" {
    type master;
    allow-transfer { key "zonetransfer.key"; };
    file "/etc/bind/named.dns.lab.rev";
};

// lab's ddns zone
zone "ddns.lab" {
    type master;
    allow-transfer { key "zonetransfer.key"; };
    allow-update { key "zonetransfer.key"; };
    file "/etc/bind/named.ddns.lab";
};
```
- **➜  provisioning git:(master) ✗ cat slave-named.conf**
```bash
options {

    // network 
    listen-on port 53 { 127.0.0.1; 192.168.50.11; };
    listen-on-v6 port 53 { ::1; };

    // data
    directory       "/var/cache/bind";
    dump-file       "/var/cache/bind/cache_dump.db";
    statistics-file "/var/cache/bind/named_stats.txt";
    memstatistics-file "/var/cache/bind/named_mem_stats.txt";

    // server
    recursion yes;
    allow-query     { any; };
    allow-transfer { none; };
    
    // dnssec
    dnssec-validation auto;

    // others
    bindkeys-file "/etc/bind/named.iscdlv.key";
    managed-keys-directory "/var/cache/bind/dynamic";
    pid-file "/run/named/named.pid";
    session-keyfile "/run/named/session.key";
};

logging {
    channel default_debug {
        file "/var/log/named/named.run";
        severity dynamic;
    };
};

// RNDC Control for client
key "rndc-key" {
    algorithm hmac-md5;
    secret "GrtiE9kz16GK+OKKU/qJvQ==";
};
controls {
    inet 127.0.0.1 allow { localhost; } keys { "rndc-key"; }; 
};

// ZONE TRANSFER WITH TSIG
include "/etc/bind/named.zonetransfer.key"; 
server 192.168.50.10 {
    keys { "zonetransfer.key"; };
};

// root zone
zone "." IN {
    type hint;
    file "/usr/share/dns/root.hints";
};


// lab's zone
zone "dns.lab" {
    type slave;
    primaries { 192.168.50.10; };
    allow-transfer { key none; };
    file "slaves/named.dns.lab";
};

// lab's zone reverse
zone "50.168.192.in-addr.arpa" {
    type slave;
    primaries { 192.168.50.10; };
    file "slaves/named.dns.lab.rev";
};

// lab's ddns zone
zone "ddns.lab" {
    type slave;
    primaries { 192.168.50.10; };
    file "slaves/named.ddns.lab";
};
```
### Все же Ansible отработал 
- **➜  provisioning git:(master) ✗ ansible-playbook playbook.yml -k -K**                               
```bash
SSH password: 
BECOME password[defaults to SSH password]: 

PLAY [all] ****************************************************************************************************

TASK [Gathering Facts] ****************************************************************************************
ok: [ns02]
ok: [client2]
ok: [client]
ok: [ns01]

TASK [Temporary DNS] ******************************************************************************************
changed: [client]
changed: [client2]
changed: [ns02]
changed: [ns01]

TASK [Wait for dpkg lock] *************************************************************************************
changed: [ns02]
changed: [client]
changed: [client2]
changed: [ns01]

TASK [Update apt cache] ***************************************************************************************
changed: [ns02]
changed: [ns01]
changed: [client]
changed: [client2]

TASK [Set timezone] *******************************************************************************************
ok: [ns02]
ok: [ns01]
ok: [client]
ok: [client2]

TASK [Install chrony] *****************************************************************************************
ok: [ns02]
ok: [ns01]
ok: [client2]
ok: [client]

TASK [Configure chrony to use custom NTP server] **************************************************************
ok: [ns02]
ok: [client]
ok: [ns01]
ok: [client2]

TASK [Enable and start chrony service] ************************************************************************
ok: [ns02]
ok: [client]
ok: [client2]
ok: [ns01]

TASK [Wait for chrony to sync] ********************************************************************************
changed: [ns02]
changed: [ns01]
changed: [client2]
changed: [client]

TASK [Make a one-time time correction] ************************************************************************
changed: [ns01]
changed: [ns02]
changed: [client]
changed: [client2]

TASK [Show chrony tracking status] ****************************************************************************
changed: [ns01]
changed: [client]
changed: [client2]
changed: [ns02]

TASK [Show NTP sources] ***************************************************************************************
changed: [ns01]
changed: [client2]
changed: [ns02]
changed: [client]

TASK [Display chrony status] **********************************************************************************
ok: [ns01] => {
    "chrony_status.stdout_lines": [
        "Reference ID    : 596DFB17 (ntp3.vniiftri.ru)",
        "Stratum         : 2",
        "Ref time (UTC)  : Tue Mar 10 11:04:29 2026",
        "System time     : 0.000000000 seconds fast of NTP time",
        "Last offset     : +0.000039458 seconds",
        "RMS offset      : 0.000081662 seconds",
        "Frequency       : 16.490 ppm slow",
        "Residual freq   : +0.001 ppm",
        "Skew            : 0.031 ppm",
        "Root delay      : 0.004787003 seconds",
        "Root dispersion : 0.000856529 seconds",
        "Update interval : 1033.1 seconds",
        "Leap status     : Normal"
    ]
}
ok: [ns02] => {
    "chrony_status.stdout_lines": [
        "Reference ID    : 5E64B485 (ntp1.mail.ru)",
        "Stratum         : 3",
        "Ref time (UTC)  : Tue Mar 10 11:09:51 2026",
        "System time     : 0.000000000 seconds slow of NTP time",
        "Last offset     : +0.000039512 seconds",
        "RMS offset      : 0.000147538 seconds",
        "Frequency       : 16.394 ppm slow",
        "Residual freq   : -0.000 ppm",
        "Skew            : 0.053 ppm",
        "Root delay      : 0.007453739 seconds",
        "Root dispersion : 0.000234529 seconds",
        "Update interval : 516.9 seconds",
        "Leap status     : Normal"
    ]
}
ok: [client] => {
    "chrony_status.stdout_lines": [
        "Reference ID    : 596DFB18 (ntp4.vniiftri.ru)",
        "Stratum         : 2",
        "Ref time (UTC)  : Tue Mar 10 11:08:22 2026",
        "System time     : 0.000000000 seconds slow of NTP time",
        "Last offset     : +0.000060026 seconds",
        "RMS offset      : 0.000092363 seconds",
        "Frequency       : 16.471 ppm slow",
        "Residual freq   : +0.002 ppm",
        "Skew            : 0.042 ppm",
        "Root delay      : 0.005046131 seconds",
        "Root dispersion : 0.000207578 seconds",
        "Update interval : 1026.6 seconds",
        "Leap status     : Normal"
    ]
}
ok: [client2] => {
    "chrony_status.stdout_lines": [
        "Reference ID    : 504251D3 (ntp.sipleg.ru)",
        "Stratum         : 3",
        "Ref time (UTC)  : Tue Mar 10 11:00:21 2026",
        "System time     : 0.000000000 seconds slow of NTP time",
        "Last offset     : +0.000037685 seconds",
        "RMS offset      : 0.000196040 seconds",
        "Frequency       : 16.490 ppm slow",
        "Residual freq   : +0.000 ppm",
        "Skew            : 0.093 ppm",
        "Root delay      : 0.003300552 seconds",
        "Root dispersion : 0.001542723 seconds",
        "Update interval : 1037.2 seconds",
        "Leap status     : Normal"
    ]
}

TASK [Install packages] ***************************************************************************************
ok: [ns01]
ok: [client]
ok: [client2]
ok: [ns02]

TASK [Copy transfer key] **************************************************************************************
ok: [client]
ok: [client2]
ok: [ns01]
ok: [ns02]

PLAY [ns01] ***************************************************************************************************

TASK [Gathering Facts] ****************************************************************************************
ok: [ns01]

TASK [Install master config] **********************************************************************************
ok: [ns01]

TASK [Copy zone files] ****************************************************************************************
ok: [ns01] => (item=named.dns.lab)
ok: [ns01] => (item=named.dns.lab.rev)
ok: [ns01] => (item=named.ddns.lab)

TASK [Create DNSSEC directory] ********************************************************************************
ok: [ns01]

TASK [Check bind config] **************************************************************************************
changed: [ns01]

TASK [Check forward zone] *************************************************************************************
changed: [ns01]

TASK [Check reverse zone] *************************************************************************************
changed: [ns01]

TASK [Configure resolv.conf] **********************************************************************************
changed: [ns01]

PLAY [ns02] ***************************************************************************************************

TASK [Gathering Facts] ****************************************************************************************
ok: [ns02]

TASK [Configure resolv.conf for slave] ************************************************************************
changed: [ns02]

TASK [Install slave config] ***********************************************************************************
ok: [ns02]

TASK [Ensure bind directory permissions] **********************************************************************
ok: [ns02]

TASK [Ensure cache directory exists for slave zones] **********************************************************
ok: [ns02]

TASK [Create DNSSEC directory] ********************************************************************************
ok: [ns02]

TASK [Check bind config] **************************************************************************************
changed: [ns02]

TASK [Check zone from slave] **********************************************************************************
changed: [ns02]

TASK [Configure resolv.conf] **********************************************************************************
changed: [ns02]

PLAY [clients] ************************************************************************************************

TASK [Gathering Facts] ****************************************************************************************
ok: [client]
ok: [client2]

TASK [Configure DNS resolver] *********************************************************************************
changed: [client]
changed: [client2]

TASK [Install MOTD] *******************************************************************************************
ok: [client]
ok: [client2]

PLAY RECAP ****************************************************************************************************
client                     : ok=18   changed=8    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
client2                    : ok=18   changed=8    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ns01                       : ok=23   changed=11   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ns02                       : ok=24   changed=11   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

➜  provisioning git:(master) ✗ 
```
### Для того, чтобы при установке ПО на машины стенда у них был доступ в Интернет развернул еще один сервер inetServer с двумя сетевыми интерфейсами в качестве шлюза с NAT-ом и прокидыванием порта для доступа извне по ssh.

<img width="1202" height="527" alt="Screenshot 2026-03-10 at 10 07 04" src="https://github.com/user-attachments/assets/13e00436-dd11-447a-a8db-33ebb12a1141" />

### В предверии защиты проекта его разворачивание реализовал через Ansible:
- **➜  provisioning git:(master) ✗ cd ../../inetrouter** 
- **➜  inetrouter tree**
  
```bash
.
├── inventory.ini
└── playbook.yml
```

- **➜  inetrouter cat inventory.ini** 
```bash
[routers]
inetrouter ansible_host=10.0.77.182

[all:vars]
ansible_python_interpreter=/usr/bin/python3.12
ansible_user=spg
```
- **➜  inetrouter cat playbook.yml**
```bash
---
- hosts: inetrouter
  become: yes
  vars:
    lan_iface: ens224
    wan_iface: ens192
    lan_net: 192.168.50.0/24

  tasks:

    ########################################
    # Enable IPv4 forwarding
    ########################################
    - name: Enable IPv4 forwarding
      sysctl:
        name: net.ipv4.ip_forward
        value: '1'
        state: present
        reload: yes

    ########################################
    # Flush iptables
    ########################################
    - name: Flush filter table
      command: iptables -F

    - name: Flush NAT table
      command: iptables -t nat -F

    ########################################
    # Allow ICMP and loopback
    ########################################
    - name: Allow ICMP
      command: iptables -A INPUT -p icmp -j ACCEPT

    - name: Allow loopback
      command: iptables -A INPUT -i lo -j ACCEPT

    ########################################
    # Forward LAN <-> WAN
    ########################################
    - name: Forward LAN to WAN
      command: iptables -A FORWARD -i {{ lan_iface }} -o {{ wan_iface }} -j ACCEPT

    - name: Forward WAN to LAN for established connections
      command: iptables -A FORWARD -i {{ wan_iface }} -o {{ lan_iface }} -m state --state RELATED,ESTABLISHED -j ACCEPT

    ########################################
    # MASQUERADE outgoing traffic from LAN
    ########################################
    - name: MASQUERADE LAN -> WAN
      command: iptables -t nat -A POSTROUTING -s {{ lan_net }} -o {{ wan_iface }} -j MASQUERADE

    ########################################
    # DNAT for remote SSH (optional)
    ########################################
    - name: DNAT port 1010 -> internal host 192.168.50.10
      command: iptables -t nat -A PREROUTING -p tcp --dport 1010 -j DNAT --to-destination 192.168.50.10:22

    - name: DNAT port 1011 -> internal host 192.168.50.11
      command: iptables -t nat -A PREROUTING -p tcp --dport 1011 -j DNAT --to-destination 192.168.50.11:22

    - name: DNAT port 1015 -> internal host 192.168.50.15
      command: iptables -t nat -A PREROUTING -p tcp --dport 1015 -j DNAT --to-destination 192.168.50.15:22

    - name: DNAT port 1016 -> internal host 192.168.50.16
      command: iptables -t nat -A PREROUTING -p tcp --dport 1016 -j DNAT --to-destination 192.168.50.16:22
    ########################################
    # Save iptables rules persistently
    ########################################
    - name: Save iptables rules persistently
      shell: iptables-save > /etc/iptables/rules.v4
      args:
        executable: /bin/bash

    ########################################
    # Apply netplan
    ########################################
    - name: Apply netplan configuration
      command: netplan apply
```
- **root@inetrouter:~# cat /etc/netplan/50-cloud-init.yaml**
```bash
network:
  version: 2
  renderer: networkd
  ethernets:
    ens192:
      dhcp4: no
      addresses:
        - 10.0.77.182/24
      routes:
        - to: default
          via: 10.0.77.1
      nameservers:
        addresses: [10.0.1.167, 10.0.1.194]
    ens224:
      dhcp4: no
      addresses:
        - 192.168.50.1/24
```
- **root@ns01:~# cat /etc/netplan/50-cloud-init.yaml** # У остальных трех машин (192.168.50.11, 192.168.50.15 и 192.168.50.16) сетевые настройки аналогичные. Все получили доступ в Интернет и доступ к ним по портам 1010,1011,1015 и 1016 на 22 порт.
```bash
network:
  version: 2
  renderer: networkd

  ethernets:

    ens192:
      dhcp4: no
      addresses:
        - 192.168.50.10/24
      routes:
        - to: default
          via: 192.168.50.1
```

### Проверки
- **root@client1otus:~# dig @192.168.50.10 web1.dns.lab**
```bash

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> @192.168.50.10 web1.dns.lab
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 38497
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: eeae3ef1d95bd04a0100000069afc703beea775ffc1279b0 (good)
;; QUESTION SECTION:
;web1.dns.lab.			IN	A

;; ANSWER SECTION:
web1.dns.lab.		3600	IN	A	192.168.50.15

;; Query time: 0 msec
;; SERVER: 192.168.50.10#53(192.168.50.10) (UDP)
;; WHEN: Tue Mar 10 07:23:47 UTC 2026
;; MSG SIZE  rcvd: 85
```
- **root@client1otus:~# dig @192.168.50.11 web2.dns.lab**
```bash
; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> @192.168.50.11 web2.dns.lab
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 63665
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 86bdf845caedfd970100000069affd4bf8f3154d8d91cf22 (good)
;; QUESTION SECTION:
;web2.dns.lab.			IN	A

;; ANSWER SECTION:
web2.dns.lab.		3600	IN	A	192.168.50.16

;; Query time: 1 msec
;; SERVER: 192.168.50.11#53(192.168.50.11) (UDP)
;; WHEN: Tue Mar 10 14:15:23 MSK 2026
;; MSG SIZE  rcvd: 85
```
### Пропишем новую зону на DNS-серверах:
- **root@ns01:~# vi /etc/bind/named.conf**
```bash
...
// lab's newdns zone
zone "newdns.lab" {
    type master;
    allow-transfer { key "zonetransfer.key"; };
    allow-update { key "zonetransfer.key"; };
    file "/etc/bind/named.newdns.lab";
};
```
- **root@ns020tus:~# vi /etc/bind/named.conf**
```bash
...
// lab's newdns zone
zone "newdns.lab" {
    type slave;
    primaries { 192.168.50.10; };
    file "slaves/named.newdns.lab";
};
```
- **root@ns01:~# cat /etc/bind/named.newdns.lab** # сам файл
```bash
$TTL 3600
$ORIGIN newdns.lab.
@               IN      SOA     ns01.dns.lab. root.dns.lab. (
                            2026031001 ; serial
                            3600       ; refresh (1 hour)
                            600        ; retry (10 minutes)
                            86400      ; expire (1 day)
                            600        ; minimum (10 minutes)
                        )

                IN      NS      ns01.dns.lab.
                IN      NS      ns02.dns.lab.

; DNS Servers
ns01            IN      A       192.168.50.10
ns02            IN      A       192.168.50.11

;WWW
www             IN      A       192.168.50.15
www             IN      A       192.168.50.16
```
- **root@ns01:~# ls -hal  /etc/bind/named.newdns.lab**
```bash
-rw-rw---- 1 root bind 700 Mar 10 14:29 /etc/bind/named.newdns.lab
```
### увеличиваем счетчик 2026031001 ; serial на 1 и перезапускаем bind - systemctl restart named
- **root@ns020tus:~# ls /var/cache/bind/slaves/ | grep newdns** # на slave появилась новая зона
```bind
named.newdns.lab
```
## 2. Настройка Split-DNS 
```bind
У нас уже есть прописанные зоны dns.lab и newdns.lab. Однако по заданию client1  должен видеть запись web1.dns.lab и не видеть запись web2.dns.lab. Client2 может видеть обе записи из домена dns.lab, но не должен видеть записи домена newdns.lab Осуществить данные настройки нам поможет технология Split-DNS.  
Для настройки Split-DNS нужно: 
1) Создать дополнительный файл зоны dns.lab, в котором будет прописана только одна запись: vim /etc/named/named.dns.lab.client
```
- **root@ns01:~# cat  /etc/bind/named.dns.lab.client**
```bash
$TTL 3600
$ORIGIN dns.lab.
@               IN      SOA     ns01.dns.lab. root.dns.lab. (
                            2026031001 ; serial
                            3600       ; refresh (1 hour)
                            600        ; retry (10 minutes)
                            86400      ; expire (1 day)
                            600        ; minimum (10 minutes)
                        )

                IN      NS      ns01.dns.lab.
                IN      NS      ns02.dns.lab.

; DNS Servers
ns01            IN      A       192.168.50.10
ns02            IN      A       192.168.50.11

;Web
web1            IN      A       192.168.50.15
```
- **root@ns01:~# ls -hal /etc/bind/named.dns.lab.client**
```bash
-rw-rw---- 1 root bind 651 Mar 10 14:55 /etc/bind/named.dns.lab.client
```
### сгенерируем ключи для хостов client и client2
- **root@ns01:/etc/bind# sudo rndc-confgen -a -b 256 -k tsig-client -c /etc/bind/tsig-client.key**
```bash
wrote key file "/etc/bind/tsig-client.key"
```
- **root@ns01:/etc/bind# cat /etc/bind/tsig-client.key**
```bash
key "tsig-client" {
	algorithm hmac-sha256;
	secret "Vmu2YJy3PxwOP2IYUSEfTgSPHjZt54WYpZYD9seU9DI=";
};
```
- **root@ns01:/etc/bind# sudo rndc-confgen -a -b 256 -k tsig-client2 -c /etc/bind/tsig-client2.key
cat /etc/bind/tsig-client2.key**
```bash
wrote key file "/etc/bind/tsig-client2.key"
key "tsig-client2" {
	algorithm hmac-sha256;
	secret "2fOKPhzHxkN+aNNckFhfnNWX3b5davBppBhJSNjrn7Q=";
};
```
### добавим блок с access листами в конец файла /etc/named.conf на обоих серверах в конец:
```bash
#Описание ключа для хоста client
key "client-key" {
    algorithm hmac-sha256;
    secret "Vmu2YJy3PxwOP2IYUSEfTgSPHjZt54WYpZYD9seU9DI=";
};
#Описание ключа для хоста client2
key "client2-key" {
    algorithm hmac-sha256;
    secret "2fOKPhzHxkN+aNNckFhfnNWX3b5davBppBhJSNjrn7Q=";
};
#Описание access-листов
acl client { !key client2-key; key client-key; 192.168.50.15; };
acl client2 { !key client-key; key client2-key; 192.168.50.16; };
```
### client имеет адрес 192.168.50.15, использует client-key и не использует client2-key
### client2 имеет адрес 192ю168.50.16, использует clinet2-key и не использует client-key
### /etc/bind/named.dns.lab.client файл у нас уже создан выше
### Теперь можно внести правки в /etc/named.conf

### Технология Split-DNS реализуется с помощью описания представлений (view), для каждого отдельного acl. В каждое представление (view) добавляются только те зоны, которые разрешено видеть хостам, адреса которых указаны в access листе.

### Все ранее описанные зоны должны быть перенесены в модули view. Вне view зон быть недолжно, зона any должна всегда находиться в самом низу. 
- **root@ns01:~# cat /etc/bind/named.conf** # Правим зоны в представлениях для ограничейни клиентов
```bash
options {

    // network
	listen-on port 53 { 127.0.0.1; 192.168.50.10; };
	listen-on-v6 port 53 { ::1; };

    // data
	directory 	"/var/cache/bind/";
	dump-file 	"/var/cache/bind/data/cache_dump.db";
	statistics-file "/var/cache/bind/data/named_stats.txt";
	memstatistics-file "/var/cache/bind/data/named_mem_stats.txt";

    // server
	recursion yes;
	allow-query     { any; };
        allow-transfer { any; };

    // dnssec
	dnssec-validation auto;

    // others
	bindkeys-file "/etc/bind/bind.key";
	managed-keys-directory "/var/cache/bind";
	pid-file "/run/named/named.pid";
	session-keyfile "/run/named/session.key";
};

logging {
        channel default_debug {
                file "/var/log/named/named.log";
                severity dynamic;
        };
};

// RNDC Control for client
key "rndc-key" {
    algorithm hmac-md5;
    secret "GrtiE9kz16GK+OKKU/qJvQ==";
};
controls {
        inet 192.168.50.10 allow { 192.168.50.15;  192.168.50.16; } keys { "rndc-key"; };
};

key "client-key" {
    algorithm hmac-sha256;
    secret "Vmu2YJy3PxwOP2IYUSEfTgSPHjZt54WYpZYD9seU9DI=";
};
key "client2-key" {
    algorithm hmac-sha256;
    secret "2fOKPhzHxkN+aNNckFhfnNWX3b5davBppBhJSNjrn7Q=";
};

// ZONE TRANSFER WITH TSIG
include "/etc/bind/named.zonetransfer.key";
server 192.168.50.11 {
    keys { "zonetransfer.key"; };
};
#Описание access-листов
acl client { !key client2-key; key client-key; 192.168.50.15; };
acl client2 { !key client-key; key client2-key; 192.168.50.16; };

// Настройка первого view
view "client" {
    // Кому из клиентов разрешено подключаться, нужно указать имя access-листа
    match-clients { client; };

    // Описание зоны dns.lab для client
    zone "dns.lab" {
        // Тип сервера — мастер
        type master;
        // Добавляем ссылку на файл зоны, который создали в прошлом пункте
        file "/etc/bind/named.dns.lab.client";
        // Адрес хостов, которым будет отправлена информация об изменении зоны
        also-notify { 192.168.50.11 key client-key; };
    };

    // newdns.lab zone
    zone "newdns.lab" {
        type master;
        file "/etc/bind/named.newdns.lab";
        also-notify { 192.168.50.11 key client-key; };
    };
};

// Описание view для client2
view "client2" {
    match-clients { client2; };

    // dns.lab zone
    zone "dns.lab" {
        type master;
        file "/etc/bind/named.dns.lab";
        also-notify { 192.168.50.11 key client2-key; };
    };

    // dns.lab zone reverse
    zone "50.168.192.in-addr.arpa" {
        type master;
        file "/etc/bind/named.dns.lab.rev";
        also-notify { 192.168.50.11 key client2-key; };
    };
};

// Зона any, указана в файле самой последней
view "default" {
    match-clients { any; };

// root zone
zone "." IN {
	type hint;
	file "/usr/share/dns/root.hints";
};

// lab's zone
zone "dns.lab" {
    type master;
    allow-transfer { key "zonetransfer.key"; };
    file "/etc/bind/named.dns.lab";
};

// lab's zone reverse
zone "50.168.192.in-addr.arpa" {
    type master;
    allow-transfer { key "zonetransfer.key"; };
    file "/etc/bind/named.dns.lab.rev";
};

// lab's ddns zone
zone "ddns.lab" {
    type master;
    allow-transfer { key "zonetransfer.key"; };
    allow-update { key "zonetransfer.key"; };
    file "/etc/bind/named.ddns.lab";
};

};
```


### Проверка на клиенте 1 и 2 прошли успешно (и при остановленной службе named на ns01) :
```bash
root@client1otus:~# ping www.newdns.lab
PING www.newdns.lab (192.168.50.15) 56(84) bytes of data.
64 bytes from 192.168.50.15: icmp_seq=1 ttl=64 time=0.018 ms
64 bytes from 192.168.50.15: icmp_seq=2 ttl=64 time=0.016 ms
64 bytes from 192.168.50.15: icmp_seq=3 ttl=64 time=0.026 ms
^C
--- www.newdns.lab ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2080ms
rtt min/avg/max/mdev = 0.016/0.020/0.026/0.004 ms

root@client1otus:~# ping web1.dns.lab
PING web1.dns.lab (192.168.50.15) 56(84) bytes of data.
64 bytes from 192.168.50.15: icmp_seq=1 ttl=64 time=0.012 ms
64 bytes from 192.168.50.15: icmp_seq=2 ttl=64 time=0.016 ms
^C
--- web1.dns.lab ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1025ms
rtt min/avg/max/mdev = 0.012/0.014/0.016/0.002 ms

root@client1otus:~# ping web2.dns.lab
ping: web2.dns.lab: Name or service not known

root@client2otus:~# ping www.newdns.lab
ping: www.newdns.lab: Name or service not known

root@client2otus:~# ping web1.dns.lab
PING web1.dns.lab (192.168.50.15) 56(84) bytes of data.
64 bytes from 192.168.50.15: icmp_seq=1 ttl=64 time=0.084 ms
64 bytes from 192.168.50.15: icmp_seq=2 ttl=64 time=0.087 ms
^C
--- web1.dns.lab ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1028ms
rtt min/avg/max/mdev = 0.084/0.085/0.087/0.001 ms

root@client2otus:~# ping web2.dns.lab
PING web2.dns.lab (192.168.50.16) 56(84) bytes of data.
64 bytes from 192.168.50.16: icmp_seq=1 ttl=64 time=0.023 ms
64 bytes from 192.168.50.16: icmp_seq=2 ttl=64 time=0.018 ms
^C
--- web2.dns.lab ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1040ms
rtt min/avg/max/mdev = 0.018/0.020/0.023/0.002 ms
```
- **root@ns020tus:~# dig @192.168.50.10 dns.lab AXFR -k /etc/bind/named.zonetransfer.key**
```bash
; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> @192.168.50.10 dns.lab AXFR -k /etc/bind/named.zonetransfer.key
; (1 server found)
;; global options: +cmd
dns.lab.		3600	IN	SOA	ns01.dns.lab. root.dns.lab. 2026030801 3600 600 86400 600
dns.lab.		3600	IN	NS	ns01.dns.lab.
dns.lab.		3600	IN	NS	ns02.dns.lab.
ns01.dns.lab.		3600	IN	A	192.168.50.10
ns02.dns.lab.		3600	IN	A	192.168.50.11
web1.dns.lab.		3600	IN	A	192.168.50.15
web2.dns.lab.		3600	IN	A	192.168.50.16
dns.lab.		3600	IN	SOA	ns01.dns.lab. root.dns.lab. 2026030801 3600 600 86400 600
zonetransfer.key.	0	ANY	TSIG	hmac-md5.sig-alg.reg.int. 1773162410 300 16 GR4tzY39ryGUEy9tkDappA== 11393 NOERROR 0
;; Query time: 0 msec
;; SERVER: 192.168.50.10#53(192.168.50.10) (TCP)
;; WHEN: Tue Mar 10 20:06:50 MSK 2026
;; XFR size: 8 records (messages 1, bytes 339)
```
### Добавил в Ansible проект файлы named.dns.lab.client и named.newdns.lab
- **➜  DNS tree**
```bash
.
├── ansible.cfg
├── client-motd
├── client-resolv.conf
├── files
│   ├── master-named.conf
│   ├── named.ddns.lab
│   ├── named.dns.lab
│   ├── named.dns.lab.client
│   ├── named.dns.lab.rev
│   ├── named.newdns.lab
│   └── named.zonetransfer.key
├── inventory.ini
├── master-named.conf.old
├── playbook.all
├── playbook.bkp
├── playbook.last
├── playbook.ns2
├── playbook.yml
├── rndc.conf
├── servers-resolv.conf
├── slave-named.conf
├── slave-named.conf.old
└── zonetransfer.key

2 directories, 22 files
```
### Ansible отработал без ошибок: 
```bash
PLAY RECAP ****************************************************************************************************
client                     : ok=18   changed=7    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
client2                    : ok=18   changed=8    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ns01                       : ok=24   changed=13   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ns02                       : ok=24   changed=11   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

➜  DNS date
Tue Mar 10 21:19:42 MSK 2026
```
### Тесты прошли успешно и на этом ДЗ закончено наконец...
```bash
root@client1otus:~# ping www.newdns.lab
PING www.newdns.lab (192.168.50.15) 56(84) bytes of data.
64 bytes from 192.168.50.15: icmp_seq=1 ttl=64 time=0.020 ms
64 bytes from 192.168.50.15: icmp_seq=2 ttl=64 time=0.016 ms
^C
--- www.newdns.lab ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1024ms
rtt min/avg/max/mdev = 0.016/0.018/0.020/0.002 ms

root@client1otus:~# ping web1.dns.lab
PING web1.dns.lab (192.168.50.15) 56(84) bytes of data.
64 bytes from 192.168.50.15: icmp_seq=1 ttl=64 time=0.009 ms
64 bytes from 192.168.50.15: icmp_seq=2 ttl=64 time=0.018 ms
^C
--- web1.dns.lab ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1043ms
rtt min/avg/max/mdev = 0.009/0.013/0.018/0.004 ms

root@client1otus:~# ping web2.dns.lab
ping: web2.dns.lab: Name or service not known

root@client2otus:~# ping www.newdns.lab
ping: www.newdns.lab: Name or service not known

root@client2otus:~# ping web1.dns.lab
PING web1.dns.lab (192.168.50.15) 56(84) bytes of data.
64 bytes from 192.168.50.15: icmp_seq=1 ttl=64 time=0.102 ms
64 bytes from 192.168.50.15: icmp_seq=2 ttl=64 time=0.104 ms
^C
--- web1.dns.lab ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1056ms
rtt min/avg/max/mdev = 0.102/0.103/0.104/0.001 ms

root@client2otus:~# ping web2.dns.lab
PING web2.dns.lab (192.168.50.16) 56(84) bytes of data.
64 bytes from 192.168.50.16: icmp_seq=1 ttl=64 time=0.024 ms
64 bytes from 192.168.50.16: icmp_seq=2 ttl=64 time=0.018 ms
^C
--- web2.dns.lab ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1050ms
rtt min/avg/max/mdev = 0.018/0.021/0.024/0.003 ms

root@client2otus:~# date
Tue Mar 10 09:26:19 PM MSK 2026
```


## 38 урок LDAP. Централизованная авторизация и аутентификация 

**Домашнее задание** <ins>"LDAP"</ins>

**Цель**: Научиться настраивать LDAP-сервер и подключать к нему LDAP-клиентов;

🎯 Что нужно сделать?
**1. Установить FreeIPA**

### 1. В CentOS 8 столкнулся с проблемами. Недоступность официальных зеркал репозиториев из-за того, что CentOS 8 достиг конца жизни (EOL) 31 декабря 2021 года, и официальные зеркала заархивированы или удалены.
### 2. Перешел на  Ubuntu. Нет IPA-сервера, только клиент.
### 3. Выбрал Rockylinux 9, на нем и выполнено задание.

- **[root@localhost ~]# hostnamectl set-hostname FreeIPA_Server**
- **[root@localhost ~]# hostnamectl status**
 Static hostname: FreeIPAServer

- **[root@FreeIPAServer ~]# nmcli con modify ens192 \
  ipv4.method manual \
  ipv4.addresses 10.0.77.170/24 \
  ipv4.gateway 10.0.77.1 \
  ipv4.dns "10.0.1.167 10.0.1.194" \
  ipv4.dns-search garant.ru \
  connection.autoconnect yes**

- **[root@FreeIPAServer ~]#** 
```bash
nmcli con down ens192
nmcli con up ens192
```
- **[root@FreeIPAServer ~]# ip -br a**
```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
ens192           UP             10.0.77.170/24 fe80::250:56ff:feb3:7658/64
```
- **[root@FreeIPAServer ~]# cat /etc/resolv.conf**
```bash
# Generated by NetworkManager
search garant.ru
nameserver 10.0.1.167
nameserver 10.0.1.194
```
- **[root@FreeIPAServer ~]# ping ya.ru**

```bash
PING ya.ru (5.255.255.242) 56(84) bytes of data.
64 bytes from ya.ru (5.255.255.242): icmp_seq=1 ttl=56 time=8.03 ms
64 bytes from ya.ru (5.255.255.242): icmp_seq=2 ttl=56 time=7.83 ms
```
**[root@FreeIPAServer ~]# dnf repolist** # Репозитории
```bash
идентификатор репозитория                        имя репозитория
appstream                                        Rocky Linux 9 - AppStream
baseos                                           Rocky Linux 9 - BaseOS
epel                                             Extra Packages for Enterprise Linux 9 - x86_64
epel-cisco-openh264                              Extra Packages for Enterprise Linux 9 openh264 (From Cisco) - x86_64
extras                                           Rocky Linux 9 - Extras
```
- **[root@FreeIPAServer ~]# setenforce 0** # гасим Selinux
```bash
getenforce
Permissive
```
- **[root@FreeIPAServer ~]# vi /etc/selinux/config** # **SELINUX=disabled**
- **[root@FreeIPAServer ~]# dnf install -y ipa-server ipa-server-dns** # Установка пакетов IPA сервера
```bash
  xkeyboard-config-2.33-2.el9.0.1.noarch                                  xml-commons-apis-1.4.01-39.el9.noarch
  xml-commons-resolver-1.2-42.el9.noarch                                  xorg-x11-fonts-Type1-7.5-33.el9.noarch
  ...
Выполнено!
```
- **[root@FreeIPAServer ~]# hostnamectl set-hostname ipa.otus.lan** # переименовал (?)
- **[root@FreeIPAServer ~]# cat /etc/hosts**
```bash
host.conf  hostname   hosts
[root@FreeIPAServer ~]# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
10.0.77.170 ipa.otus.lan ipa
```
- **[root@ipa ~]# ipa-server-install** # установка (много, долго и непонятно)
```bash
Server host name [FreeIPAServer]: ipa.otus.lan
the domain name [otus.lan]
Following DNS servers are configured in /etc/resolv.conf: 10.0.1.167, 10.0.1.194
a realm name [OTUS.LAN]:
Do you want to configure DNS forwarders? [yes]: yes
Do you want to configure these servers as DNS forwarders? [yes]: yes
Do you want to search for missing reverse zones? [yes]: no
NetBIOS domain name [OTUS]:
Do you want to configure chrony with NTP server or pool address? [no]:
Continue to configure the system with these values? [no]: yes

==============================================================================
Setup complete

Next steps:
	1. You must make sure these network ports are open:
		TCP Ports:
		  * 80, 443: HTTP/HTTPS
		  * 389, 636: LDAP/LDAPS
		  * 88, 464: kerberos
		  * 53: bind
		UDP Ports:
		  * 88, 464: kerberos
		  * 53: bind
		  * 123: ntp

	2. You can now obtain a kerberos ticket using the command: 'kinit admin'
	   This ticket will allow you to use the IPA tools (e.g., ipa user-add)
	   and the web user interface.

Be sure to back up the CA certificates stored in /root/cacert.p12
These files are required to create replicas. The password for these
files is the Directory Manager password
The ipa-server-install command was successful
```
- **[root@ipa ~]# kinit admin** # проверим, что система может выдать билет
```bash
Password for admin@OTUS.LAN:
```
- **[root@ipa ~]# klist** # выдает
```bash
Ticket cache: KCM:0
Default principal: admin@OTUS.LAN

Valid starting       Expires              Service principal
04.02.2026 13:57:52  05.02.2026 13:31:28  krbtgt/OTUS.LAN@OTUS.LAN
```
- **[root@ipa ~]# kdestroy** # Удалим полученный билет
- ### Зашел с хоста (mac mini M4) на web-интерфейс IPA-сервера, завел пользователя
- 
<img width="1330" height="835" alt="Screenshot 2026-02-04 at 14 26 13" src="https://github.com/user-attachments/assets/b43a8e47-c507-49c2-8c03-b1938cbbd260" />
<img width="1341" height="571" alt="Screenshot 2026-02-04 at 14 28 14" src="https://github.com/user-attachments/assets/384222ac-e051-41d4-a1ed-079a03254247" />

- ### Настройка и подключение клиента

- **root@client1:~# timedatectl set-timezone Europe/Moscow** # Время
- **root@client1:~# update**
- **root@client1:~# apt install chrony** # Синхронизация
- **root@client1:~# apt update**
- **root@client1:~# apt install freeipa-client** # Установка клиента
- **root@client1:~# ipa-client-install --mkhomedir** # Настройка клиента
```bash
Provide the domain name of your IPA server (ex: example.com): otus.lan
Provide your IPA server name (ex: ipa.example.com): ipa.otus.lan
Proceed with fixed values and no DNS discovery? [no]: yes
Do you want to configure chrony with NTP server or pool address? [no]: yes
Enter NTP source server addresses separated by comma, or press Enter to skip:
Enter a NTP source pool address, or press Enter to skip:
Client hostname: client1.ptus.lan
Realm: OTUS.LAN
DNS Domain: otus.lan
IPA Server: ipa.otus.lan
BaseDN: dc=otus,dc=lan
Continue to configure the system with these values? [no]: yes
User authorized to enroll computers: admin
Password for admin@OTUS.LAN:

SSSD enabled
Configured /etc/openldap/ldap.conf
Configured /etc/ssh/ssh_config
Configured /etc/ssh/sshd_config.d/04-ipa.conf
Configuring otus.lan as NIS domain.
Configured /etc/krb5.conf for IPA realm OTUS.LAN
Client configuration complete.
The ipa-client-install command was successful
```
- **root@client1:~# kinit admin** # проверим, что клиент может получать билет от сервера
```bash
Password for admin@OTUS.LAN:
```
- **root@client1:~# klist** # проверяем, что билет получен
```bash
Ticket cache: KEYRING:persistent:0:0
Default principal: admin@OTUS.LAN

Valid starting       Expires              Service principal
02/04/2026 15:22:03  02/05/2026 15:04:55  krbtgt/OTUS.LAN@OTUS.LAN
```
### Клиент настроен.
### Использованный материал: https://www.dmosk.ru/miniinstruktions.php?mini=freeipa-centos#client


## 42 урок Динамический веб 
 

**Домашнее задание** <ins>"Развертывание веб приложения на ВМ с помощью принципа IaC (реализация серез Ansible)"</ins>

**Цель**: 
- **1. Получить практические навыки в настройке инфраструктуры с помощью манифестов и конфигураций;**
- **2. Отточить навыки использования ansible/docker;**
- **3. Использование методологий в построении информационных систем - Infrastructure as Code ( Инфраструктура как код, IaC )**

🎯 Что нужно сделать?
**1. Создать вариант стенда Вnginx + php-fpm (wordpress) + python (django) + js(node.js) с деплоем через docker-compose

- ### Так как у меня хостовая машина нам macOS (M4) и я использую ВМ созданные в vSphere часть связанную с их созданием опускаю (нет Vagrant)
- ### Структура (дерево) проекта на хосте:
```bash
➜  dynamicweb pwd
/Users/spg/Ansible/dynamicweb
➜  dynamicweb tree
.
├── inventory.ini
├── project
│   ├── docker-compose.yml
│   ├── nginx-conf
│   │   └── nginx.conf
│   ├── node
│   │   └── test.js
│   ├── python
│   │   ├── Dockerfile
│   │   ├── manahe.py
│   │   ├── mysite
│   │   │   ├── _init_.py
│   │   │   ├── settings.py
│   │   │   ├── urls.py
│   │   │   └── wsgi.py
│   │   └── requirements.txt
│   └── screens
└── prov.yml

6 directories, 13 files
```
### Содержание дерева снизу вверх:

- **➜  dynamicweb cat project/python/mysite/wsgi.py** 
```bash
import os
from django.core.wsgi import get_wsgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')
application = get_wsgi_application()
```
- **➜  dynamicweb cat project/python/mysite/urls.py**
```bash
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```
- ➜  **dynamicweb cat project/python/mysite/settings.py**
```bash
import os
import ast
from pathlib import Path

BASE_DIR = Path(__file__).resolve(strict=True).parent.parent
SECRET_KEY = os.getenv('MYSITE_SECRET_KEY', '')
DEBUG = ast.literal_eval(os.getenv('DEBUG', 'True'))
ALLOWED_HOSTS = ['*']
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'mysite.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'mysite.wsgi.application'
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]
LANGUAGE_CODE = 'en-us'
TIME_ZONE = 'UTC'
USE_I18N = True
USE_L10N = True
USE_TZ = True
STATIC_URL = '/static/'
```
- **➜  dynamicweb cat project/python/manahe.py**       
```bash
#!/usr/bin/env python
"""Django's command-line utility for administrative tasks."""
import os
import sys

def main():
    """Run administrative tasks."""
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')
    try:
        from django.core.management import execute_from_command_line
    except ImportError as exc:
        raise ImportError(
            "Couldn't import Django. Are you sure it's installed and "
            "available on your PYTHONPATH environment variable? Did you "
            "forget to activate a virtual environment?"
        ) from exc
    execute_from_command_line(sys.argv)

if __name__ == '__main__':
    main()
```
- **➜  dynamicweb cat project/python/requirements.txt**
```bash
Django==3.1
gunicorn==20.0.4
pytz==2020.1
```
- **➜  dynamicweb cat project/python/Dockerfile**
```bash
FROM python:3.8.3

ENV APP_ROOT /src
ENV CONFIG_ROOT /config

RUN mkdir ${CONFIG_ROOT}
COPY requirements.txt ${CONFIG_ROOT}/requirements.txt
RUN pip install -r ${CONFIG_ROOT}/requirements.txt

RUN mkdir ${APP_ROOT}
WORKDIR ${APP_ROOT}
ADD . ${APP_ROOT}
```
- **➜  dynamicweb cat project/node/test.js**
```bash
const http = require('http');
const hostname = '0.0.0.0';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello from node js server');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```
- **➜  dynamicweb cat project/nginx-conf/nginx.conf** 
```bash
# ===============================
# WORDPRESS (PHP-FPM)
# ===============================
server {
    listen 8083;
    listen [::]:8083;
    server_name localhost;

    index index.php index.html index.htm;
    root /var/www/html;

    location / {
        try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass wordpress:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }

    location = /favicon.ico {
        log_not_found off;
        access_log off;
    }

    location ~* \.(css|gif|ico|jpeg|jpg|js|png)$ {
        expires max;
        log_not_found off;
    }
}

# ===============================
# DJANGO (reverse proxy)
# ===============================
upstream django {
    server app:8000;
}

server {
    listen 8081;
    listen [::]:8081;
    server_name localhost;

    location / {
        try_files $uri @proxy_to_app;
    }

    location @proxy_to_app {
        proxy_pass http://django;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_redirect off;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Host $server_name;
    }
}

# ===============================
# NODE.JS
# ===============================
server {
    listen 8082;
    listen [::]:8082;
    server_name localhost;

    location / {
        proxy_pass http://node:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_redirect off;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Host $server_name;
    }
}
```
- **➜  dynamicweb cat project/docker-compose.yml**
```bash
version: '3.7'

services:

  database:
    image: mysql:8.0
    container_name: database
    restart: unless-stopped
    environment:
      MYSQL_DATABASE: ${DB_NAME}
      MYSQL_ROOT_PASSWORD: ${DB_ROOT_PASSWORD}
    volumes:
      - ./dbdata:/var/lib/mysql
    command: '--default-authentication-plugin=mysql_native_password'
    networks:
      - app-network

  wordpress:
    image: wordpress:5.1.1-fpm-alpine
    container_name: wordpress
    restart: unless-stopped
    environment:
      WORDPRESS_DB_HOST: database
      WORDPRESS_DB_NAME: ${DB_NAME}
      WORDPRESS_DB_USER: root
      WORDPRESS_DB_PASSWORD: ${DB_ROOT_PASSWORD}
    volumes:
      - ./wordpress:/var/www/html
    depends_on:
      - database
    networks:
      - app-network

  nginx:
    image: nginx:1.15.12-alpine
    container_name: nginx
    restart: unless-stopped
    ports:
      - "8083:8083"
      - "8081:8081"
      - "8082:8082"
    volumes:
      - ./wordpress:/var/www/html
      - ./nginx-conf:/etc/nginx/conf.d
    depends_on:
      - wordpress
      - app
      - node
    networks:
      - app-network

  app:
    build: ./python
    container_name: app
    restart: always
    env_file:
      - .env
    command: gunicorn --workers=2 --bind=0.0.0.0:8000 mysite.wsgi:application
    networks:
      - app-network

  node:
    image: node:16.13.2-alpine3.15
    container_name: node
    working_dir: /opt/server
    volumes:
      - ./node:/opt/server
    command: node test.js
    networks:
      - app-network

networks:
  app-network:
    driver: bridge
```
- **➜  dynamicweb cat prov.yml** 
```bash
- hosts: DynamicWeb
  become: yes
  gather_facts: yes

  tasks:

  - name: Install dependencies
    apt:
      name:
        - ca-certificates
        - curl
        - gnupg
      update_cache: yes
      state: present

  - name: Add Docker GPG key
    apt_key:
      url: https://download.docker.com/linux/ubuntu/gpg
      state: present

  - name: Add Docker repo
    apt_repository:
      repo: deb https://download.docker.com/linux/ubuntu noble stable
      state: present

  - name: Install Docker
    apt:
      name:
        - docker-ce
        - docker-ce-cli
        - containerd.io
      state: present
      update_cache: yes

  - name: Install docker compose plugin
    apt:
      name: docker-compose-plugin
      state: present

  - name: Add user to docker group
    user:
      name: "{{ ansible_user }}"
      groups: docker
      append: yes

  - name: Copy project
    copy:
      src: project
      dest: /home/{{ ansible_user }}/

  - name: Run containers
    shell: docker compose up -d --build
    args:
      chdir: /home/{{ ansible_user }}/project
```
- **➜  dynamicweb cat inventory.ini**
```bash
[DynamicWeb]
10.0.77.163 ansible_user=spg
```
- **➜  dynamicweb ansible-playbook -i inventory.ini prov.yml -k -K** # Запускаем задание
```bash
SSH password: 
BECOME password[defaults to SSH password]: 

PLAY [DynamicWeb] ****************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************
[WARNING]: Host '10.0.77.163' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.20/reference_appendices/interpreter_discovery.html for more information.
ok: [10.0.77.163]

TASK [Install dependencies] ******************************************************************************************************************
ok: [10.0.77.163]

TASK [Add Docker GPG key] ********************************************************************************************************************
ok: [10.0.77.163]

TASK [Add Docker repo] ***********************************************************************************************************************
ok: [10.0.77.163]

TASK [Install Docker] ************************************************************************************************************************
ok: [10.0.77.163]

TASK [Install docker compose plugin] *********************************************************************************************************
ok: [10.0.77.163]

TASK [Add user to docker group] **************************************************************************************************************
ok: [10.0.77.163]

TASK [Copy project] **************************************************************************************************************************
ok: [10.0.77.163]

TASK [Run containers] ************************************************************************************************************************
changed: [10.0.77.163]

PLAY RECAP ***********************************************************************************************************************************
10.0.77.163                : ok=9    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
### Проверяем
<img width="1055" height="856" alt="Screenshot 2026-02-16 at 11 24 37" src="https://github.com/user-attachments/assets/6a8026a1-95b2-4e9f-870c-f7812884af89" />

<img width="539" height="227" alt="Screenshot 2026-02-16 at 11 25 11" src="https://github.com/user-attachments/assets/8581d033-659e-4c32-b4b0-ce3a2e73e33f" />

<img width="806" height="858" alt="Screenshot 2026-02-16 at 11 25 42" src="https://github.com/user-attachments/assets/75a62f4c-dae8-41b4-b728-aff9ed3f67c1" />

## УРОК 44 MySQL: Backup + Репликация
- **Домашнее задание "Репликация mysql"**
- 🎯 Цель:
- **Научиться настраивать репликацию и создавать резервные копии в СУБД MySQL;** # 
- 🎯 Что нужно сделать?
- **Базу развернуть на мастере и настроить так, чтобы реплицировались таблицы**
- **настроить правильное резервное копирование**

- ### Выполнение
### 

### Делать не собирался, но в ходе подготовки к защите проекта встал перед выбором, какую СУБД использовать: Postgresql или MySQL.
### Выбор пал на последнюю, и так образовалось еще одно ДЗ, о чем ни разу не пожалел (не было столько мучений, как c psql)
### Использовал psql-master, web2-psql-replica и barman (master/replica/backup) без переименования дабы не изменять старой русской традиции (запутать врага %)
### Linux Ubuntu 24.04
### mysql  Ver 8.0.45-0ubuntu0.24.04.1 for Linux on x86_64 ((Ubuntu))
### Ansible тоже на Ubuntu (раньше оркестрация выполнялась с машины на MacOS, но появились сомнения в правильности такого выбора)
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# tree** # реализация на Ansible
```bash
.
├── inventory.ini
├── roles
│   ├── barman
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── files
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── README.md
│   │   ├── tasks
│   │   │   └── main.yml
│   │   ├── templates
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   ├── mysql_master
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── files
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── README.md
│   │   ├── tasks
│   │   │   ├── backup_user.yml
│   │   │   ├── config.yml
│   │   │   ├── db_init.yml
│   │   │   ├── main.yml
│   │   │   └── replication_user.yml
│   │   ├── templates
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   └── mysql_replica
│       ├── defaults
│       │   └── main.yml
│       ├── files
│       ├── handlers
│       │   └── main.yml
│       ├── meta
│       │   └── main.yml
│       ├── README.md
│       ├── tasks
│       │   ├── main.yml
│       │   ├── replication.yml
│       │   └── setup.yml
│       ├── templates
│       ├── tests
│       │   ├── inventory
│       │   └── test.yml
│       └── vars
│           └── main.yml
└── site.yml

29 directories, 32 files
```
### Выполняем стандартные настройки на хостах из проекта:
```bash
Сгенерировать ключ (если нет)
На машине с Ansible (192.168.50.2):

ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa
-------------------------------------------

Скопировать ключ на ВСЕ хосты
ssh-copy-id spg@192.168.50.16 # replica
ssh-copy-id spg@192.168.50.15 # master
ssh-copy-id spg@192.168.50.23 # backup
-------------------------------------------

Проверить доступ (ОБЯЗАТЕЛЬНО)

Проверка вручную:

ssh spg@192.168.50.15
ssh spg@192.168.50.16
ssh spg@192.168.50.23

Проверка через Ansible
ansible all -i inventory.ini -m ping
-------------------------------------------
```
### Содержимой файлов проекта (чистовики после нескольких дней ):
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat inventory.ini**
```bash
[mysql_master]
master ansible_host=192.168.50.15

[mysql_replica]
replica ansible_host=192.168.50.16

[mysql:children]
mysql_master
mysql_replica

[barman_server]
barman ansible_host=192.168.50.23

[all:vars]
ansible_user=spg
ansible_ssh_private_key_file=~/.ssh/id_rsa
ansible_python_interpreter=/usr/bin/python3.12
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat site.yml**
```bash
---
- name: MySQL Master
  hosts: master
  become: yes
  roles:
    - mysql_master

- name: Wait for MySQL master
  hosts: mysql_replica
  tasks:
    - wait_for:
        host: 192.168.50.15
        port: 3306
        timeout: 60

- name: MySQL Replica
  hosts: replica
  become: yes
  roles:
    - role: mysql_replica
      vars:
        mysql_replica_mode: rebuild

- name: Barman Backup
  hosts: barman
  become: yes
  roles:
    - barman
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat roles/mysql_master/tasks/main.yml**
```bash
---
- name: Install MySQL server
  tags: install
  apt:
    name:
      - mysql-server
      - python3-pymysql
    state: present
    update_cache: yes

- name: Ensure MySQL started
  tags: service
  service:
    name: mysql
    state: started
    enabled: yes

- name: Configure MySQL
  tags: config
  import_tasks: config.yml

- name: Restart MySQL after config
  tags: service
  service:
    name: mysql
    state: restarted

- name: Wait for MySQL
  tags: wait
  wait_for:
    port: 3306
    timeout: 30

- name: Initialize databases and users
  tags: users
  import_tasks: replication_user.yml

- name: Initialize databases
  tags: db
  import_tasks: db_init.yml

- name: Initialize backup user
  tags: users
  import_tasks: backup_user.yml
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat roles/mysql_master/tasks/config.yml**
```bash
---
- name: Configure bind address
  lineinfile:
    path: /etc/mysql/mysql.conf.d/mysqld.cnf
    regexp: '^bind-address'
    line: 'bind-address = 0.0.0.0'

- name: Enable binary logging
  blockinfile:
    path: /etc/mysql/mysql.conf.d/mysqld.cnf
    block: |
      server-id = 1
      log_bin = /var/log/mysql/mysql-bin.log
      binlog_format = ROW
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat roles/mysql_master/tasks/db_init.yml**
```bash
---
- name: Create application database
  community.mysql.mysql_db:
    name: appdb
    state: present
    login_user: root
    login_unix_socket: /var/run/mysqld/mysqld.sock

- name: Create application user
  community.mysql.mysql_user:
    name: "{{ mysql_app_user }}"
    password: "{{ mysql_app_password }}"
    priv: "appdb.*:ALL"
    host: "%"
    state: present
    login_unix_socket: /var/run/mysqld/mysqld.sock
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat roles/mysql_master/tasks/replication_user.yml**
```bash
- name: Create replication user
  community.mysql.mysql_user:
    name: "{{ mysql_repl_user }}"
    password: "{{ mysql_repl_password }}"
    priv: "*.*:REPLICATION SLAVE"
    host: "%"
    state: present
    login_unix_socket: /var/run/mysqld/mysqld.sock
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat roles/mysql_master/tasks/backup_user.yml**
```bash
- name: Create backup user
  community.mysql.mysql_user:
    name: "{{ mysql_backup_user }}"
    password: "{{ mysql_backup_password }}"
    host: "%"
    priv: "*.*:PROCESS,SELECT,LOCK TABLES,SHOW VIEW"
    state: present
    login_unix_socket: /var/run/mysqld/mysqld.sock
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat roles/mysql_master/defaults/main.yml**
```bash
---
mysql_app_user: appuser
mysql_app_password: app63

mysql_repl_user: repl
mysql_repl_password: repl63

mysql_backup_user: backup
mysql_backup_password: backup63
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat roles/mysql_master/handlers/main.yml**
```bash
---
# handlers file for mysql_master
- name: Restart MySQL
  service:
    name: mysql
    state: restarted
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat roles/mysql_replica/tasks/main.yml**
```bash
---
- import_tasks: setup.yml
- import_tasks: replication.yml
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat roles/mysql_replica/tasks/setup.yml**
```bash
---
- name: Install Python MySQL dependencies
  apt:
    name:
      - python3-pymysql
      - python3-mysqldb
    state: present
    update_cache: yes

- name: Install MySQL
  apt:
    name: mysql-server
    state: present
    update_cache: yes

- name: Start MySQL
  service:
    name: mysql
    state: started
    enabled: yes

- name: Configure server-id
  lineinfile:
    path: /etc/mysql/mysql.conf.d/mysqld.cnf
    regexp: '^server-id'
    line: 'server-id = 2'
  notify: Restart MySQL
```
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# cat roles/mysql_replica/tasks/replication.yml**
```bash
---
- name: Stop replication
  community.mysql.mysql_replication:
    mode: stopreplica
    login_user: root
    login_unix_socket: /var/run/mysqld/mysqld.sock
  when: mysql_replica_mode in ["init", "rebuild"]

- name: Reset replication
  community.mysql.mysql_replication:
    mode: resetreplicaall
    login_user: root
    login_unix_socket: /var/run/mysqld/mysqld.sock
  when: mysql_replica_mode in ["init", "rebuild"]

- name: Dump all databases from master
  delegate_to: 192.168.50.15
  shell: >
    mysqldump --all-databases
    --single-transaction
    --routines --events --triggers
    --source-data=2 > /tmp/full.sql
  when: mysql_replica_mode in ["init", "rebuild"]

- name: Fetch dump to controller
  delegate_to: 192.168.50.15
  fetch:
    src: /tmp/full.sql
    dest: /tmp/full.sql
    flat: yes
  when: mysql_replica_mode in ["init", "rebuild"]

- name: Copy dump to replica
  copy:
    src: /tmp/full.sql
    dest: /tmp/full.sql
  when: mysql_replica_mode in ["init", "rebuild"]

- name: Import dump
  community.mysql.mysql_db:
    state: import
    name: all
    target: /tmp/full.sql
    login_user: root
    login_unix_socket: /var/run/mysqld/mysqld.sock
  when: mysql_replica_mode in ["init", "rebuild"]

- name: Get master status
  delegate_to: 192.168.50.15
  community.mysql.mysql_replication:
    mode: getprimary
  register: master_status
  when: mysql_replica_mode in ["init", "rebuild"]

- name: Configure replication source
  community.mysql.mysql_replication:
    mode: changeprimary
    master_host: "192.168.50.15"
    master_user: "repl"
    master_password: "repl63"
    master_log_file: "{{ master_status.File }}"
    master_log_pos: "{{ master_status.Position }}"
    login_user: root
    login_unix_socket: /var/run/mysqld/mysqld.sock
  when: mysql_replica_mode in ["init", "rebuild"]

- name: Start replication
  community.mysql.mysql_replication:
    mode: startreplica
    login_user: root
    login_unix_socket: /var/run/mysqld/mysqld.sock
  when: mysql_replica_mode in ["init", "rebuild", "start"]
```
### Протокол исполнения 
- **root@ansible:/home/spg/Ansible1603/Ansible/mysql# ansible-playbook -i inventory.ini site.yml -K**
```bash
BECOME password:

PLAY [MySQL Master] *****************************************************************************************************

TASK [Gathering Facts] **************************************************************************************************
ok: [master]

TASK [mysql_master : Install MySQL server] ******************************************************************************
ok: [master]

TASK [mysql_master : Ensure MySQL started] ******************************************************************************
ok: [master]

TASK [mysql_master : Configure bind address] ****************************************************************************
ok: [master]

TASK [mysql_master : Enable binary logging] *****************************************************************************
ok: [master]

TASK [mysql_master : Restart MySQL after config] ************************************************************************
changed: [master]

TASK [mysql_master : Wait for MySQL] ************************************************************************************
ok: [master]

TASK [mysql_master : Create replication user] ***************************************************************************
[WARNING]: Option column_case_sensitive is not provided. The default is now false, so the column's name will be
uppercased. The default will be changed to true in community.mysql 4.0.0.
changed: [master]

TASK [mysql_master : Create application database] ***********************************************************************
ok: [master]

TASK [mysql_master : Create application user] ***************************************************************************
ok: [master]

TASK [mysql_master : Create replication user] ***************************************************************************
changed: [master]

TASK [mysql_master : Create barman user] ********************************************************************************
ok: [master]

TASK [mysql_master : Create backup user for mysqldump] ******************************************************************
ok: [master]

PLAY [Wait for MySQL master] ********************************************************************************************

TASK [Gathering Facts] **************************************************************************************************
ok: [replica]

TASK [wait_for] *********************************************************************************************************
ok: [replica]

PLAY [MySQL Replica] ****************************************************************************************************

TASK [Gathering Facts] **************************************************************************************************
ok: [replica]

TASK [mysql_replica : Install Python MySQL dependencies] ****************************************************************
ok: [replica]

TASK [mysql_replica : Install MySQL] ************************************************************************************
ok: [replica]

TASK [mysql_replica : Start MySQL] **************************************************************************************
ok: [replica]

TASK [mysql_replica : Configure server-id] ******************************************************************************
ok: [replica]

TASK [mysql_replica : Stop replication] *********************************************************************************
changed: [replica]

TASK [mysql_replica : Reset replication] ********************************************************************************
changed: [replica]

TASK [mysql_replica : Configure replication source] *********************************************************************
changed: [replica]

TASK [mysql_replica : Start replication] ********************************************************************************
changed: [replica]

PLAY [Barman Backup] ****************************************************************************************************

TASK [Gathering Facts] **************************************************************************************************
ok: [barman]

TASK [barman : Install mysql client] ************************************************************************************
ok: [barman]

TASK [barman : Create backup directory] *********************************************************************************
ok: [barman]

TASK [barman : Create mysql backup script] ******************************************************************************
ok: [barman]

TASK [barman : Schedule backup cron] ************************************************************************************
ok: [barman]

PLAY RECAP **************************************************************************************************************
barman                     : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
master                     : ok=13   changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
replica                    : ok=11   changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

🔁 1. ПРОВЕРКА РЕПЛИКАЦИИ
### Проверка показала:
```bash
- репликация запущена, но не идет (Replica_IO_Running: Yes
          Replica_SQL_Running: No)
- Source_Log_File и Exec_Source_Log_Pos - не соотвествует текущему на мастере
- appdb.test_replica - не создается на replica
```
### Внес изменения в роль mysql_replica под различные условия, согласно которым будут или нет копироваться уже существующие БД с мастера на реплику (сценарий выхода из строя машины реплики):
```bash
ansible-playbook -i inventory.ini site.yml -e mysql_replica_mode=rebuild -K # -e "mysql_replica_mode=rebuild"можно было не указывать, так уже прописано в главном файле
init → первичное разворачивание
rebuild → пересоздание реплики
start → просто запуск/подключение
stop → обслуживание
```
### Изменения отразил выше (поправил)

📍 на master
- **root@psql-master:~# sudo mysql**
```bash
Welcome to the MySQL monitor.  Commands end with ; or \g.
mysql> SHOW MASTER STATUS;
+------------------+----------+--------------+------------------+-------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+------------------+----------+--------------+------------------+-------------------+
| mysql-bin.000018 |      717 |              |                  |                   |
+------------------+----------+--------------+------------------+-------------------+
1 row in set (0.00 sec)

mysql> mysql> INSERT INTO appdb.test_replica VALUES (7);

Query OK, 1 row affected (0.00 sec)
```
📍 на replica
-**root@web2-psql-replica:~# sudo mysql**
```bash
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 169
Server version: 8.0.45-0ubuntu0.24.04.1 (Ubuntu)

mysql> SHOW REPLICA STATUS\G
Relay_Source_Log_File: mysql-bin.000018
Replica_IO_Running: Yes
Replica_SQL_Running: Yes
Exec_Source_Log_Pos: 717

mysql> SELECT * FROM appdb.test_replica;
+------+
| id   |
+------+
|    1 |
|    2 |
|    3 |
|    4 |
|    5 |
|    6 |
|    7 |
+------+
7 rows in set (0.00 sec)
```
🔁 1. ПРОВЕРКА БЭКАПА
-**root@barman:~# ls -lh /backup/mysql** # немного накопилось...болел
```bash
total 36K
-rw-r--r-- 1 root root    0 Mar 21 15:42 appdb_2026-03-21_15-42.sql
-rw-r--r-- 1 root root    0 Mar 21 16:11 appdb_2026-03-21_16-11.sql
-rw-r--r-- 1 root root    0 Mar 22 02:00 appdb_2026-03-22_02-00.sql
-rw-r--r-- 1 root root    0 Mar 22 09:58 appdb_2026-03-22_09-58.sql
-rw-r--r-- 1 root root    0 Mar 22 10:02 appdb_2026-03-22_10-02.sql
-rw-r--r-- 1 root root 1.3K Mar 22 12:22 appdb_2026-03-22_12-22.sql
-rw-r--r-- 1 root root 1.9K Mar 22 12:52 appdb_2026-03-22_12-52.sql
-rw-r--r-- 1 root root 1.9K Mar 22 13:13 appdb_2026-03-22_13-13.sql
-rw-r--r-- 1 root root 1.9K Mar 22 13:19 appdb_2026-03-22_13-19.sql
-rw-r--r-- 1 root root 1.9K Mar 22 13:22 appdb_2026-03-22_13-22.sql
-rw-r--r-- 1 root root 1.9K Mar 22 13:23 appdb_2026-03-22_13-23.sql
-rw-r--r-- 1 root root 1.9K Mar 23 02:00 appdb_2026-03-23_02-00.sql
-rw-r--r-- 1 root root 1.9K Mar 24 02:00 appdb_2026-03-24_02-00.sql
-rw-r--r-- 1 root root 1.9K Mar 25 02:00 appdb_2026-03-25_02-00.sql
```
-**root@barman:~# bash -x /usr/local/bin/mysql_backup.sh** # проверка работы
```bash
++ date +%F_%H-%M
+ DATE=2026-03-25_17-43
+ BACKUP_DIR=/backup/mysql
+ FILE=/backup/mysql/appdb_2026-03-25_17-43.sql
+ mysqldump -h 192.168.50.15 -u backup -pbackup63 appdb
mysqldump: [Warning] Using a password on the command line interface can be insecure.
+ find /backup/mysql -type f -mtime +7 -delete
```
-**root@barman:~# ls -lh /backup/mysql**
```bash
total 40K
-rw-r--r-- 1 root root    0 Mar 21 15:42 appdb_2026-03-21_15-42.sql
-rw-r--r-- 1 root root    0 Mar 21 16:11 appdb_2026-03-21_16-11.sql
-rw-r--r-- 1 root root    0 Mar 22 02:00 appdb_2026-03-22_02-00.sql
-rw-r--r-- 1 root root    0 Mar 22 09:58 appdb_2026-03-22_09-58.sql
-rw-r--r-- 1 root root    0 Mar 22 10:02 appdb_2026-03-22_10-02.sql
-rw-r--r-- 1 root root 1.3K Mar 22 12:22 appdb_2026-03-22_12-22.sql
-rw-r--r-- 1 root root 1.9K Mar 22 12:52 appdb_2026-03-22_12-52.sql
-rw-r--r-- 1 root root 1.9K Mar 22 13:13 appdb_2026-03-22_13-13.sql
-rw-r--r-- 1 root root 1.9K Mar 22 13:19 appdb_2026-03-22_13-19.sql
-rw-r--r-- 1 root root 1.9K Mar 22 13:22 appdb_2026-03-22_13-22.sql
-rw-r--r-- 1 root root 1.9K Mar 22 13:23 appdb_2026-03-22_13-23.sql
-rw-r--r-- 1 root root 1.9K Mar 23 02:00 appdb_2026-03-23_02-00.sql
-rw-r--r-- 1 root root 1.9K Mar 24 02:00 appdb_2026-03-24_02-00.sql
-rw-r--r-- 1 root root 1.9K Mar 25 02:00 appdb_2026-03-25_02-00.sql
-rw-r--r-- 1 root root 1.9K Mar 25 17:43 appdb_2026-03-25_17-43.sql
```
-**root@barman:~# head -n 20 /backup/mysql/appdb_2026-03-25_02-00.sql** # Проверка содержимого бэкапа
```bash
-- MySQL dump 10.13  Distrib 8.0.45, for Linux (x86_64)
--
-- Host: 192.168.50.15    Database: appdb
-- ------------------------------------------------------
-- Server version	8.0.45-0ubuntu0.24.04.1

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!50503 SET NAMES utf8mb4 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Table structure for table `test_replica`
--
```
🔁 1. ПРОВЕРКА ВОССТАНОВЛЕНИЯ
- **root@barman:~# scp /backup/mysql/appdb_2026-03-25_02-00.sql spg@192.168.50.16:/tmp/** копируем нужный дамп на реплику (потому что там будем восстанавливать как тест)
```bash
spg@192.168.50.16's password:
appdb_2026-03-25_02-00.sql       100% 1891     5.3MB/s   00:00
```
- **root@web2-psql-replica:~# mysql test_restore <  /tmp/appdb_2026-03-25_02-00.sql**
- **root@web2-psql-replica:~# sudo mysql**
```bash
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| appdb              |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| test_restore       |
+--------------------+
6 rows in set (0.01 sec)

mysql> USE test_restore;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> SHOW TABLES;
+------------------------+
| Tables_in_test_restore |
+------------------------+
| test_replica           |
+------------------------+
1 row in set (0.00 sec)
```
### Восстановилось, поставленный цели достигнуты

## УРОК 46 Postgres SQL: Backup + Репликация 

- **Домашнее задание "Репликация postgres"**
- 🎯 Цель:
- **Научиться настраивать репликацию и создавать резервные копии в СУБД PostgreSQL;**
- 🎯 Что нужно сделать?
- **настроить hot_standby репликацию с использованием слотов**
- **настроить правильное резервное копирование**
- 
<details>
<summary> = Теория = </summary>
	
1️⃣ Hot standby

```bash
Hot standby — это режим работы слейв-сервера (реплики) PostgreSQL, когда:

Слейв постоянно получает WAL (Write-Ahead Logging) записи от мастера.

Слейв может принимать только SELECT-запросы (чтение).

Все изменения на мастере автоматически применяются на слейве.

Можно использовать слейв для чтения нагрузки, резервного копирования и быстрого переключения в случае падения мастера.
```

- ⚡ Главное: слейв живой и готов к работе → отсюда и название “hot”.

2️⃣ Репликация с использованием слотов (replication slots)

```bash
Replication slot — это объект на мастере, который:

“Запоминает” позицию слейва в WAL.

Гарантирует, что мастер не удалит WAL до того, как слейв его применит.

Предотвращает потерю данных при временной недоступности слейва.

То есть слоты делают репликацию безопасной, даже если слейв на время отключился.
```

3️⃣ Как это работает вместе

```bash
На мастере создаётся слот репликации:

SELECT * FROM pg_create_physical_replication_slot('slot1');

На слейве в postgresql.conf настраивают:

primary_conninfo = 'host=MASTER_IP port=5432 user=replicator password=***'
primary_slot_name = 'slot1'
hot_standby = on

Слейв подключается к мастеру, использует слот:

Получает WAL записи, начиная с позиции слота.

Если слейв временно отключился — мастер сохраняет WAL для него.

Когда слейв снова подключается, догоняет мастер и применяет все изменения.
```

4️⃣ Преимущества

```bash
Безопасность данных — WAL не потеряется даже если слейв недоступен.

Горячая репликация — можно читать данные с реплики.

Быстрое переключение на слейв при падении мастера.
```

5️⃣ Важные моменты

```bash
Реплика с hot_standby не может писать, только читать.

Нужно контролировать количество и размер WAL, чтобы слоты не переполнялись.

После создания слота удалять его аккуратно, иначе WAL будут накапливаться и дисковое пространство уйдёт.
```
</details>

- ### Выполнение
- создал три ВМ:
- web1-psql-master 192.168.50.15 # из урока DNS (для проекта)
- web2-psql-replica 192.168.50.16 # из урока DNS (для проекта)
- barman-graylog-zabbix 192.168.50.23 новая (для проекта)

<img width="1229" height="471" alt="Screenshot 2026-03-12 at 16 57 06" src="https://github.com/user-attachments/assets/8a6e0dc4-f846-4327-aa90-ec229a2c3366" />

- **root@web1-psql-master:~# apt update** # обновляем список пакетов
- **root@web1-psql-master:~# apt upgrade -y** # обновляем пакеты по списку
- **root@web1-psql-master:~# apt search postgresql-** # ищем доступные 
- **root@web1-psql-master:~# apt install postgresql postgresql-contrib** # устанавливаем последнюю доступную (без опыта потому что)
- **root@web1-psql-master:~# systemctl start postgresql** #  стартуем
- **root@web1-psql-master:~# systemctl enable postgresql** # включаем автозапуск при загрузке системы
- **root@web1-psql-master:~# systemctl status postgresql** # проверяем состояние

```bash
● postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/usr/lib/systemd/system/postgresql.service; enabled; preset: enabled)
     Active: active (exited) since Fri 2026-03-13 09:17:59 MSK; 1min 17s ago
   Main PID: 16190 (code=exited, status=0/SUCCESS)
        CPU: 967us
```

- **root@web1-psql-master:~# psql --version** # смотрим версию psql
```bash
psql (PostgreSQL) 16.13 (Ubuntu 16.13-0ubuntu0.24.04.1)
```
- **root@web2-psql-replica:~# psql --version** # на машине web2-psql-replica выполняем те же действия по установке psql и проверяем версию (совпадают)
```bash
psql (PostgreSQL) 16.13 (Ubuntu 16.13-0ubuntu0.24.04.1)
```
- ### Действия на машине web1-psql-master (MASTER DB)

- **root@web1-psql-master:~# sudo -u postgres psql** # подключимся к PostgreSQL
- **postgres=#**
- **postgres=# \l** # Посмотрим БД, все стандартные

```bash
                                                       List of databases
   Name    |  Owner   | Encoding | Locale Provider |   Collate   |    Ctype    | ICU Locale | ICU Rules |   Access privileges
-----------+----------+----------+-----------------+-------------+-------------+------------+-----------+-----------------------
 postgres  | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           |
 template0 | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | =c/postgres          +
           |          |          |                 |             |             |            |           | postgres=CTc/postgres
 template1 | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | =c/postgres          +
           |          |          |                 |             |             |            |           | postgres=CTc/postgres
(3 rows)

(END)
```
- **postgres=# \dt** # посмотрим таблицы, их нет
```bash
Did not find any relations.
```
- **postgres=# CREATE TABLE garantusers (
    id SERIAL PRIMARY KEY,
    name TEXT,
    age INT
);** # создадим свою таблицу в БД postdres
```bash
CREATE TABLE
```
- **postgres=# \dt** # теперь есть одна таблица
```bash
  List of relations
 Schema |    Name     | Type  |  Owner
--------+-------------+-------+----------
 public | garantusers | table | postgres
(1 row)
```
- **postgres=# INSERT INTO garantusers (name, age) VALUES ('Pavel', 63);** # добавим запись в таблицу из двух полей
```bash
INSERT 0 1
```
- **postgres=# INSERT INTO garantusers (name, age) VALUES ('Oleg', 39);** # --"--
```bash
INSERT 0 1
```
- **postgres=# SELECT * FROM garantusers;**
```bash
 id | name  | age
----+-------+-----
  1 | Pavel |  63
  2 | Oleg  |  39
(2 rows)
``` 
- **postgres=# \d garantusers** # Проверка структуры таблицы
```bash
                            Table "public.garantusers"
 Column |  Type   | Collation | Nullable |                 Default
--------+---------+-----------+----------+-----------------------------------------
 id     | integer |           | not null | nextval('garantusers_id_seq'::regclass)
 name   | text    |           |          |
 age    | integer |           |          |
Indexes:
    "garantusers_pkey" PRIMARY KEY, btree (id)
```
- ### Далее приступаем к настройке репликации: 
- **postgres=# CREATE USER replicator WITH REPLICATION Encrypted PASSWORD 'Otus2026!';** # В psql создаём пользователя replicator c правами репликации и паролем «Otus2026!»
```bash
CREATE ROLE
```
- **postgres=# SHOW config_file;** # проверяем, где расположен наш конфигурационный файл
```bash
			   config_file
-----------------------------------------
 /etc/postgresql/16/main/postgresql.conf
(1 row)
```
- **postgres=# quit**
- **root@web1-psql-master:~# vim /etc/postgresql/16/main/postgresql.conf** # указываем следующие параметры:
```bash
listen_addresses = 'localhost,192.168.50.15'            # what IP address(es) to listen on;
port = 5432                             # (change requires restart)
max_connections = 100                   # (change requires restart)
log_timezone = 'Europe/Moscow'
hot_standby = on                        # "off" disallows queries during recovery
wal_level = replica                     # minimal, replica, or logical
max_wal_senders = 3                     # max number of walsender processes
max_replication_slots = 3               # max number of replication slots
hot_standby_feedback = on               # send info from standby to prevent
password_encryption = scram-sha-256     # scram-sha-256 or md5
```
- **root@web1-psql-master:~# vim /etc/postgresql/16/main/pg_hba.conf** # в файле управления доступом добавляем две последние строки, которые разрешают репликацию пользователю replicator (в методичке ошибка - replication).
```bash
host    replication replicator         192.168.50.15/32        scram-sha-256
host    replication replicator         192.168.50.16/32        scram-sha-256
```
- **root@web1-psql-master:~# systemctl restart postgresql** # Перезапускаем postgresql-server

### Действия на машине web2-psql-replica (REPLICA DB)

- **root@web2-psql-replica:~# systemctl stop postgresql** # Останавливаем postgresql-server
- **root@web2-psql-replica:~# ls /var/lib/postgresql/16/main/** # директория данных
base          pg_dynshmem   pg_notify    pg_snapshots  pg_subtrans  PG_VERSION  postgresql.auto.conf
global        pg_logical    pg_replslot  pg_stat       pg_tblspc    pg_wal      postmaster.opts
pg_commit_ts  pg_multixact  pg_serial    pg_stat_tmp   pg_twophase  pg_xact
- **root@web2-psql-replica:~# sudo rm -rf /var/lib/postgresql/16/main/*** # очищаем директорию данных (в методичке пропущено)
- **root@web2-psql-replica:~# pg_basebackup -h 192.168.50.15 -U replicator -D /var/lib/postgresql/16/main -R -P** # копируем БД с мастера на реплику утилитой pg_basebackup (в методичке пропущен пользователь replicator)
```bash
Password: Otus2026!
23249/23249 kB (100%), 1/1 tablespace
```
- **root@web2-psql-replica:~# ls /var/lib/postgresql/16/main** # директория данных после копирования
```bash
backup_label     pg_commit_ts  pg_notify     pg_stat      pg_twophase  postgresql.auto.conf
backup_manifest  pg_dynshmem   pg_replslot   pg_stat_tmp  PG_VERSION   standby.signal
base             pg_logical    pg_serial     pg_subtrans  pg_wal
global           pg_multixact  pg_snapshots  pg_tblspc    pg_xact
```
- **root@web2-psql-replica:~# vim  /etc/postgresql/16/main/postgresql.conf** # меняем одну строку
```bash
listen_addresses = 'localhost, 192.168.50.16'           # what IP address(es) to listen on;
```
- **root@web2-psql-replica:~# sudo systemctl start postgresql**

- **root@web2-psql-replica:~# sudo -u postgres psql**
- **psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: No such file or directory
	Is the server running locally and accepting connections on that socket?**
- ### На Ubuntu 22.04+ и PostgreSQL 16 сервер на слейве не стартует просто через systemctl start postgresql, потому что systemd unit postgresql.service просто поднимает кластеры, но если они уже существуют как hot_standby — service завершается exited. Видимо, этого не было в 14 версии и поэтому не отражено в методичке)
- **root@web2-psql-replica:~# sudo systemctl start postgresql@16-main**
- **root@web2-psql-replica:~# sudo systemctl status postgresql@16-main**
```bash
● postgresql@16-main.service - PostgreSQL Cluster 16-main
     Loaded: loaded (/usr/lib/systemd/system/postgresql@.service; enabled-runtime; preset: enabled)
     Active: active (running) since Fri 2026-03-13 12:50:24 MSK; 19min ago
```
- ### Действия на машине web1-psql-master (MASTER DB)
- **root@web1-psql-master:~# sudo -u postgres psql
psql (16.13 (Ubuntu 16.13-0ubuntu0.24.04.1))
Type "help" for help.**

- **postgres=# CREATE DATABASE otus_test;
CREATE DATABASE
postgres=# \l** Создали новую БД otus-test
```bash
                                                       List of databases
   Name    |  Owner   | Encoding | Locale Provider |   Collate   |    Ctype    | ICU Locale | ICU Rules |   Access privileges
-----------+----------+----------+-----------------+-------------+-------------+------------+-----------+-----------------------
 otus_test | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           |
 postgres  | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           |
 template0 | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | =c/postgres          +
           |          |          |                 |             |             |            |           | postgres=CTc/postgres
 template1 | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | =c/postgres          +
           |          |          |                 |             |             |            |           | postgres=CTc/postgres
(4 rows)

(END)
```
- ### Действия на машине web2-psql-replica (REPLICA DB)
- **root@web2-psql-replica:~# sudo -u postgres psql**
```bash
psql (16.13 (Ubuntu 16.13-0ubuntu0.24.04.1))
Type "help" for help.
```
- **postgres=# \l** # Увидели созданную на MASTER БД, репликация работает

```bash                                                       List of databases
   Name    |  Owner   | Encoding | Locale Provider |   Collate   |    Ctype    | ICU Locale | ICU Rules |   Access privileges
-----------+----------+----------+-----------------+-------------+-------------+------------+-----------+-----------------------
 otus_test | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           |
 postgres  | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           |
 template0 | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | =c/postgres          +
           |          |          |                 |             |             |            |           | postgres=CTc/postgres
 template1 | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | =c/postgres          +
           |          |          |                 |             |             |            |           | postgres=CTc/postgres
(4 rows)

(END)
```
- ### Дополнительный проверки репликации

- ### Действия на машине web1-psql-master (MASTER DB)
- **postgres=# select * from pg_stat_replication;**
```bash
  pid  | usesysid |  usename   | application_name |  client_addr  | client_hostname | client_port |         backend_start         | backend_xmin |   state   | sent_lsn  | write_lsn | flush_lsn | replay_lsn |    write_lag    |    flush_lag    |   replay_lag    | sync_priority | sync_state |          reply_time
-------+----------+------------+------------------+---------------+-----------------+-------------+-------------------------------+--------------+-----------+-----------+-----------+-----------+------------+-----------------+-----------------+-----------------+---------------+------------+-------------------------------
 18225 |    16397 | replicator | 16/main          | 192.168.50.16 |                 |       60866 | 2026-03-13 12:50:22.562685+03 |              | streaming | 0/342DAC8 | 0/342DAC8 | 0/342DAC8 | 0/342DAC8  | 00:00:00.000269 | 00:00:00.000585 | 00:00:00.000688 |             0 | async      | 2026-03-13 12:52:39.277268+03
(1 row)
```
- ### Действия на машине web2-psql-replica (REPLICA DB)
- **select * from pg_stat_wal_receiver;**
```bash
...skipping...
 pid  |  status   | receive_start_lsn | receive_start_tli | written_lsn | flushed_lsn | received_tli |      last_msg_send_time       |     last_msg_receipt_time     | latest_end_lsn |        latest_end_time        | slot_name |  sender_host  | sender_port |                                                                                                                                                                     conninfo
-------+-----------+-------------------+-------------------+-------------+-------------+--------------+-------------------------------+-------------------------------+----------------+-------------------------------+-----------+---------------+-------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 17363 | streaming | 0/3000000         |                 1 | 0/342DAC8   | 0/342DAC8   |            1 | 2026-03-13 12:52:39.276428+03 | 2026-03-13 12:52:39.276806+03 | 0/342DAC8      | 2026-03-13 12:52:39.276428+03 |           | 192.168.50.15 |        5432 | user=replicator password=******** channel_binding=prefer dbname=replication host=192.168.50.15 port=5432 fallback_application_name=16/main sslmode=prefer sslcompression=0 sslcertmode=allow sslsni=1 ssl_min_protocol_version=TLSv1.2 gssencmode=prefer krbsrvname=postgres gssdelegation=0 target_session_attrs=any load_balance_hosts=disable
(1 row)

```
- ### На этом настройка репликации завершена. 

- ### В случае выхода из строя master-хоста (node1), на slave-сервере (node2) в psql необхоимо выполнить команду select pg_promote(); Также можно создать триггер-файл. Если в дальнейшем хост node1 заработает корректно, то для восстановления его работы (как master-сервера) необходимо наастроить сервер node1 как slave-сервер. Также с помощью команды select pg_promote(); перевести режим его работы в master.

- ### Действия на машине web2-psql-replica (REPLICA DB)

-** postgres=# SELECT pg_is_in_recovery();
 pg_is_in_recovery
-------------------
- t - **слейв в режиме репликации.**
- (1 row)**
- ### Действия на машине web1-psql-master (MASTER DB)

- **root@web1-psql-master:~# shutdown now** # выводим из строя мастера

- ### Действия на машине web2-psql-replica (REPLICA DB)

- **postgres=# SELECT pg_promote(wait_seconds => 60);
 pg_promote
------------**
```bash
-  t - **промоуция завершена**
- (1 row)
```  
**postgres=# SELECT pg_is_in_recovery();
 pg_is_in_recovery
-------------------**
-  f - **значит слейв стал полноценным мастером (read-write).**
- (1 row)
- **postgres=# \dt**
```bash
            List of relations
 Schema |    Name     | Type  |  Owner
--------+-------------+-------+----------
 public | garantusers | table | postgres
(1 row)**
```
- **postgres=# INSERT INTO garantusers (name, age) VALUES ('Mariya', 63);** # попробуем записать
- INSERT 0 1
- **postgres=# SELECT * FROM garantusers; # проверка что запись добавилась**
```bash
 id |  name  | age
----+--------+-----
  1 | Pavel  |  63
  2 | Oleg   |  39
  3 | Test   |  99
  4 | Mariya |  63
(4 rows)**
```
- ### web1-psql-master (MASTER DB) "восстановили" и нужно вернуться к первоначальной схеме
- ### Действия на машине web2-psql-replica (REPLICA DB)
- ### Перенесем данные, которые добавили на slave
- **root@web2-psql-replica:~# sudo -u postgres pg_dump -Fc -f /tmp/garantusers.dump postgres** # дамп нашей таблицы
- **root@web2-psql-replica:~# sudo -u postgres pg_dumpall -f /tmp/all_data.sql** # или все БД ...
- **root@web2-psql-replica:~# scp /tmp/garantusers.dump spg@192.168.50.15:/tmp/** # Передадимм данные на master
```bash
spg@192.168.50.15's password:
garantusers.dump                                                 100% 3049     9.0MB/s   00:00
```
- ### Действия на машине web1-psql-master (MASTER DB)
- **root@web1-psql-master:~# sudo -u postgres pg_restore --clean -d postgres /tmp/garantusers.dump**
- **root@web1-psql-master:~# sudo -u postgres psql**
```bash
psql (16.13 (Ubuntu 16.13-0ubuntu0.24.04.1))
Type "help" for help.
```
- **postgres=# SELECT * FROM garantusers;** # выровняли
```bash
 id |  name  | age
----+--------+-----
  1 | Pavel  |  63
  2 | Oleg   |  39
  3 | Test   |  99
  4 | Mariya |  63
(4 rows)
```
- ### Эту тему до конца довести не удалось (она и не была заявлена к выполнению в ДЗ). Нужно отдельно разбираться в восстановлении данных на мастере и приведении репликации в исходное положение после промоушена реплики в отдельный мастер. Стало понятно, что одним  select "pg_promote()" это не решить. Интересная тема для администратора баз данных.
  
- ### Настройка резервного копирования
- **root@web1-psql-master:~# apt install barman-cli**

- **root@web2-psql-replica:~# apt install barman-cli**

- **root@barmen-graylog-zabbix:~# apt install barman-cli barman postgresql**

### Создаем ключи и обмениваемся публичными меджу мастером и бекапом
- **root@barmen-graylog-zabbix:~# su barman**
- **barman@barmen-graylog-zabbix:/root$ cd**
- **barman@barmen-graylog-zabbix:~$ pwd**
/var/lib/barman
- **barman@barmen-graylog-zabbix:~$ ssh-keygen -t rsa -b 4096**
```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/var/lib/barman/.ssh/id_rsa):
Created directory '/var/lib/barman/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /var/lib/barman/.ssh/id_rsa
Your public key has been saved in /var/lib/barman/.ssh/id_rsa.pub
The key fingerprint is:.....
```
- **root@web1-psql-master:~# su postgres**
- **postgres@web1-psql-master:/root$ cd**
- **postgres@web1-psql-master:~$ pwd**
```bash
/var/lib/postgresql
```

- **postgres@web1-psql-master:~$ ssh-keygen -t rsa -b 4096**
```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/var/lib/postgresql/.ssh/id_rsa):
Created directory '/var/lib/postgresql/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /var/lib/postgresql/.ssh/id_rsa
Your public key has been saved in /var/lib/postgresql/.ssh/id_rsa.pub
The key fingerprint is:
```
- **postgres@barmen-graylog-zabbix:~$ cat ~/.ssh/id_rsa.pub**  # После генерации ключа, выводим содержимое файла и копируем содержимое файла на сервер **postgres** в файл /var/lib/postgresql/.ssh/authorized_keys
 ~/.ssh/id_rsa.pub: 
- **web1-psql-master:~$ cat ~/.ssh/id_rsa.pub** # После генерации ключа, выводим содержимое файла и копируем содержимое файла на сервер **barman** в файл /var/lib/barman/.ssh/authorized_keys

- **postgres@web1-psql-master:~$ psql**
```bash
psql (16.13 (Ubuntu 16.13-0ubuntu0.24.04.1))
Type "help" for help.
```
- **postgres=# CREATE USER barman WITH REPLICATION Encrypted PASSWORD 'Otus2026!';** # В psql создаём пользователя barman c правами суперпользователя
```bash
CREATE ROLE
```
- **postgres=# \q** # выходим
- **postgres@web1-psql-master:~$ vim /etc/postgresql/16/main/pg_hba.conf** # добавляем разрешения для пользователя barman (2 последние стрки)
```bash
# "local" is for Unix domain socket connections only
local   all             all                                     peer
# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
# IPv6 local connections:
host    all             all             ::1/128                 scram-sha-256
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     peer
host    replication     all             127.0.0.1/32            scram-sha-256
host    replication     all             ::1/128                 scram-sha-256
host    replication 	replication	192.168.50.15/32        scram-sha-256
host    replication 	replication	192.168.50.16/32        scram-sha-256
host	all		barman		192.168.50.23/32        scram-sha-256
host	replication	barman		192.168.50.23/32	scram-sha-256
```
- **root@web1-psql-master:~# systemctl restart postgresql** # перезапускаем psql
- **root@web1-psql-master:~# sudo -u postgres psql** # заходим в psql
- **postgres=# CREATE DATABASE otus**; создаем тестовую базу otus
```bash
CREATE DATABAS otus=# CREATE TABLE test (id int, name varchar(30));
CREATE TABLE
```
- **otus=# \d**
```bash
		List of relations
 Schema | Name | Type  |  Owner
--------+------+-------+----------
 public | test | table | postgres
(1 row)
```
- **postgres=# \c otus;** # создаём таблицу garantusers в базе otus, добавляем записи и проверяем содержимое
```bash
otus=# CREATE TABLE garantusers (
    НОМЕР SERIAL PRIMARY KEY,
    ИМЯ VARCHAR(100) NOT NULL,
    ВОЗРАСТ INTEGER,
    ПОЛ VARCHAR(10)
);

otus=# INSERT INTO garantusers (ИМЯ, ВОЗРАСТ, ПОЛ)
VALUES
    ('Ольга Новикова', 22, 'Женский'),
    ('Дмитрий Соколов', 40, 'Мужской'),
    ('Елена Воробьева', 31, 'Женский'),
    ('Алексей Крылов', 29, 'Мужской');
INSERT 0 4
otus=# SELECT * FROM garantusers;
 НОМЕР |       ИМЯ       | ВОЗРАСТ |   ПОЛ
-------+-----------------+---------+---------
     1 | Ольга Новикова  |      22 | Женский
     2 | Дмитрий Соколов |      40 | Мужской
     3 | Елена Воробьева |      31 | Женский
     4 | Алексей Крылов  |      29 | Мужской
(4 rows)
```
- **root@web2-psql-replica:~# sudo -u postgres psql**
```bash
psql (16.13 (Ubuntu 16.13-0ubuntu0.24.04.1))
Type "help" for help.
```

- **postgres=# \l**
<img width="929" height="200" alt="Screenshot 2026-03-17 at 12 19 42" src="https://github.com/user-attachments/assets/dc4b36f8-1f40-409d-8ca3-2ffc26dcb3f0" />

- **postgres=# \c otus**
```bash
You are now connected to database "otus" as user "postgres".
```
- **otus=# \d** # структура таблицы
```bash
				  List of relations
 Schema |         Name          |   Type   |  Owner
--------+-----------------------+----------+----------
 public | garantusers           | table    | postgres
 public | garantusers_НОМЕР_seq | sequence | postgres
 public | test                  | table    | postgres
(3 rows)
```
- **otus=# SELECT * FROM garantusers;** # выборка
```bash
 НОМЕР |       ИМЯ       | ВОЗРАСТ |   ПОЛ
-------+-----------------+---------+---------
     1 | Ольга Новикова  |      22 | Женский
     2 | Дмитрий Соколов |      40 | Мужской
     3 | Елена Воробьева |      31 | Женский
     4 | Алексей Крылов  |      29 | Мужской
(4 rows)
```
- **barman@barmen-graylog-zabbix:~$ cat ~/.pgpass** # Находясь в пользователе barman создаём файл ~/.pgpass со следующим содержимым: 
```bash
192.168.50.15:5432:*:barman:Otus2026!
```
- **barman@barmen-graylog-zabbix:~$ chmod 600  ~/.pgpass** # Файл должен быть с правами 600, владелец файла barman.
- **barman@barmen-graylog-zabbix:~$ ls -hal  ~/.pgpass**
```bash
-rw------- 1 barman barman 38 Mar 16 08:07 /var/lib/barman/.pgpass
```
- **barman@barmen-graylog-zabbix:~$ psql -h 192.168.50.15 -U barman -d postgres** # проверяем, что права для пользователя настроены корректно
```bash
psql (16.13 (Ubuntu 16.13-0ubuntu0.24.04.1))
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, compression: off)
Type "help" for help.
```
- **postgres=> \q** # выход
- **barman@barmen-graylog-zabbix:~$ psql -h 192.168.50.15 -U barman -c "IDENTIFY_SYSTEM" replication=1** # Проверяем репликацию
```bash
	  systemid       | timeline |  xlogpos  | dbname
---------------------+----------+-----------+--------
 7617513940940913251 |        1 | 0/745A9D8 |
(1 row)
>
```
- **postgres=#** # даем дополнительные права для barman (что-то не работает...)
```bash
GRANT EXECUTE ON FUNCTION pg_start_backup(text, boolean, boolean) TO barman;
GRANT EXECUTE ON FUNCTION pg_stop_backup() TO barman;
GRANT EXECUTE ON FUNCTION pg_stop_backup(boolean, boolean) TO barman;
GRANT EXECUTE ON FUNCTION pg_switch_wal() TO barman;
GRANT EXECUTE ON FUNCTION pg_create_restore_point(text) TO barman;
ERROR:  function pg_start_backup(text, boolean, boolean) does not exist
ERROR:  function pg_stop_backup() does not exist
ERROR:  function pg_stop_backup(boolean, boolean) does not exist
GRANT
GRANT
```
- **postgres=# SELECT rolname FROM pg_roles WHERE rolname = 'barman';** # проверяем
```bash
 rolname
---------
 barman
(1 row)
```
**root@barmen-graylog-zabbix:~# barman receive-wal --create-slot node1** # создаёт replication slot на PostgreSQL для стриминга WAL
```bash
Creating physical replication slot 'node1' on server 'node1'
```
- **postgres=#**
```bash
CREATE TABLE test_wal(id serial); # делаем изменения в данных, чтобы пошли wal-файлы на barman
CREATE TABLE
```
- **postgres=#**
```bash
INSERT INTO test_wal DEFAULT VALUES;
INSERT 0 1
```
- **barman@barmen-graylog-zabbix:/root$ sudo pkill -u barman -f receive-wal** # удаляем лишние процессы, которые мешают запустить 

- **barman@barmen-graylog-zabbix:/root$ barman receive-wal node1**
```bash
Starting receive-wal for server node1
node1: pg_receivewal: starting log streaming at 0/16000000 (timeline 1)
node1: pg_receivewal: finished segment at 0/17000000 (timeline 1)
node1: pg_receivewal: finished segment at 0/18000000 (timeline 1)
```
### Долгожданный результат. С Postgresql еще надо попрактиковаться...
<img width="891" height="529" alt="Screenshot 2026-03-17 at 10 48 47" src="https://github.com/user-attachments/assets/dc33951b-42b9-4bce-b004-c58f5098c792" />

- barman@barmen-graylog-zabbix:/root$ rm -rf /var/lib/barman/node1/incoming/*
<img width="791" height="434" alt="Screenshot 2026-03-17 at 10 49 39" src="https://github.com/user-attachments/assets/5902e56d-fa71-48c8-befd-39a2bcd4fb60" />

### На этом процесс настройки бекапа закончен, для удобства команду barman backup node1 требуется добавить в crontab. 


### 2. Настройка hot_standby репликации с использованием слотов и резервного копирования с помощью Ansible

<img width="266" height="1031" alt="Screenshot 2026-03-17 at 14 26 37" src="https://github.com/user-attachments/assets/fdeb824b-c38b-4598-a58c-6c539461b375" />

### Содержимое файлов:

- **➜  ansible cat ansible.cfg**
```bash
[defaults]
host_key_checking = False
allow_world_readable_tmpfiles = True

[ssh_connection]
pipelining = True
```
- **➜  ansible cat inventory/hosts** 
```bash
[master]
node1 ansible_host=192.168.50.15

[replica]
node2 ansible_host=192.168.50.16

[barman]
barman ansible_host=192.168.50.23

[master:vars]
listen_addresses='localhost,192.168.50.15'

[replica:vars]
listen_addresses='localhost,192.168.50.16'

[all:vars]
ansible_user=spg
ansible_ssh_private_key_file=~/.ssh/id_rsa
ansible_python_interpreter=/usr/bin/python3.12
```
- **➜  ansible cat provision.yml** 
```bash
---
- name: Postgres
  hosts: all
  become: yes
  tasks:
#Устанавливаем vim и telnet (для более удобной работы с хостами)
    - name: install base tools
      apt:
        name:
         - vim
         - telnet
        state: present
        update_cache: true

#Запуск ролей install_postgres и postgres_replication на хостах node1 и node2
- name: install postgres 16 and set up replication
  hosts: node1,node2
  become: yes
  roles:
   - install_postgres
   - postgres_replication

#Запуск роли install_barman на всех хостах
- name: set up backup
  hosts: all
  become: yes
  roles:
   - install_barman
```
 - **➜  ansible cat install_postgres/tasks/main.yml**
```bash
#SPDX-License-Identifier: MIT-0
---
# tasks file for install_postgres
- name: install postgresql-server 16
  apt: 
    name: 
        - postgresql-16 
        - postgresql-client-16 
        - postgresql-contrib
    state: present
    update_cache: true

# Запускаем postgresql-16
- name: Start PostgreSQL cluster 16-main
  service:
    name: postgresql@16-main
    state: started
    enabled: yes
  when: "'replica' not in group_names"
```
- **➜  ansible cat postgres_replication/defaults/main.yml** 
```bash
#SPDX-License-Identifier: MIT-0
---
# defaults file for postgres_replication
replicator_password: 'Otus2026!'
master_ip: '192.168.50.15'
slave_ip: '192.168.50.16'
```
- **➜  ansible cat postgres_replication/tasks/main.yml**   
```bash
#SPDX-License-Identifier: MIT-0
---
# tasks file for postgres_replication
- name: install base tools
  apt:
    name:
      - python3-pexpect
      - python3-psycopg2
    state: present
    update_cache: true

#CREATE USER replicator WITH REPLICATION Encrypted PASSWORD 'Otus2022!';
- name: Create replicator user
  become: yes
  become_user: postgres
  postgresql_user:
    name: replicator
    password: "{{ replicator_password }}"
    role_attr_flags: REPLICATION
  when: "'master' in group_names"

#Останавливаем postgresql-16 на хосте psql-replica
- name: stop postgresql-server on psql-replica
  service: 
    name: postgresql
    state: stopped
  when: "'replica' in group_names"

#Копируем конфигурационный файл postgresql.conf
- name: copy postgresql.conf
  template:
    src: postgresql.conf.j2
    dest: /etc/postgresql/16/main/postgresql.conf
    owner: postgres
    group: postgres
    mode: '0600'
  when: "'master' in group_names"

#Копируем конфигурационный файл pg_hba.conf
- name: copy pg_hba.conf
  template:
    src: pg_hba.conf.j2
    dest: /etc/postgresql/16/main/pg_hba.conf
    owner: postgres
    group: postgres
    mode: '0600'
  when: "'master' in group_names"
#Перезапускаем службу  postgresql-16
- name: restart postgresql-server on psql-master
  service: 
    name: postgresql
    state: restarted
  when: "'master' in group_names"

#Удаляем содержимое каталога /var/lib/postgresql/16/main/
- name: Remove files from data catalog
  file:
    path: /var/lib/postgresql/16/main/
    state: absent
  when: "'replica' in group_names"

#Копируем данные с psql-master на psql-replica
- name: copy files from master to slave
  become_user: postgres
  expect:
    command: 'pg_basebackup -h {{ master_ip }} -U  replication -p 5432 -D /var/lib/postgresql/16/main/ -R -P'
    responses: 
      '.*Password*': "{{ replicator_password }}"
  when: "'replica' in group_names"

#Копируем конфигурационный файл postgresql.conf
- name: copy postgresql.conf
  become: yes
  become_user: postgres
  template:
    src: postgresql.conf.j2
    dest:  /etc/postgresql/16/main/postgresql.conf
    owner: postgres
    group: postgres
    mode: '0600'
  when: "'replica' in group_names"

#Копируем конфигурационный файл pg_hba.conf
- name: copy pg_hba.conf
  become: yes
  become_user: postgres
  template:
    src: pg_hba.conf.j2
    dest:  /etc/postgresql/16/main/pg_hba.conf
    owner: postgres
    group: postgres
    mode: '0600'
  when: "'replica' in group_names"
 
#Запускаем службу postgresql-16 на хосте psql-replica
- name: start postgresql-server on psql-replica
  service: 
    name: postgresql
    state: started
  when: "'replica' in group_names"
```
- ➜  ansible cat install_barman/defaults/main.yml 
```bash
#SPDX-License-Identifier: MIT-0
---
# defaults file for install_barman
master_ip: '192.168.50.15'
master_user: 'postgres'
barman_ip: '192.168.50.23'
barman_user: 'barman'
barman_user_password: 'Otus2026!'
```
- **➜  ansible cat install_barman/tasks/main.yml**  
```bash
#SPDX-License-Identifier: MIT-0
---
# tasks file for install_barman
# Установка необходимых пакетов для работы с postgres и пользователями
  - name: install base tools
    apt:
      name:
        - python3-pexpect
        - python3-psycopg2
        - bash-completion 
        - wget 
      state: present
      update_cache: true

  #  Установка пакетов barman и postgresql-client на сервер barman 
  - name: install barman and postgresql packages on barman
    apt:
      name:
        - barman
        - barman-cli
        - postgresql
      state: present
      update_cache: true
    when: "'barman' in group_names"

 #  Установка пакетов barman-cli на серверах node1 и node2 
  - name: install barman-cli and postgresql packages on nodes
    apt:
      name:
        - barman-cli
      state: present
      update_cache: true
    when: "'barman' not in group_names"

#  Генерируем SSH-ключ для пользователя postgres на хосте node1
  - name: generate SSH key for postgres
    user:
      name: postgres
      generate_ssh_key: yes
      ssh_key_type: rsa
      ssh_key_bits: 4096
      force: no
    when: "'master' in group_names"
 
#  Генерируем SSH-ключ для пользователя barman на хосте barman
  - name: generate SSH key for barman
    user:
      name: barman
      uid: 994
      shell: /bin/bash
      generate_ssh_key: yes
      ssh_key_type: rsa
      ssh_key_bits: 4096
      force: no
    when: "'barman' in group_names"

  #  Забираем содержимое открытого ключа postgres c хоста node1
  - name: fetch all public ssh keys node1
    shell: cat /var/lib/postgresql/.ssh/id_rsa.pub
    register: ssh_keys
    when: "'master' in group_names"

  #  Копируем ключ с barman на node1
  - name: transfer public key to barman
    delegate_to: barman
    authorized_key:
      key: "{{ ssh_keys.stdout }}"
      comment: "{{ ansible_facts['hostname'] }}"
      user: barman
    when: "'master' in group_names"

  #  Забираем содержимое открытого ключа barman c хоста barman 
  - name: fetch all public ssh keys barman
    shell: cat /var/lib/barman/.ssh/id_rsa.pub
    register: ssh_keys
    when: "'barman' in group_names"

 #  Копируем ключ с node1 на barman
  - name: transfer public key to barman
    delegate_to: node1
    authorized_key:
      key: "{{ ssh_keys.stdout }}"
      comment: "{{ ansible_facts['hostname'] }}"
      user: postgres
    when: "'barman' in group_names"

  #CREATE USER barman SUPERUSER;
  - name: Create barman user
    become_user: postgres
    postgresql_user:
      name: barman
      password: '{{ barman_user_password }}'
      role_attr_flags: SUPERUSER 
    ignore_errors: true
    when: "'master' in group_names"

   # Добавляем разрешения для подключения с хоста barman
  - name: Add permission for barman
    lineinfile:
      path: /etc/postgresql/16/main/pg_hba.conf
      line: 'host    all   {{ barman_user }}    {{ barman_ip }}/32    scram-sha-256'
    when: "'master' in group_names or 'replica' in group_names"

  # Добавляем разрешения для подключения с хоста barman
  - name: Add permission for barman
    lineinfile:
      path: /etc/postgresql/16/main/pg_hba.conf
      line: 'host    replication   {{ barman_user }}    {{ barman_ip }}/32    scram-sha-256'
    when: "'master' in group_names or 'replica' in group_names"

  # Перезагружаем службу postgresql-server
  - name: restart postgresql-server on node1
    service: 
      name: postgresql
      state: restarted
    when: "'master' in group_names"

  # Создаём БД otus;
  - name: Create DB for backup
    become_user: postgres
    postgresql_db:
      name: otus
      encoding: UTF-8
      template: template0
      state: present
    when: "'master' in group_names"

  # Создаем таблицу test1 в БД otus;
  - name: Add tables to otus_backup
    become_user: postgres
    postgresql_table:
      db: otus
      name: test1
      state: present
    when: "'master' in group_names"

  # Копируем файл .pgpass
  - name: copy .pgpass
    template:
      src: .pgpass.j2
      dest: /var/lib/barman/.pgpass
      owner: barman
      group: barman
      mode: '0600'
    when: "'barman' in group_names"

  # Копируем файл barman.conf
  - name: copy barman.conf
    template:
      src: barman.conf.j2
      dest: /etc/barman.conf 
      owner: barman
      group: barman
      mode: '0755'
    when: "'barman' in group_names"

 # Копируем файл node1.conf
  - name: copy node1.conf
    template:
      src: node1.conf.j2
      dest: /etc/barman.d/node1.conf
      owner: barman
      group: barman
      mode: '0755'
    when: "'barman' in group_names"

  - name: barman switch-wal node1
    become_user: barman
    shell: barman switch-wal node1
    when: "'barman' in group_names"

  - name: barman cron
    become_user: barman
    shell: barman cron
    when: "'barman' in group_names"
```    
<img width="961" height="1031" alt="Screenshot 2026-03-17 at 16 43 26" src="https://github.com/user-attachments/assets/4ee8d971-fd77-4b5d-88ee-731486088061" />
<img width="963" height="1043" alt="Screenshot 2026-03-17 at 16 44 07" src="https://github.com/user-attachments/assets/02b9f7e3-9689-4aa4-8118-b289ef67682c" />
<img width="952" height="1042" alt="Screenshot 2026-03-17 at 16 45 20" src="https://github.com/user-attachments/assets/5b9a1f45-6415-491e-bb78-9239686be5a4" />


### Настройка бекапа с помощью Ansible завершена.
✅ 1. Проверка репликации (master → replica)

📌 1. Проверка на мастере
- **root@web1-psql-master:~# sudo -u postgres psql -c "SELECT * FROM pg_stat_replication;"**
```bash
  pid  | usesysid |   usename   |  application_name  |  client_addr  | client_hostname | client_port |         backend_start         | backend_xmin |   state   | sent_lsn  | write_lsn | flush_lsn | replay_lsn |    write_lag    |    flush_lag    |   replay_lag    | sync_priority | sync_state |          reply_time
-------+----------+-------------+--------------------+---------------+-----------------+-------------+-------------------------------+--------------+-----------+-----------+-----------+-----------+------------+-----------------+-----------------+-----------------+---------------+------------+-------------------------------
 27279 |    16394 | replication | 16/main            | 192.168.50.16 |                 |       43834 | 2026-03-18 14:46:32.515942+03 |          746 | streaming | 0/5000060 | 0/5000060 | 0/5000060 | 0/5000060  |                 |                 |                 |             0 | async      | 2026-03-18 14:47:42.713356+03
 27283 |    16389 | barman      | barman_receive_wal | 192.168.50.23 |                 |       44488 | 2026-03-18 14:46:33.772815+03 |              | streaming | 0/5000060 | 0/5000060 | 0/5000000 |            | 00:00:02.078799 | 00:01:11.055784 | 00:01:11.055784 |             0 | async      | 2026-03-18 14:47:44.845769+03
(2 rows)
```
📌 2. Проверка на реплике
- **root@web2-psql-replica:~# sudo -u postgres psql -c "SELECT pg_is_in_recovery();"** 
```bash
 pg_is_in_recovery
-------------------
 t
(1 row)


(END)
```
📌 3. Проверка через реальное изменение
- **root@web1-psql-master:~# sudo -u postgres psql**
```bash
psql (16.13 (Ubuntu 16.13-0ubuntu0.24.04.1))
Type "help" for help.
```
- **postgres=# CREATE TABLE test_replication (id int);**
```bash
INSERT INTO test_replication VALUES (1);
CREATE TABLE
INSERT 0 1
```
- **root@web2-psql-replica:~# sudo -u postgres psql**
```bash
psql (16.13 (Ubuntu 16.13-0ubuntu0.24.04.1))
Type "help" for help.
```
- **postgres=# SELECT * FROM test_replication;**
```bash
 id
----
  1 # работает!
(1 row)
```
✅ 2. Проверка backup (Barman)

📌 1. Проверка сервера в Barman
<img width="880" height="546" alt="Screenshot 2026-03-18 at 15 00 40" src="https://github.com/user-attachments/assets/357cdb07-2406-40db-8983-fcf3e4d58ad5" />

📌 2. Сделать backup вручную
- **root@barman:~# barman backup node1**

📌 3. Проверить список backup'ов
- **root@barman:~# barman list-backup node1**
```bash
2026-03-18 12:05:10,885 [10500] barman.utils WARNING: Failed opening the requested log file. Using standard error instead.
2026-03-18 12:05:10,886 [10500] barman.config WARNING: Discarding configuration file: .barman.auto.conf (not a file)
node1 20260318T120129 - Wed Mar 18 15:01:29 2026 - Size: 29.5 MiB - WAL Size: 0 B
```

📌 4. Проверка WAL
- **root@barman:~# barman list-files node1 latest**
```bash
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6110
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6111
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6112
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6113
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6116
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6117
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6175
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6176
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6228
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6229
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6237
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6238
/var/lib/barman/node1/base/20260318T120129/data/base/16390/6239
/var/lib/barman/node1/base/20260318T120129/data/base/16390/826
/var/lib/barman/node1/base/20260318T120129/data/base/16390/827
/var/lib/barman/node1/base/20260318T120129/data/base/16390/828
/var/lib/barman/node1/base/20260318T120129/data/base/16390/PG_VERSION
/var/lib/barman/node1/base/20260318T120129/data/base/16390/pg_filenode.map
/var/lib/barman/node1/base/20260318T120129/data/pg_multixact/members/0000
/var/lib/barman/node1/base/20260318T120129/data/pg_multixact/offsets/0000
/var/lib/barman/node1/wals/0000000100000000/000000010000000000000006
```
### Резюме: Тема сложная. С БД нужно практиковаться.

