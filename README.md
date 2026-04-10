# tms-disk-lvm-
1. Создал 2 диска через Virtual Box, перед этим сделал snapshop.
   ![Alt text](https://github.com/stepan-bogach/tms-disk-lvm-/blob/main/photo_2026-04-08_16-35-15.jpg)

3. Создал по ошибке в 2 дисках раздела 3 в место 4 раздела 2/2 1/1, пользовался parted.

4. Собрал vg с помощью команд sudo pvcreate tms-vg /диск/раздел
   ![Alt text](https://github.com/stepan-bogach/tms-disk-lvm-/blob/main/photo_2026-04-08_16-38-37.jpg)

6. Создал 2 lv с помощью sudo lvcreate -n (data/bkp) -L (размер) tms-vg
   Поменял ФС - mkfs.ext4 /dev/tms-gv/bkp, mkfs.xfs /dev/tms-gv/data
   Примонтировал lv к дир sudo mount /dev/tms-gv/* /opt/*
   ![Alt text](https://github.com/stepan-bogach/tms-disk-lvm-/blob/main/photo_2026-04-08_16-40-17.jpg)

8. Добавил раздел к vg с помощью команды sudo vgextend tms-vg /dev/sdc2

9. Расширил lv sudo lvextend -l +100%FREE /dev/tms-vg/data

# Из-за неверного интерпретирования задания сделал 3 раздела вместо 4 невыполнил пункт 7.8.9.
# Так как не понял как можно создать еще раздел с учетом тогда что в шаге 6 расширили всю vg и диск  более не осталось.
# Поэтому вместо того чтоб еще несколько раз перечитать дз, пошел другим путем, в пункте 10,11,12 воспользовался lv /dev/tms-gv/bkp в /opt/backup и выполнил все шаги описанные в 10,11,12.
# В итоге когда создаешь файлы и делаешь umount то файлы остаются на диске, но не в дир, и наоборот когда создаешь файлы в дир и монтируешь туда диск то исходный файл остаеться в корневой ФС и ее не видно на только что примонтированной ФС.
