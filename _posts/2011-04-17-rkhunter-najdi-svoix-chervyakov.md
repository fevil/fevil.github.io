---
id: 119
title: 'rkhunter &#8211; Найди своих червяков'
author: fevil
layout: post
guid: http://fevil.org.ru/rkhunter-najdi-svoix-chervyakov
permalink: /rkhunter-najdi-svoix-chervyakov
post_views_count:
  - 1
categories:
  - Linux
tags:
  - Debian
  - Linux
  - ubuntu
  - Песочница
---
Если враг силен &#8211; обойди его, если сердит &#8211; раздразни его, если равен тебе &#8211; сражайся, если нет &#8211; унизь его. Так учит японская мудрость. Рассмотрим сегодня утилиту, которая, сможет нам указать нам, на слабость наших механизмов зашиты от проникновения посторонних. Очень хочу верить, что это лишь голая теория, и нам никогда не придется анализировать журналы, взломанных серверов.<!--more-->

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/04/червяк.jpeg"><img class="aligncenter size-full wp-image-120" title="червяк" src="http://fevil.org.ru/wp-content/uploads/2011/04/червяк.jpeg" alt="червяк" width="182" height="143" /></a>
</p>

<p style="text-align: justify;">
  <strong>rkhunter</strong> &#8211; сканер руткитов, уязвимостей и эксплоитов. Утилита которая должна запускаться, и изучением отчетов которой, должен заниматься системный администратор ежедневно. Какова бы ни была система безопасности, обойти ее, можно всегда, все зависит от настойчивости и средств злоумышленника. Рассматриваемая утилита, похожа на антивирус, имеет базу известных rootkit-ов (rootkit, согласно википедии, это  &#8211; программа или набор программ для скрытия следов присутствия злоумышленника или вредоносной программы в системе). Она выявляет изменения в системных файлах.
</p>

<p style="text-align: justify;">
  Для установки утилиты в Debian GNU/Linux, и на нем основанных дистрибутивах, необходимо выполнить команду:
</p>

<p style="text-align: center;">
  <strong>sudo apt-get install rkhunter</strong>
</p>

<p style="text-align: justify;">
  После установки, необходимо создать базу свойств, всех директорий и файлов в нашей системе, и заодно проверить наличие обновлений:
</p>

<p style="text-align: center;">
  <strong>sudo rkhunter &#8211;propupd  &#8211;update</strong>
</p>

<p style="text-align: justify;">
  Мне нравиться когда сервера пишут мне письма, для того чтобы отчеты rkhunter&#8217;а приходили нам по почте, укажем наш почтовый ящик в конфигурационном файле <strong>/etc/rkhunter.conf </strong>
</p>

<p style="text-align: center;">
  <strong>MAIL-ON-WARNING=admin@admindomain</strong>
</p>

<p style="text-align: justify;">
  Теперь можно первый раз запустить проверку
</p>

<p style="text-align: center;">
  <strong>sudo r</strong><strong>khunter -c</strong>
</p>

<p style="text-align: left;">
  В ходе проверки необходимо несколько раз нажать клавишу Enter для продолжения, и почитывать выводимые на экран сообщения. Осталось прописать задание в cron, чтобы проверка выполнялась каждую ночь в 01-00 &#8211; <strong>crontab -e</strong>:
</p>

<p style="text-align: center;">
  <strong>0 01 * * *  /usr/bin/rkhunter -c  &#8211;cronjob</strong>
</p>
