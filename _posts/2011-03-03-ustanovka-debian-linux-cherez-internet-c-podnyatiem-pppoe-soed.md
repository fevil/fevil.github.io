---
id: 9
title: Установка Debian Linux через internet c поднятием pppoe соединения
author: fevil
excerpt: 'Решил установить новый Debian 6.0, скачал установочный образ диска debian-6.0.0-i386-netinst.iso, нарезал на диск, загрузился, ставлю систему, потирая руки и возник один нюанс.  Мой провайдер предоставляет широкополосный доступ в интернет, с авторизацией, через соединение по протоколу pppoe. Полез на домашний сайт Debian, почитал руководства, в итоге установил систему, следующим образом'
layout: post
guid: http://fevil.org.ru/ustanovka-debian-linux-cherez-internet-c-podnyatiem-pppoe-soed
permalink: /ustanovka-debian-linux-cherez-internet-c-podnyatiem-pppoe-soed
robotsmeta:
  - index,follow
post_views_count:
  - 0
categories:
  - Linux
tags:
  - Debian
  - Linux
  - Network
  - pppoe
  - Песочница
---
Решил установить новый Debian 6.0, скачал установочный образ диска debian-6.0.0-i386-netinst.iso, нарезал на диск, загрузился, ставлю систему, потирая руки и возник один нюанс.  Мой провайдер предоставляет широкополосный доступ в интернет, с авторизацией, через соединение по протоколу pppoe. Полез на домашний сайт Debian, почитал руководства, в итоге установил систему, следующим образом:

<!--more-->

Грузимся с установочного диска. И выбираем самый нижний пункт &#8211; Help.

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/03/help.png"><img class="size-full wp-image-13 aligncenter" title="Выбор пункта - Help, при установке" src="http://fevil.org.ru/wp-content/uploads/2011/03/help.png" alt="Выбор пункта - Help, при установке" width="400" height="400" /></a>
</p>

<p style="text-align: center;">
  &nbsp;
</p>

<p style="text-align: left;">
  Нажимаем Enter, и далее пишем в командной строке : installgui modules=ppp-udeb
</p>

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/03/fevil_ppp-udeb.png"><img class="size-full wp-image-18 aligncenter" title="установка с загрузкой модуля ppp-udeb" src="http://fevil.org.ru/wp-content/uploads/2011/03/fevil_ppp-udeb.png" alt="установка с загрузкой модуля ppp-udeb" width="384" height="384" /></a>
</p>

Далее следует процедура обычной установки системы. Единственным отличиием будет новый пункт, в котором, будет необходимо, ввести логин и пароль к интернет подключению.
