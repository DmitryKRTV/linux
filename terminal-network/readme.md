## Linux terminal network

Команды:
- `ifconfig` - информация о ip
- `ip addr show` - информация о ip
- `route` - информация о перенаправлении пакетов
- `id route show` - информация о перенаправлении пакетов
- `ping -C 4 IP` - пинг, флаг `-C 4` - означает назначить счетчик и сделать пинг 4 раза
- `traceroute` - команда, показывающая информацию о соединении
- `host site` - информация о site
- `dig site` - информация о site
- `netstat` - информация о соединениях и портах
- `sudo ufw allow portnumber` - открыть порт по его номеру
- `ssh computerName` - подключиться к удаленному серверу
- `hostname` - храниться в `etc/hostname` - если изменить название в этом файле, то имя компьютера поменяется при перезагрузке
- `sudo hostname newComputerName` - сменить название компьютера
- `sudo vim etc/hosts` если изменить название в этом файле, то ip адрес заменится при перезагрузке
- `sudo nano etc/network/interfaces` - прописать там 
```bash
auto enp0s3(название сетевой карты(networkName) из ifconfig)
iface enp0s3 inet statuc
address  20.20.20.20
netmask 255.0.0.0
gateway 20.20.20.1
dns-nameservers 8.8.8.8
```
- `sudo ifdown newtworkName` - выключить сеть
- `sudo ifup newtworkName` - включить сеть
- `sudo ifconfig nerworkName 10.10.10.10 netmask 255.0.0.0` - временно изменить ip адрес