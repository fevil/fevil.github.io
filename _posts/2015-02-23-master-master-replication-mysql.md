---
id: 287
title: Мастер-мастер репликация mysql
author: fevil
layout: post
guid: http://fevil.org.ru/master-master-replication-mysql
permalink: /master-master-replication-mysql
custom_retweet_text:
  - 
categories:
  - Linux
tags:
  - cluster
  - Linux
  - mariadb
  - mysql
  - 'мастер - мастер репликация'
  - Плюшки
---
<p style="text-align: justify">
  Возникла необходимость в мастер-мастер репликации базы данных одного проекта. Всегда думал, что мастер &#8211; мастер репликация это чтото очень сложное, ракетное. Однако все не так страшно как кажется. <!--more-->Специфика проекта требовала использование форка mysql &#8211; mariadb и операционной системы linux centos 6.x 64-bit.
</p>

<p style="text-align: justify">
  Настройку мастер &#8211; мастер репликации mysql  начал с добавления репозитариев mariadb, так как в штатном репозитории в отличии от centos 7.x их еще нету.<br /> Для этого создал файл /etc/yum.repos.d/mariadb.repo его содержание в листинге ниже, а затем средствами yum обновил систему до актуального состояния.
</p>

<pre class="lang:default decode:true ">[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/5.5/centos6-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1</pre>

<p style="text-align: justify">
  Собственно мастер-мастер репликация mysql обеспечивается прослойкой &#8211; mariadb galera cluster. Как только найду несколько минут, обязательно расскажу как она работает и почему я выбрал именно ее. А пока опишу шаги которые я выполнил для установки и настройки данного решения чтобы оно завелось. Большинство шагов описано в официальной документации, но продублирую тут чтобы знать где искать при следующей установке.
</p>

<p style="text-align: justify">
  Собственно после обновления установил сервер mariadb, клиент mariadb, и galera средствами yum:
</p>

<pre class="lang:default decode:true">sudo yum install -y  MariaDB-client galera MariaDB-Galera-server</pre>

<p style="text-align: justify">
  Очень важно чтобы все узлы нашей сисемы имели записи либо на сервере имен, либо в файле /etc/hosts и отвечали по именам. У меня это три узла которые откликаются по именам node1(192.168.122.60),node2(192.168.122.79) и node3(192.168.122.218) далее в описании конфигурационных файлов я буду использовать эти имена.
</p>

<p style="text-align: justify">
  После установки необходимых пакетов, на всех трех серверах  необходимо выполнить первоначальную настройку mysql для этого сначала запускаем службу mysql, а затем вспомогательную утилиту инициализации. Листинг выполнения приведен ниже:
</p>

<pre class="lang:default decode:true">sudo service mysql start
Starting MySQL..... SUCCESS!

sudo mysql_secure_installation
Set root password? [Y/n] Y
New password: rootpwd
Re-enter new password:rootpwd 
Remove anonymous users? [Y/n] Y
Disallow root login remotely? [Y/n] n
Remove test database and access to it? [Y/n] Y
Reload privilege tables now? [Y/n] Y


sudo service mysql stop
Shutting down MySQL. SUCCESS!

</pre>

<p style="text-align: justify">
  После этого необходимо отредактировать конфигурационный файл  /etc/my.cnf.d/server.cnf на каждом узле, путем внесения индивидуальных изменений указанных ниже в листингах:
</p>

<pre class="lang:default decode:true">#node1
[mariadb]
query_cache_size=0
binlog_format=ROW
default_storage_engine=innodb
innodb_autoinc_lock_mode=2
wsrep_provider=/usr/lib64/galera/libgalera_smm.so
wsrep_cluster_address=gcomm://192.168.122.79,192.168.122.218
wsrep_cluster_name='mariadbgaleratest'
wsrep_node_address='192.168.122.60'
wsrep_node_name='node1'
wsrep_sst_method=rsync
wsrep_sst_auth=root:rootpwd</pre>

<pre class="lang:default decode:true">#node2
[mariadb]
query_cache_size=0
binlog_format=ROW
default_storage_engine=innodb
innodb_autoinc_lock_mode=2
wsrep_provider=/usr/lib64/galera/libgalera_smm.so
wsrep_cluster_address=gcomm://192.168.122.60,192.168.122.218
wsrep_cluster_name='mariadbgaleratest'
wsrep_node_address='192.168.122.79'
wsrep_node_name='node2'
wsrep_sst_method=rsync
wsrep_sst_auth=root:rootpwd</pre>

<pre class="lang:default decode:true">#node3
[mariadb]
query_cache_size=0
binlog_format=ROW
default_storage_engine=innodb
innodb_autoinc_lock_mode=2
wsrep_provider=/usr/lib64/galera/libgalera_smm.so
wsrep_cluster_address=gcomm://192.168.122.60,192.168.122.79
wsrep_cluster_name='mariadbgaleratest'
wsrep_node_address='192.168.122.218'
wsrep_node_name='node3'
wsrep_sst_method=rsync
wsrep_sst_auth=root:rootpwd</pre>

<p style="text-align: justify">
  Все готово для запуска mysql сервера с мастер-мастер репликацией на три узла. Для  этого на первом узле выполняем команду:
</p>

<pre class="lang:default decode:true">sudo /etc/init.d/mysql bootstrap
Bootstrapping the cluster.. Starting MySQL.... SUCCESS!</pre>

<p style="text-align: justify">
  На двух других:
</p>

<pre class="lang:default decode:true">sudo service mysql start
Starting MySQL....SST in progress, setting sleep higher. SUCCESS!</pre>

<p style="text-align: justify">
  В результате всех перечисленных выше действий имеем mysql сервер с репликацией на три узла сети. Поставленную задачу я выполнил, как оказалось она не такая сложная какой была несколько лет назад. Для тестирования корректной работы мастер &#8211; мастер mysql репликации необходимо подключиться к каждому узлу клиентом баз данных, на одном узле создать базу данных, на другом убедится что она появилась, выбрать ее создать в ней таблицу, далее посмотреть что на третьем узле есть база данных с тестовой таблицей удалить ее. Вернувшись на первую консоль убедится что база пропала и получить удовольствие от проделанной работы.
</p>

<p style="text-align: justify">
