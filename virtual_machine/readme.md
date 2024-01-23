# Virtual machine

## Для создания вирутальной машины  необходимо установить qemu-kvm
```
sudo apt install -y qemu-kvm qemu-utils dnsmasq virt-manager libvirt-daemon-system virtinst libvirt-clients bridge-utils
sudo systemctl enable --now libvirtd
sudo systemctl start libvirtd
```

Далее, для управления виртуальными машинами необходима установка virt-manager

https://computingforgeeks.com/use-virt-manager-as-non-root-user/ - установка
```
sudo getent group | grep libvirt
sudo usermod -a -G libvirt $(whoami)

id $(whoami)
uid=1000(dark123us) gid=1000(dark123us) groups=1000(dark123us),27(sudo),118(libvirt)

virsh net-list
```

## Name State Autostart Persistent
```
default active yes yes

sudo vim /etc/libvirt/libvirtd.conf
unix_sock_group = "libvirt"
unix_sock_rw_perms = "0770"

sudo systemctl restart libvirtd.service

systemctl status libvirtd.service 
```
## Создание виртуальной машины с помощью virt-manager 

1) подключаемся через virt-manager к s6
2) скачиваем на s6 .iso образ unutu по ссылке wget "https://releases.ubuntu.com/20.04/ubuntu-20.04.6-live-server-amd64.iso"
ссылку можно получить на сайте https://releases.ubuntu.com/20.04/ нажав повой кнопкой по желаемому образу, в выпавшем окне выбрать копировать ссылку
3) В virt-manager File -> Create virt machine
4) Далее нужно нажать на Start Pool(кнопка треугольника) чтобы появилась возможность выбрать образ из пула
5) Выбираем желаемую ОС, выделяем мощности

## Удаление виртуальной машины 
```
sudo virsh undefine [originalMach]
```

## Клонирование виктульной машины

https://codeby.net/blogs/kak-klonirovat-sushhestvuyushhie-obrazy-virtualnoj-mashiny-kvm-v-linux/

1) Подготавливаем машину с помощью команды:
```
sudo virt-sysprep --domain [originalMach] 
```
2) Используем команду для клонирвоания
```
sudo virt-clone --original [originalMach] --name [newName] --auto-clone
```

## Измнение id и hostname машины

Генерация нового UUID
Замена ID машины в файле /etc/machine-id
```
NEW_UUID=$(uuidgen)
sudo sh -c "echo $NEW_UUID > /etc/machine-id"
```
Замена текущего hostname на новый
```
NEW_HOSTNAME="новое_имя_хоста"
sudo sh -c "echo $NEW_HOSTNAME > /etc/hostname"
sudo hostname $NEW_HOSTNAME
```

## Удаление старой машины из сети 
```
sudo virsh net-update default delete ip-dhcp-host "<host mac='$1' name='$2' ip='$3' />" --live --config
```

---
## Проблемы 

### Если возникли проблемы с dnsmasq
```
sudo apt install dnsmasq
sudo virsh net-start default
sudo virsh net-autostart default
```

### Сброс вируталньой машины

вероятная проблема это использование команды virt-sysprep
Нужно СНАЧАЛА скопировать, а потом применить её к КОПИИ виртуальной машины
``` bash
sudo virt-sysprep --operations dhcp-client-state,machine-id,customize,dhcp-server-state,net-hwaddr,net-hostname --hostname master1 -d master1
master 1 - имя копии виртуальной машины
```

### Изменение mac и ip для работы в сети 

``` bash
IP="192.168.122.10"
VM=master1
MAC=$(sudo virsh domiflist $VM | tail -2 | awk '{print $5}')
sudo virsh net-update default add ip-dhcp-host "<host mac='$MAC' name='$VM' ip='$IP' />" --live --config
sudo virsh start $VM
```
