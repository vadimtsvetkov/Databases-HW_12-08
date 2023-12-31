#Databases HW_12-08
## VADIM TSVETKOV

«Резервное копирование баз данных»

**Задание 1.**

1.1. Восстанавление данных в полном объёме за предыдущий день:

Для данной задачи хорошо подходит дифференциальный бэкап (Differential backup). В виду не кретичности сроков востановления (в ТЗ указаны сутки), по возможности, используем холодное резервирование БД. В противном случае используем горячее резервирование БД.

1.2. Восстанавление данных за час до предполагаемой поломки:

Для данной задачи хорошо подходит инкрементный бэкап (Incremental backup). Плюс использовать горячее резервирование БД.
В зависимости от стратегии копирования могут использоваться дифференциальные и инкрементальные бэкапы, дополнительно к полным. Дифференциальный бэкап содержит изменения в данных относительно полного бэкапа, инкрементальный — содержит изменения со времени последнего частичного бэкапа – последней инкрементальной копии. Стратегическим планом резервного копирования можно рассмотреть вариант с «недельным» планом, когда в конце недели создаётся полный бэкап, в начале каждого рабочего дня создаётся дифференциальный бэкап, и каждый час в течение рабочего времени — создание инкрементального бэкапа. Такой план в самом плохом сценарии позволит сохранить данные, не потеряв более одного часа, или восстановить состояние баз на начало любого рабочего часа. А наличие дифференциального бэкапа позволит сократить количество необходимых копий, используемых при восстановлении.

В тоже самое время использование горячего резервирования позволит не останавливать технологический процесс.

Так же, на второй вопрос, можно рассмотреть выполнение горячего резервного копирования рабочей БД MySQL с помощью снапшотов LVM и сохранять данные в удаленном хранилище.

**Задание 2.**

PostgreSQL - пример команды резервирования данных и восстановления БД:

Общая форма команды для создания дампа:

pg_dump dbname> dumpfile

Общая форма команды для восстановления дампа:

psql dbname< dumpfile

**Задание 3.**

MySQL - пример команды резервирования данных и восстановления БД:

Общая форма команды для создания дампа:

mysqldump [options] db_name [tbl_name ...]

mysqldump [options] --databases db_name ...

mysqldump [options] --all-databases

Пример команды для восстановления дампа:

mysql -u root -p ${DBNAME} < ./dump.sql
