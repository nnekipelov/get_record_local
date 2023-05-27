# get_record_local 
### 2022-03-01, IT-Director, v.3.5.1

_The file get_record_local.php is required for integration Asterisk and CRM system via ITD-Asterisk module_

---
Предназначено для возможности скачивания отдельной записи разговора из АТС и передачи его в CRM систему через модуль интеграции ITD-Asterisk

В качестве параметров принимает аргументы `clientId` и `uniqueid`. В случае неправильного указания `clientId`, а также отсутствие в запросе любого из указанных параметров, результатом будет  `ошибка 404`.

В своей работе скрипт требует установленного на сервере модуля `lame` для конвертации из `WAV` в формат `MP3`.

**Данная версия предназначена для работы в сборке FreePBX и Elastix, а также для чистого Asterisk, при условии идентичности организации хранения файлов записи, структуры таблиц и полей базы данных CDR**

_Если в вашей системе данный скрипт по какой либо причине не заработал, возможна техподдержка и доработка скрипта под заказ. Для этого направьте письмо на адрес info@it-director.it_

---
Рекомендуется на уровне FireWall ограничить доступ к веб-серверу АТС извне. Необходимо разрешить доступ к IP адресам из списка `trust.it-d.it`

---
### Подготовка файла с ключами авторизации
Помимо самого скрипта для работы необходим файл с ключами интеграци, а точнее с их хэшами - результатом обработки хэш-функцией `SHA-256`.
Это необходимо для проверки, чтобы скрипт не возвращал записи звонков по неавторизованным запросам.

Файл `keys.dat` должен находится в этой же директории что и PHP скрипт

Обработать функцией ключи интерации и получить значения хешей можно можно на сайте https://sha256.online

Предполагается возможность использования нескольких ключей, так как одна АТС может быть подключена к нескольким  интеграциям с CRM. Каждый хэш ключа необходимо расположить на новой строке без каких либо знаков препинания, пометок и комментариев.

**!!! Доступ к файлу `keys.dat` требуется ограничить через директивы `.htaccess`, например:**

```
Options All -Indexes
IndexIgnore *
Order deny,allow
<Files "keys.dat">
    Deny from all
</Files>
<Files "./">
    Allow from all
</Files>
```
