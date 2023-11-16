# Домашнее задание к занятию 8 "«Резервное копирование баз данных»" - `Филон Андрей`  

---

### Задание 1. Резервное копирование

### Кейс
Финансовая компания решила увеличить надёжность работы баз данных и их резервного копирования. 
Необходимо описать, какие варианты резервного копирования подходят в случаях: 

1.1. Необходимо восстанавливать данные в полном объёме за предыдущий день.  
1.2. Необходимо восстанавливать данные за час до предполагаемой поломки.  
1.3.* Возможен ли кейс, когда при поломке базы происходило моментальное переключение на работающую или починенную базу данных.  

*Приведите ответ в свободной форме.*

<ins>**Ответ:**</ins>

1.1 Дифференциальный бэкап: используем последний полный бэкап и последний дифференциальный бэкап.  
1.2 Инкрементный бэкап: созданем инкрементные бэкапы, фиксирующих изменения данных каждый час.   
1.3 Использовать репликацию: master-slave или master-master.  

---

### Задание 2. PostgreSQL

2.1. С помощью официальной документации приведите пример команды резервирования данных и восстановления БД (pgdump/pgrestore).  
2.1.* Возможно ли автоматизировать этот процесс? Если да, то как?  

*Приведите ответ в свободной форме.*

<ins>**Ответ:**</ins>

2.1 pg_dump -U username -d dbname -f backup.sql 
    pg_restore -U username -d dbname backup.sql  
где:
-U username: Имя пользователя PostgreSQL. 
-d dbname: Имя базы данных, которую мы экспортируем. 
-f backup.sql: Имя файла, в который будет сохранен дамп данных.  

2.2 Резервирование и восстановления БД в PostgreSQL можно автоматизировать с помощью скриптов и планировщиков задач. Можно создать скрипт, который будет выполнять резервирование данных с заданной периодичностью и затем сохранять дампы в указанном месте. Его можно запускать автоматически по расписанию, чтобы регулярно создавать резервные копии БД.  

---

### Задание 3. MySQL

3.1. С помощью официальной документации приведите пример команды инкрементного резервного копирования базы данных MySQL. 
3.1.* В каких случаях использование реплики будет давать преимущество по сравнению с обычным резервным копированием?  

*Приведите ответ в свободной форме.* 

<ins>**Ответ:**</ins>

3.1 mysqldump --single-transaction -u username -p dbname > backup.sql  
где:  
--single-transaction: опция выполняет резервное копирование в рамках одной транзакции, это позволяет избежать блокировок и получить согласованную копию данных. 
-u username: Имя пользователя MySQL. 
-p: При запросе пароля для доступа к базе данных. 
dbname: Имя базы данных, которую мы копируем. 
backup.sql: Имя файла, в который будет сохранен дамп данных.

---
