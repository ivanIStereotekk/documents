## Docs test-task:

Задание
1. Необходимо создать таблицу на сервере 3 столбцами
2. Реализовать загрузку данных на сервер через VBA или Python через UI. При реализации на
Python можно использовать любой UI framework
3. Сделать хранимую процедуру на MS SQL сервере для выгрузки данных за определенный
период.
4. Реализовать возможность указывать период от до (на форме VBA или значения в Excel, на
выбранной UI framework форме) и результат хранимой процедуры из 3 пункта выгружать в
новую книгу Excel. Так же реализовать форматирование отчета (закрепление шапки и
формат столбцов)
5. Отчет должен содержать столбцы: Год, Месяц, Артикул, средние продажи за год и месяц,
доля продаж артикула за выбранный период
6. Логика отчета с расчетом средних продаж и доли продаж должна быть реализована в
хранимой процедуре



-----------------------------
> [!IMPORTANT]
> Использовал Postgres SQL по тех причинам.


> [!NOTE]
> Swagger Open API в качестве UI

-----------------------------


### Создание хранимой процедуры:
```sql
CREATE OR REPLACE PROCEDURE btwdt(start_dt date, end_dt date)
LANGUAGE SQL
BEGIN ATOMIC
    SELECT article,count(id) FROM item WHERE dt BETWEEN start_dt AND end_dt GROUP BY article;
END;

```
### Вызов хранимой процедуры:


```sql
CALL btwdt('2021-02-04','2021-03-01')
```
Так выглядит Stored Procedure для Postgres SQL. 
> [!NOTE]
> Процесс создания хранимой процедуры на MS SQL немного отличается.

-----------------------------
### Сборка и запуск приложения `Docker` - `FastAPI` - `Postgres`:

> [!NOTE] 
> Как бы не рекомендуется пушить `.env`,в целях наглядности и удобства все тут. Просто скопируйте себе и все...


1 - Создайте у себя на компьютере пустой файл `.env` и скопируйте в него этот текст. Перенесите созданный вами файл в локальный репозиторий.


```java

POSTGRES_USER=ewan
POSTGRES_PASSWORD=myPassword1979
POSTGRES_HOST_DOCKER=db_postgres
POSTGRES_HOST_LOCAL=127.0.0.1
POSTGRES_PORT=5432
POSTGRES_DB_NAME=pgdb1
# CHANGE WHILE BUILDING IN DOCKER
POSTGRES_DOCKER_BUILD='True'


API_DESCRIPTION='Docs API - Тестовая работа Ивана Гончарова'
API_TITLE='eXCEL55 - Вэб сервис получения отчетов в формате файлов Excel'
CONTACT_EMAIL='iva.atp3@gmail.com'
CONTACT_NAME='Ivan Goncharov'
CONTACT_URL='http://www.iskk.space/resume'
CONTACT_PHONE='+798****'
CONTACT_CV_FILE='https://hh.ru/resume/ede10e7eff0b33519e0039ed1f695844313832'
SECRET=GghjcnjNjrty3455

```

2 - Клонируйте репозиторий в local папку - `git clone ivanIStereotekk/documents`


3 - Перейдите в репозиторий при помощи `cd /Ваш/Путь/В/папку/documents`

4 - Запустите сборку при помощи комманды ` docker compose up --build`

5 - Немного подождите как все соберется и запустится, а затем перейдите на `0.0.0.0/docs`. 

Работает !

> [!NOTE]
> На странице Swagger UI OpenAPI вы найдете инструкции как пользоваться приложением.





