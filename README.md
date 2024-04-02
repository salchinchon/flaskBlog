# Тестовое задание для vizorlabs
## Установка
После того как вы склонировали проект, в его корне создайте .env файл c переменными:
 - DOMAIN - доменное имя проекта, нужно для работы веб сервера и получения сертификатов
 - DRY_RUN - фллаг для тестового режима при получении сертификатов, нужен для проверки, чтобы не исчерпать лимит запросов. Принимает значени 1 и 0, где 1 включения безопасного реима, а 0 выключение.

Для получения сертификатов letsencrypt используется крипт init-letsencrypt.sh, выдайте ему права на исполнение и запустите:
```sh
chmod +x flaskBlog/init-letsencrypt.sh && ./flaskBlog/init-letsencrypt.sh
```
После получения сертификата, нужно настроить ssl в конфигурационном фале nginx:
```sh
nano flaskBlog/nginx/config/flaskblog.conf.template
```
Вы можете добавить какой то свой блок, или раскоментировать имеющейся там. После чего перезапустите контейнеры:
```sh
docker-compose restart
```
## Бэкап и востоновление 
Чтобы сделать бекап SQLite, достаточно куда скопировать каталог db находящейся в корне проекта, желательно при выключеном контейнере:
- cp -r flaskBlog/db ~/backup

По аналогии, чтобы востоновить из бекапа базу, перенести файлы бд в каталог db в корне проекта:
- rm -rf flaskBlog/db && cp -r ~/backup/db flaskBlog/

