## MongoDB
Имеет одну мастер-ноду, при потере свзи между узлами не принимаются запросы на запись, тем самым гарантируя согласованность данных и устойчивость к распределению
MongoDB является PC-системой

## MSSQL
Реляционная база данных, поддерживает требования ASID, данные остаются согласованными, но при разделении сети взамодействие с ситемой становится невозможным.
MSSQL является CA-системой

## Cassandra
Cassandra использует схему репликации master-master. Каждый узел является самодостаточным, но не гарантирует согласованность данных. При разделении сети система продолжает работать в режиме чтения/записи
Cassandra является AP системой
