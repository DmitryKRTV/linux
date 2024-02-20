# Создание обратного прокси сервера

Модель: клиент-интернет-прокси_сервер-хост

На готовую сборку модно установить ssl сертификат

```
server {
        listen 443 ssl;
        server_name _;

        ssl_certificate /etc/letsencrypt/live/domain_name/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/domain_name/privkey.pem;

        location / {
                proxy_pass domain_name;
                proxy_set_header Host domain_name;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_buffering off;
        }
}
```
 proxy_buffering off; - отсутствие этого флага не будет подгружать ресурсы, нужно на это обращать внимание
