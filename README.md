# Язык SQL 

Язык SQL — это непроцедурный язык, который является стандартным средством работы с данными во всех реляционных СУБД. Операторы (команды), написанные на этом языке, лишь указывают СУБД, какой результат должен быть получен, но не описывают процедуру получения этого результата. СУБД сама определяет способ выполнения команды пользователя. В языке SQL традиционно выделяются группа операторов определения данных (Data Definition Language — DDL), группа операторов манипулирования данными (Data Manipulation Language — DML) и группа операторов, управляющих привилегиями доступа к объектам базы данных (Data Control Language — DCL).
К операторам языка определения данных (DDL) относятся команды для создания, изменения и удаления таблиц, представлений и других объектов базы данных. 
К операторам языка манипулирования данными (DML) относятся команды для выборки строк из таблиц, вставки строк в таблицы, обновления и удаления строк. 

# Установка ПО

Для установки PostgreSQL перейдите на сайт: https://www.enterprisedb.com/downloads/postgres-postgresql-downloads и скачайте последнюю версию дистрибутива для вашей операционной системы.

В процессе установки установите галочки на пунктах:

1. PostgreSQL Server – сам сервер СУБД
2. PgAdmin 4 – визуальный редактор SQL
3. Stack Builder – дополнительные инструменты для разработки (возможно вам они понадобятся в будущем)
4. Command Line Tools – инструменты командной строки

Установите пароль для пользователя postgres (он создается по умолчанию и имеет права суперпользователя).


# PostgreSQL

PostgreSQL — это реляционная система управления базами данных (РСУБД). 
Это означает, что это система управления данными, представленными в виде отношений (relation). Отношение — это математически точное обозначение таблицы. Хранение данных в таблицах так распространено сегодня, что это кажется самым очевидным вариантом, хотя есть множество других способов организации баз данных. 
Например, файлы и каталоги в Unix-подобных операционных системах образуют иерархическую базу данных, а сегодня активно развиваются объектно-ориентированные базы данных.
Любая таблица представляет собой именованный набор строк. Все строки таблицы имеют одинаковый набор именованных столбцов, при этом каждому столбцу назначается определённый тип данных. Хотя порядок столбцов во всех строках фиксирован, важно помнить, что SQL не гарантирует какой-либо порядок строк в таблице (хотя их можно явно отсортировать при выводе).
Таблицы объединяются в базы данных, а набор баз данных, управляемый одним экземпляром сервера PostgreSQL, образует кластер баз данных.

Рассмотрим управление и основные операции, которые можно выполнять с PostgreSQL через командную строку с помощью нескольких утилит. 
Основные инструменты управления PostgreSQL находятся в папке bin, потому все команды будем выполнять из данного каталога.

1. Перед запуском СУБД, смените кодировку для нормального отображения в Windows 10. В командной строке выполните: 
```
chcp 1251
```

2. Перейдите в каталог bin выполнив команду: 
```
CD C:\Program Files\PostgreSQL\16\bin

```

# Основные команды PostgreSQL

1. Проверка установленной версии СУБД: 
```
psql –V
```
2. После запуска сервера базы данных, выполним подключение к ней с помощью команды:

```
psql –-U postgres
```
3. Для создания новой базы данных воспользуйтесь утилитой createdb:
```
CREATE DATABASE newtestdb
```
4. Выход:
```
\q
```
5. Проверить список активных баз:
```
psql -U postgres –l
```
6. Для выводы списка пользователей и ролей в СУБД выполните команду: 
```
\du 
```
7. С помощью инструмента createuser cоздадим нового пользователя: 
```
createuser –U postgres name
```
(где name - имя нового пользователя)

8. Командой:
```
GRANT CONNECT ON DATABASE newtestdb TO name 
```
выполним привязку пользователя к базе данных

9. Для подключения к новой базе данных выполним команду:
```
\connect newtestdb
```
10. Просмотрим доступные таблицы базы:
```
\dt
```
# PgAdmin 4: Визуальный редактор для PostgreSQL
Редактор PgAdmin служит для упрощения управления базой данных PostgreSQL в понятном визуальном режиме.
1. Для запуска редактора запустите PgAdmin 4 в меню Пуск
2. Для доступа нужно ввести пароль суперпользователя postgres
3. В панели Servers вы можете раскрыть список активных БД.

# Query Tool: использование SQL запросов в PostgreSQL
1. Выберите базу данных, в панели Tools откройте Query Tool
2. Создадим таблицу сотрудников:
```
CREATE TABLE emp
(
Id SERIAL PRIMARY KEY,
FirstName CHARACTER VARYING(50),
LastName CHARACTER VARYING(50),
Email CHARACTER VARYING(50),
Age INTEGER
);
```
3. Для заполнения полей в свойствах таблицы выберите таблицу emp в разделе Schemas -> Tables. Откройте меню Object инструмент View/Edit Data.
4. После заполнения данных выполним инструментом Query простой запрос на выборку:
```
select Email from emp;
```