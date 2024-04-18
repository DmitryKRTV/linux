## NGINX (engine x)
— это бесплатный высокопроизводительный HTTP-сервер с открытым исходным кодом и обратный прокси-сервер, а также прокси-сервер IMAP/POP3.

NGINX можно использовать в качестве веб-сервера, обратного прокси-сервера, балансировщика нагрузки, почтового прокси-сервера и кэша HTTP. Его также можно использовать для обслуживания статических файлов, динамического контента и потоковой передачи мультимедиа.

Чтобы хостить файлы с помощью nginx необходимо:
1) Permissions должны удовлетворять требованиям как в этой [статье](https://stackoverflow.com/questions/53293210/403-forbidden-nginx)(755 for directories and 644 for files is recommended for use with NGINX. The NGINX user also needs to be the owner of the files.) Легче всего просто в nginx.conf поставить запуск не от стандартнорго www-data, а от root или другого юзера

2) Отдельные файлы должны лежатиь в папке sites-enabled как ссылки на sites-available, кроме доступов из пункта выше для стандартной настройки ничего не нужно
пример такого файла 
```
server {
        listen 80;

        location /buh {
                alias /home/krtv/tmp/svc/svcdoc/builddoc/development/html;
        }

}
```
 alias - пусть к папке, в index можно прописать какой файл искать. Если указывать root то к нему ещё прибавиться значение location
### [Installing](installing/readme.md)
