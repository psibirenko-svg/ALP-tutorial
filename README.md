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

🎯**Задание
1.создать свой RPM (можно взять свое приложение, либо собрать к примеру Apache с определенными опциями);
2.cоздать свой репозиторий и разместить там ранее собранный RPM;
3.реализовать это все либо в Vagrant, либо развернуть у себя через Nginx и дать ссылку на репозиторий.**

<details>
	
<summary> = Теория = </summary>

</details>
