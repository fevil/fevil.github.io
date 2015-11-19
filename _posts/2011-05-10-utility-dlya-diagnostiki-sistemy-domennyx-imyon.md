---
id: 167
title:
  - DNS lookup utility
author: fevil
layout: post
guid: http://fevil.org.ru/?p=167
permalink: /?p=167
description:
  - Обзор утилит по тестированию сервера имен.
keywords:
  - DNS lookup utility, системное администрирование, нслукап, nslookup, nslokup, dig, host
robotsmeta:
  - index,follow
post_views_count:
  - 4
categories:
  - Internet
---
<p style="text-align: justify;">
  Очень часто наблюдаю картину когда коллеги, для того, что бы определить адрес машины в сети, используют сетевую утилиту ping, их действия приводят к решению поставленной задачи, но ведь для этой цели есть специальные утилиты, поэтому считаю, что правильнее все же использовать их. Посмотрим, что у нас есть.
</p>

<p style="text-align: justify;">
  <!--more-->
  
  <a href="http://fevil.org.ru/wp-content/uploads/2011/05/исслед.jpeg"><img class="aligncenter size-full wp-image-169" title="исследователи" src="http://fevil.org.ru/wp-content/uploads/2011/05/исслед.jpeg" alt="" width="155" height="102" /></a>
</p>

<p style="text-align: justify;">
  <strong>nslookup</strong>, <strong>dig</strong> и <strong>host</strong> &#8211; троица которая, в первую очередь, помогает любому администратору диагностировать работу своего, и не только своего, сервера  имен (DNS).   Самое простое для чего можно использовать данные утилиты &#8211; сделать запрос к серверу имен для преобразования доменного имени в адрес сетевого узла. Утилита nslookup, по умолчанию, присутствует в операционных системах windows, есть во многих unixlike системах; host по умолчанию установлена на многих unixlike системах; dig &#8211; разрабатывается совместно с сервером имен bind, и так же во многих unixlike системах стоит по умолчанию.
</p>

<p style="text-align: justify;">
  Рассмотрим на практике действия, выполняемые с данными утилитами, для решения штатной задачи преобразования доменного имени в сетевой адрес:
</p>

<p style="text-align: justify;">
  <strong>nslookup:</strong>
</p>

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/05/nslookup.png"><img class="aligncenter" title="nslookup" src="http://fevil.org.ru/wp-content/uploads/2011/05/nslookup.png" alt="nslookup screen" width="318" height="141" /></a>
</p>

<p style="text-align: justify;">
  <strong>host:</strong>
</p>

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/05/host.png"><img class="aligncenter" title="host" src="http://fevil.org.ru/wp-content/uploads/2011/05/host.png" alt="host screen" width="464" height="103" /></a>
</p>

<p style="text-align: justify;">
  <strong>dig:</strong>
</p>

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/05/dig.png"><img class="aligncenter" title="dig" src="http://fevil.org.ru/wp-content/uploads/2011/05/dig.png" alt="" width="477" height="254" /></a>
</p>

<p style="text-align: justify;">
  Как видно по снимкам экрана, чтобы определить адрес по доменному имени, как впрочем и для обратной процедуры, нет необходимости для указания дополнительных параметров утилитам. Утилита host дополнительно сообщает нам MX записи  для исследуемого домена. Это еще одна функция, для которой очень часто приходится использовать троицу.  Чтобы просмотреть MX записи, с помощью nslookup &#8211; необходимо необходимо попасть в интерактивный режим работы утилиты, запустив nslookup в консоли и без параметров. Далее необходимо поменять тип запроса по умолчанию, выполнив команду <strong>set type=MX</strong> (можно поставить type=ALL, если необходимо получить записи всех типов). Следующим действием необходимо ввести доменное имя и просмотреть результат. Чтобы получить информацию о MX записи, с помощью <strong>dig</strong> &#8211;  необходимо произвести запрос вида: dig w3c.org MX.
</p>

<p style="text-align: justify;">
  Утилиты для диагностики системы доменных имён  очень просты в использовании. Был рассмотрен лишь базовый функционал, в станицах помощи по каждой утилите подробно описаны расширенные функции.
</p>