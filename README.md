# get_record_local
The file get_record_local.php is required for integration Asterisk and CRM system via ITD-Asterisk module
### 2022-03-01, IT-Director, version 3.3
Предназначено для возможности скачивания записи разговора из АТС в CRM систему через модуль интеграции ITD-Asterisk
В качестве параметров принимает аргументы `clientId` и `uniqueid` 
В случае неправильного указания `clientId`, а также отсутствие в запросе любого из указанных параметров, вызовет результат `ошибка 404`
В своей работе скрипт требует установленного на сервере модуля `lame` для конвертации из `WAV` в формат `MP3`

**Данная версия предназначена для работы в сборке FreePBX и Elastix, а также для чистого Asterisk, при условии идентичности организации хранения файлов записи и структуры таблиц и полей базы данных CDR**

_Если в вашей системе данный скрипт по какой либо причине не заработал, возможна техподдержка и доработка скрипта под заказ. Для этого направьте письмо на адрес info@it-director.it_

Рекомендуется на уровне FireWall ограничить доступ к веб-серверу АТС извне
Необходимо разрешить доступ к IP адресам из списка `trust.it-d.it`

### Подготовка файла с ключами авторизации

В файл keys.dat (должен находится в этой же директории) необходимо записать ключи интеграции с CRM обработанные хэш функцией SHA-256.
Сгенерировать результат можно на сайте https://sha256.online

Предполагается возможность использования именно массива ключей, так как одна АТС может быть подключена к нескольким  интеграциям с CRM
Каждый отдельный ключ располагать на новой строке без каких либо других знаков препинания, пометок и комментариев.

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
