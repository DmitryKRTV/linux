## Linux terminal installing uninstalling programs

Linux установщики различаются по дистрибутиву: для ubuntu (.deb)- `apt-get` и для redhot, centos (.rpm)- `sudo yum`

`cat /etc/apt/sources.list` - файл с repository-sites

`apt-get install package-name -y` - `-y` - флаг установить yes для всех возникающих вопросов в процессе установки

Команды:
- `wget passToFile` - скачивание файлов с интернета по полному пути
- `sudo apt-get install packageName` - скачать и установить пакет с repository-sites
- `sudo apt-get remove packageName` - стереть пакет
- `sudo dpkg -i packagename` - установка локальных .deb файлов, флаг `-i` - install
- `sudo dpkg -r packagename` - удаление локальных .deb файлов, флаг `-r` - remove
- `yun install packegeName` - скачать и установить пакет с repository-sites
- `yun remove packegeName` - стереть пакет
- `sudo rpm -i filename` - установка скачанного пакета .rpm для redhot, centos
- `sudo rpm -e filename` - удаление скачанного пакета .rpm для redhot, centos
- `reboot now` - перезагрузка сейчас
- `shutdown now` - выключить компьютер сейчас
