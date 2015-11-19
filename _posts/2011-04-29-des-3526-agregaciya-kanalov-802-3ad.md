---
id: 145
title:
  - Увеличиваем пропускную способность
author: fevil
layout: post
guid: http://fevil.org.ru/des-3526-agregaciya-kanalov-802-3ad
permalink: /des-3526-agregaciya-kanalov-802-3ad
description:
  - Заметка об агрегации каналов связи.
keywords:
  - 802.3ad, DES-3526, d-link, dlink, корпоротивные сети
robotsmeta:
  - index,follow
post_views_count:
  - 4
categories:
  - Network
tags:
  - D-link
  - Debian
  - Network
  - Плюшки
---
<p style="text-align: justify;">
  Настраивал недавно сетевое хранилище, которое имеет два адаптера, и увидел в настройках пункт, который позволяет объединить их в один с увеличением скорости и надежности, но для этого необходимо соответствующим образом настроить коммутатор (у меня это D-link DES 3526).  Рассмотрим как это делается.
</p>

<p style="text-align: justify;">
  <!--more-->
</p>

<p style="text-align: justify;">
  Для решения данной задачи применяется технология объединения  нескольких физических каналов в один &#8211; IEEE 803.2ad. Данная технология ограничена скоростью 8Гб.  Выбираем два порта на коммутаторе в которые подключаем наше устройство и конфигурируем следующим образом:
</p>

<p style="padding-left: 150px;">
  <strong>config link_aggregation algorithm mac_destination</strong>
</p>

<p style="padding-left: 150px;">
  <strong>create link_aggregation group_id 10 type lacp</strong>
</p>

<p style="padding-left: 150px;">
  <strong>config link_aggregation group_id 10 ports 9-10</strong>
</p>

<p style="padding-left: 150px;">
  <strong>config lacp_port 9-10 mode active</strong>
</p>

<p style="text-align: justify;">
  Сохраняем конфигурацию. Ждем некоторое время и проверяем работу устройства (мне пришлось ждать около пяти минут).  Следом за сетевым хранилищем аналогичным образом был подключен один из серверов, работающий под управлением Windows Server 2k8, агрегирование сетевых карт осуществлялось с помощью утилиты  &#8211; hp network configuration utility.
</p>

<p style="text-align: justify;">
  Вышеописанными действиями удалось добиться повышения надежности и пропускной способности канала связи с сетевым хранилищем. Следующим этапом планирую разобраться с данным стандартов в Debian GNU/Linux, а также объединить два коммутатора D-link DES 3526.
</p>

<p style="text-align: justify;">
  <strong><br /> </strong>
</p>
