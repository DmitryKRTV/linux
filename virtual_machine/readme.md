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

---
## Проблемы 

###Если возникли проблемы с dnsmasq
```
sudo apt install dnsmasq
sudo virsh net-start default
sudo virsh net-autostart default
```
