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
- Если что-то пойдет не так, всегда можно загрузиться со старого ядра (оно остаётся в меню GRUB).*
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
**Домашнее задание** <ins>"построить массив"</ins>

Цель: научиться работать с массивами в ОС Linux;

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
- Чтобы система присылала уведомления об ошибках, в mdadm.conf можно настроить email-оповещения:  
</details>

**Выполнение домашнего задания:**

- Добавлено 2 диска по 25ГБ.
- Перезагружена машина
- **root@ol-alp-ubuntu1:/home/spg#fdisk -l**
- Disk /dev/sda: 30 GiB, 32212254720 bytes, 62914560 sectors
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


- Disk /dev/sdb: 25 GiB, 26843545600 bytes, 52428800 sectors
- Disk model: Virtual disk
- Units: sectors of 1 * 512 = 512 bytes
 -Sector size (logical/physical): 512 bytes / 512 bytes
 -I/O size (minimum/optimal): 512 bytes / 512 bytes


- Disk /dev/sdc: 25 GiB, 26843545600 bytes, 52428800 sectors
- Disk model: Virtual disk
- Units: sectors of 1 * 512 = 512 bytes
- Sector size (logical/physical): 512 bytes / 512 bytes
- I/O size (minimum/optimal): 512 bytes / 512 bytes

- **root@ol-alp-ubuntu1:/home/spg# mdadm --zero-superblock --force /dev/sd{b,c}**
- mdadm: Unrecognised md component device - /dev/sdb
- mdadm: Unrecognised md component device - /dev/sdc

- **root@ol-alp-ubuntu1:/home/spg# mdadm --create --verbose /dev/md0 -l 1 -n 2 /dev/sd{b,c}**
- mdadm: Note: this array has metadata at the start and
-    may not be suitable as a boot device.  If you plan to
-    store '/boot' on this device please ensure that
-    your boot-loader understands md/v1.x metadata, or use
-    --metadata=0.90
- mdadm: size set to 26196992K
- Continue creating array? y
- mdadm: Defaulting to version 1.2 metadata
- mdadm: array /dev/md0 started.
