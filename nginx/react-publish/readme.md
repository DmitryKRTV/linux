[Source](https://serverspace.ru/support/help/razvertyvanie-prilozheniya-react-na-nginx-pod-ubuntu/) - делать в соответствии с шагами

Для публикации react нужны:
- node, npm, nvm - для билда,
- настроенный ufw(включен нужный профиль nginx),
- настроен минимальный config `sudo vim /etc/nginx/sites-enabled/default`,
- `root /var/www/<ДОМЕННОЕ_ИМЯ>;` - должен быть изменён на папку с билдом,
- не забывать копировать билд в папку с nginx с флагом 'рекурсивно' (`cp -r targetFol outputFol`)
- не забывать перезагружать nginx после нового билда `service nginx restart`