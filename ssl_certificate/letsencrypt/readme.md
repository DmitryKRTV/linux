# Установка nginx с сертификатом lets_ecript

1. Установите пакет Certbot, который является клиентом Let's Encrypt:
```
sudo apt update
sudo apt install python3-certbot-nginx certbot
```
2. Получите SSL-сертификат от Let's Encrypt:

```
sudo certbot certonly --nginx
```

Certbot автоматически обнаружит ваш сервер Nginx и настроит соответствующие конфигурации для получения сертификата.

В процессе получения сертификата Certbot может попросить вас указать свою электронную почту и согласиться с условиями Let's Encrypt.

3. После успешного получения сертификата Let's Encrypt, Certbot сохранит сертификаты в директории /etc/letsencrypt/live/your_domain.com/. Здесь your_domain.com - это ваше доменное имя.

4. Настройте конфигурационный файл Nginx для использования SSL-сертификата Let's Encrypt:
```
sudo nano /etc/nginx/sites-available/default
```
5. В этом файле замените секцию server на следующий конфигурационный блок:
```
nginx

server {
    listen 80;
    listen [::]:80;

    server_name your_domain.com;

    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    listen [::]:443 ssl;

    server_name your_domain.com;

    ssl_certificate /etc/letsencrypt/live/your_domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/your_domain.com/privkey.pem;

    location / {
        proxy_pass http://your_backend_server;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

6. **Убедитесь**,
- что заменили your_domain.com на своё доменное имя и your_backend_server на адрес или имя вашего бэкенд-сервера.
- что есть символическая ссылка в sites-enabled

Сохраните и закройте файл.

Проверьте наличие ошибок в конфигурации Nginx:
```
sudo nginx -t
```
7. Если ошибок нет, перезапустите Nginx:
```
sudo service nginx restart
```
Теперь ваш сервер Nginx настроен для прослушивания HTTP-трафика на порту 80 и перенаправления его на HTTPS (порт 443) с использованием SSL-сертификата от Let's Encrypt. Let's Encrypt также автоматически обновит ваш сертификат, чтобы гарантировать его актуальность.
