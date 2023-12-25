# Команды для .htaccess
Options Indexes   
DirectoryIndex index.html   

## Работа с заголовками
Header set X-Admin-Name "John Smith" #Назначить заголовок  
Header unset Etag #Удалить заголовок   
Header set X-Admin-Name "John Smith"   
Header set Cache-Control "no-cache" - запретить кеширование браузера на диске   
Header set Cache-Control "no-store" -   
Header set Cache-Control "private, no-cache, must-revalidate"   
ExpiresActive On - Включить директиву включения кеширования

---
## Задать разрешение кеширования файлов
- Header set Cache-Control "public, max-age=600" Послать браузеру контроль кеширования на 600   секунд секунды будет считать от текущего времени.  
- ExpiresDefault "now"  
- ExpiresDefault "access plus 2 days" - добавить 2 дня кеширования от текущей даты
- ExpiresDefault "modification plus 3 hours" - примениться от даты изменения файла    
### Задать кеширование по типу ресурсов   
- ExpiresByType text/html "access plus 2 days" - задаст кеширование лишь на тип файла котоырй указан в заголовке
- ExpiresByType image/gif "access plus 2 weeks" - задаст кеширование для картинок формата гиф на 2 недели
### Вариант задания заголовку Expires
- ExpiresDefault A3600

---

## Привязка обработчиков
### CGI
- ScriptALias "/cgi-bin/" "www/cgi-bin" - директива где храняться обработчик скриптов
- AddHandler cgi-script .chi .pl - с помощью этой директивы мы указываем рамширения которые будут являться cgi-скриптами
### Модуль
- LoadModule php5_module(имя модуля) "PHP/php5apache2_2.dll"(место где находиться модуль)
- AddType application/x-httpd-php .php указываем файлы какого типа 
### SSI
- Options +Includes
- AddOutputFilter INCLUDES .shtml
- AddType text/html .shtml
---
### Используем модуль rewrite в папке   
- RewriteEngine On
### Правила модуля rewrite
- RewriteRule Шаблон Замена/Подстановка [Флаги]
 - Пример: 
 - RewriteCond %{REQUEST_FILENAME} !-f
 - RewriteCond %{REQUEST_FILENAME} !-d
- RewriteRule ^([a-z]{0,4})/([0-9]{4})/(\d{1,2})/(\d\d?)/?$   
- RewriteRule ^(.*)$ http://site.ru/$1 [R=301]  - переводи на страницу и подставляй все что попало в правило

- Перенаправление ```test.php?cat=$1&year=$2&mon=$3&day=$4 [L]```
