---
id: 227
title:
  - DES-3526 Сохраняем конфигурацию на tftp сервер.
author: fevil
layout: post
guid: http://fevil.org.ru/des-3526-rezervnoe-kopirovanie-konfiguracii
permalink: /des-3526-rezervnoe-kopirovanie-konfiguracii
robotsmeta:
  - index,follow
description:
  - DES-3526 Сохраняем конфигурацию на tftp сервер.
keywords:
  - atftpd, des3526, dlink, коммутатор
post_views_count:
  - 3
categories:
  - Network
tags:
  - D-link
  - Debian
  - Network
  - ubuntu
  - Песочница
---
<p style="text-align: justify;">
  Рассмотрим небольшой пример, как сохранить настройки конфигурации коммутатора D-link DES-3526, на предварительно установленный север tftp.  Установим штатными средствами atftpd: <strong>sudo apt-get install atftpd. </strong>
</p>

<p style="text-align: justify;">
  <strong> </strong> <!--more-->Конфигурация находится в файле /etc/default/atftpd, что несколько неожиданно. Для запуска в режиме демона изменим параметр
</p>

<p style="padding-left: 60px; text-align: justify;">
  <strong>USE_INETD=true,</strong> на
</p>

<p style="padding-left: 60px; text-align: justify;">
  <strong>USE_INETD=false</strong>.
</p>

<p style="text-align: justify;">
  Изменим путь к директории с загружаемыми/отдаваемыми  файлами, например /home/tftp. Создадим директорию и  разрешим туда запись.
</p>

<p style="padding-left: 60px; text-align: justify;">
  <strong>mkdir /home/tftp</strong>
</p>

<p style="padding-left: 60px; text-align: justify;">
  <strong>chmod 777 /home/tftp</strong>
</p>

<p style="text-align: justify;">
  Перезапустим демон atftpd:  <strong>/etc/init.d/atftpd restart</strong>. При наличии в системном журнале сообщения об ошибке вида &#8211; <em>atftpd: can&#8217;t bind port :69/udp, </em>необходимо перезапустить inetd. На этом этапе мы получили tftp сервер ожидающий подключений.
</p>

<p style="text-align: justify;">
  Подключаемся к консоли управления коммутатором D-link DES-3526. Для сохранения конфигурации выполняем комманду, в которой необходимо указать: адрес tftp сервера и имя под которым сохраняем конфигурацию:
</p>

<p style="padding-left: 60px; text-align: justify;">
  <strong>DES-3526:admin#</strong>upload cfg_toTFTP 172.16.0.172 des3526-manager02-30052011
</p>

<p style="text-align: justify;">
  Для восстановления конфигурации после сбоя, либо замены коммутатора используется команда:
</p>

<p style="padding-left: 60px; text-align: justify;">
  <strong>DES-3526:admin#</strong>download cfg_fromTFTP 172.16.0.172 des3526-manager02-30052011
</p>

<p style="text-align: justify;">
  Как всегда &#8211; ничего сложного. Напомню что данные команды справедливы для большинства коммутаторов D-link. А tftp сервер можно использовать для раздачи образа операционной системы для тонких клиентов.
</p>

&nbsp;
