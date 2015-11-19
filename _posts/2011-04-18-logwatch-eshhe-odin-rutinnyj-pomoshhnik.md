---
id: 124
title: 'logwatch &#8211; Еще один рутинный помощник'
author: fevil
layout: post
guid: http://fevil.org.ru/?p=124
permalink: /?p=124
post_views_count:
  - 3
categories:
  - Linux
tags:
  - Debian
  - Linux
  - Песочница
---
<p style="text-align: justify;">
  В прошлый раз мы рассмотрели <a href="http://fevil.org.ru/linux/rkhunter-najdi-svoix-chervyakov/" target="_blank">rkhunter</a>. Теперь давайте посмотрим на еще одну утилиту, которая помогает отобрать важные сообщения в огромном количестве системных журналов &#8211; <strong>logwatch</strong>. <!--more-->
  
  <a href="http://fevil.org.ru/wp-content/uploads/2011/04/писарь.jpg"><img class="aligncenter size-full wp-image-125" title="писарь" src="http://fevil.org.ru/wp-content/uploads/2011/04/писарь.jpg" alt="писарь" width="199" height="196" /></a>Данная утилита просматривает системные журналы, выбирает, в зависимости от настройки, критические сообщения и присылает их подробным отчетом на почту администратору.  В отчете так же содержаться данные о расходовании дискового пространства. И когда кто заходил по ssh.
</p>

<p style="text-align: justify;">
  Установим стандартным для Debian GNU Linux образом:
</p>

<p style="text-align: center;">
  <strong>sudo apt-get install logwatch</strong>
</p>

<p style="text-align: justify;">
  Копируем стандартный конфигурационный файл:
</p>

<p style="text-align: center;">
  <strong>cp /usr/share/logwatch/default.conf/logwatch.conf /etc/logwatch/conf/logwatch.conf</strong>
</p>

<p style="text-align: justify;">
  Создаем временную  директорию для утилиты:
</p>

<p style="text-align: center;">
  <strong> mkdir /var/cache/logwatch</strong>
</p>

<p style="text-align: justify;">
  Все готово для первого запуска. Запуск без параметров выведет отчет на стандартный ввод-вывод. Осталось добавить в cron, запуск в 01-30 каждый день:
</p>

<p style="text-align: center;">
  <strong>30 01 * * *</strong> <strong>/usr/sbin/logwatch &#8211;mailto admin@admindomain &#8211;format html</strong>
</p>

<p style="text-align: justify;">
  И начинать каждое утро, с просмотра, сообщений от серверов. Иногда можно увидеть интересные факты о попытках подбора паролей и о огромном почтовом трафике.
</p>