## Linux terminal shh(secure shell connection) connection

Программы для подключения через ssh

`putty` - одна из программ для подключения по ssh для windows
`mobaXterm` - одна из программ для подключения по ssh для windows

Если включен ufw(firewall) то не забыть прописать `sudo ufw allow 'OpenSSH'` - даст возможность подключится по ssh

Как проверить создан ли ssh ключ:\
*В директории `~/.ssh/` проверить наличие файлов id_rsa.pub и id_rsa (стандарные имена для ключей)*

Скопировать ssh сгенерированный ключ для того, чтобы сервер его сохранил и входить можно было без пароля:
```
 ssh-copy-id -i ~/.ssh/id_rsa.pub user@remotehost

где:
    user – пользователь, под которым вы подключаетесь на удалённую машину;
    remotehost – ip-адрес удаленной машины.
    -i - опция указывает путь к вашему публичному ключу, который мы хотим закинуть на удаленный сервер

```

<details>
  <summary>Как настроить ssh config?</summary>

Создать файл конфига:
```
touch ~/.ssh/config
chmod 0700 ~/.ssh/config
```

Отредактировать файл:
```
Host host1
ssh_option1=value1
ssh_option2=value1 value2
ssh_option3=value1
Host host2
ssh_option1=value1
ssh_option2=value1 value2
Host *
ssh_option1=value1
ssh_option2=value1 value2
```

   - Host host1 — это определение заголовка для host1, здесь начинается спецификация хоста и заканчивается следующим определением заголовка Host host2, создающим раздел.
   - Host1, host2 — это просто псевдонимы хостов для использования в командной строке, они не являются фактическими именами  удаленных хостов.
   - Параметры конфигурации, такие как ssh_option1 = value1, ssh_option2 = value1 value2, применяются к согласованному хосту и должны иметь отступы для хорошо организованного форматирования.
   - Для параметра, такого как ssh_option2 = value1 value2, значение value1 считается первым, а  value2 – вторым.
  -  Определение заголовка Host * (где * – шаблон – подстановочный знак, который соответствует нулю или более символов) будет соответствовать нулю или более хостам.

 <details>
 <summary>Пример:</summary>
  
  ```
Host fedora25
HostName 192.168.56.15
Port 22
ForwardX11 no
Host centos7
HostName 192.168.56.10
Port 22
ForwardX11 no
Host ubuntu
HostName 192.168.56.5
Port 2222
ForwardX11 yes
Host *
User sedicomm
IdentityFile ~/.ssh/id_rsa
Protocol 2
Compression yes
ServerAliveInterval 60
ServerAliveCountMax 20
LogLevel INFO
```
  Подробное объяснение приведенных выше параметров конфигурации ssh.
  
   - HostName — определяет имя реального хоста для входа в систему, альтернативно, вы можете использовать числовые IP-адреса, это также разрешено (как в командной строке, так и в спецификациях HostName).
   - User — указывает, что пользователь должен войти в систему.
   - Port — устанавливает номер порта для подключения на удаленном хосте, по умолчанию – 22. Используйте номер порта, настроенный в файле конфигурации sshd удаленного хоста.
   - Protocol — этот параметр определяет версии протокола, которые ssh должен поддерживать в порядке предпочтения. Обычными значениями являются «1» и «2», несколько версий должны быть разделены запятыми.
   - IdentityFile — определяет файл, с которого считывается идентификатор аутентификации пользователя DSA, Ed25519, RSA или ECDSA.
   - ForwardX11 — определяет, будут ли соединения X11 автоматически перенаправляться по защищенному каналу и устанавливать DISPLAY. Он имеет два возможных значения «да» или «нет».
   - Compression — оно используется для установки сжатия во время удаленного соединения со значением «да». По умолчанию «нет».
   - ServerAliveInterval — устанавливает интервал таймаута в секундах, после которого, если никакой ответ (или данные) не был получен с сервера, ssh отправит сообщение через зашифрованный канал, чтобы запросить ответ от сервера. Значение по умолчанию равно 0, то есть сообщения не будут отправляться на сервер, если была определена опция BatchMode.
   - ServerAliveCountMax — устанавливает количество живых сообщений сервера, которые могут быть отправлены без получения ответа ssh с сервера.
   - LogLevel — определяет уровень детализации, который используется при регистрации сообщений из ssh. Допустимые значения включают: QUIET, FATAL, ERROR, INFO, VERBOSE, DEBUG, DEBUG1, DEBUG2 и DEBUG3. И значение по умолчанию – INFO.
 </details>
  
</details>

**При подключении к сайтам с помощью ssh ключа, необходимо сначала на сайте создать публичный ssh ключ, а потом применить его для пользователя(git), который будет логиниться на сайте**

Полезные команды:
- `service ssh status` - узнать статус ssh сервиса
- `sudo apt-get install openssh-server` - установить openssh-server если не установлен
- `service ssh start` - стартануть сервер, есть не активен
- `ssh username@ipAddress` - подключится к компьютеру
- `ssh-keygen -t rsa` - сгенерировать публичный и приватный ключи (открытый id_rsa.pub и закрытый id_rsa)
- `ssh -L 9221:localhost:9229 127.0.0.1 -p 6000` - дополнительно окткрыть порт, например в докер контейнер (9221 - порт текущей машины, localhost:9229 - порт удаленной машины, 127.0.0.1 -p 6000 - ssh куда конектиться)


Источники:
- [Создание public & private rsa ключей](https://jeka.by/ask/183/generate-ssh-keys/)
- [Настройка соединения с помощью rsa ключей public & private](https://jeka.by/ask/182/ssh-without-password/)
- [Настройка ssh config для входа по имени, а не по ip](https://blog.sedicomm.com/2018/04/08/kak-nastroit-polzovatelskoe-podklyucheniya-ssh-dlya-uproshheniya-udalennogo-dostupa/)
- [Дополнительная информация по ssh](https://www.opennet.ru/cgi-bin/opennet/man.cgi?topic=ssh&category=1#lbAI)
