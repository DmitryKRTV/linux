# Mounting(Монтирование)

Для монитрования нужно:
- удалить старые partitions
- разбить диск на partitions
- отформатировать их
- смонтировать partitions на диск

## Управление диском

### Получение информации

```
lsblk -f
lsblk -l 
df -h
sudo blkid
```

### Утилита parted
```
sudo parted /dev/nvme2n1 - nvme2n1 - название диска
```

```
print -l - информация о диске
mklabel gpt - Если нужно сменить таблицу partitions, где gpt - таблица partitions
mkpart primary ext4 1MiB 100% - создать partitions, где ext4 - тип файловой системы, 1MiB 100% - границы файловых разделов
rm 1 - удалить partitions, где 1 - номер partitions
```

### Утилита fdisk 
```
sudo fdisk /dev/nvme2n1

p  (нажмите Enter, чтобы отобразить список разделов)
d  (нажмите Enter, чтобы выбрать опцию удаления раздела)
1  (нажмите Enter, чтобы указать номер раздела для удаления)
p  (нажмите Enter, чтобы проверить изменения)
w  (нажмите Enter, чтобы сохранить изменения и выйти из утилиты)
```

### Форматирование
```
 sudo mkfs -t ext4 /dev/nvme2n1p1 - отфармотировать nvme2n1p1 nvme2n1p1
```

### Монтирование 
```
sudo mount -v -t ext4 /dev/nvme2n1p1 /mnt/nvme2 - смонтировать nvme2n1p1 в дирректорию nvme2 с файловой системой ext4
```
