# Домашнее задание к занятию «Репликация и масштабирование. Часть 1»

### Задание 1

На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.

*Ответить в свободной форме.*

### Решение 1

Репликация типа master-slave обычно используется для обеспечения отказоустойчивости приложений и распределения нагрузки между несколькими серверами и репликами.
При данном типе репликации может быть один master-сервер, на котором производятся все изменения в данных, и множество slave-серверов, которые копируют данные с master-сервера. Операции чтения из базы данных производятся со slave-серверов.
Данный вид репликации лучше всего использовать, если производятся преимущественно операции чтения из БД.

Репликация master-master позволяет копировать данные с одного сервера на другой. Она повышает эффективность при обращении к данным.
При данном типе репликации каждый сервер является одновременно master-ом и slave-ом. Репликация происходит в обе стороны.
Данный вид репликации подходит для серверов, обслуживающих определенную зону. При падении одного из зональных серверов БД возможно подключение к серверу другой зоны.

---

### Задание 2

Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.

*Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.*

### Решение 2

Конфигурационные файлы БД MySQL для репликации в режиме master-slave:

[Dockerfile для master](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_slave/dockerfile_master)

[Конфиг-файл для репликации master](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_slave/master.cnf)

[Cкрипт для создания пользователя для репликации master](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_slave/master.sql)

[Dockerfile для slave](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_slave/dockerfile_slave)

[Конфиг-файл для репликации slave](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_slave/slave.cnf)

[Cкрипт для создания пользователя для репликации slave](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_slave/slave.sql)

Запустил базы данных, проверим работу репликации.

Создал базу данных на master-сервере и таблицу в ней, внес записи в таблицу:
![1](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/scshots/12-06_t2-master.png)

Смотрим состояние реплики на slave:
![2](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/scshots/12-06_t2-slave1.png)
![3](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/scshots/12-06_t2-slave2.png)

Состояние и режимы работы серверов:
![4](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/scshots/12-06_t2-master-slave-status.png)

---

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

---

### Задание 3* 

Выполните конфигурацию master-master репликации. Произведите проверку.

*Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.*

### Решение 3

Конфигурационные файлы БД MySQL для репликации в режиме master-master:

[Dockerfile для master1](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_master/dockerfile_mm1)

[Конфиг-файл для репликации master1](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_master/master1.cnf)

[Cкрипт для создания пользователя для репликации master1](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_master/master1.sql)

[Dockerfile для master2](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_master/dockerfile_mm2)

[Конфиг-файл для репликации master2](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_master/master2.cnf)

[Cкрипт для создания пользователя для репликации master2](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/master_master/master2.sql)

Запустил базы данных, проверим работу репликации.

Создал базу данных на master1-сервере и таблицу в ней, внес записи в таблицу:
![1](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/scshots/12-06_t3-1.png)

Смотрим состояние реплики на master-2:
![2](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/scshots/12-06_t3-2.png)
![3](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/scshots/12-06_t3-3.png)

Добавляем запись в таблицу на сервере master2 и читаем таблицу на сервере master1:
![4](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/scshots/12-06_t3-4.png)

Состояние и режимы работы серверов:
![5](https://github.com/murtazinilyas/12-06_SQL_replica/blob/main/scshots/12-06_t3-5.png)
