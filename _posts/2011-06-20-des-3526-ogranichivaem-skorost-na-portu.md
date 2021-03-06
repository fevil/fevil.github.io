---
id: 256
title: 'DES-3526 &#8211; Ограничиваем скорость на порту.'
author: fevil
layout: post
guid: http://fevil.org.ru/des-3526-ogranichivaem-skorost-na-portu
permalink: /des-3526-ogranichivaem-skorost-na-portu
keywords:
  - bandwidth_control, fevil, fevilorgru, DES-3526, d-link
robotsmeta:
  - index,follow
post_views_count:
  - 6
categories:
  - Network
tags:
  - D-link
  - Network
  - пропускная способность
---
[Тут][1], ранее, рассматривал вопрос о разделении трафика между несколькими фирмами, однако вопрос о том, что делать если одна из них начнет качать торренты и не будет думать о других остался открытым. Сначала была мысль настроить какой нить шейпер на linux-машине, но потом, в целях экономии ресурсов и изучения возможностей коммутатора D-link DES-3526, полоса была ограниченна очень просто.

<!--more-->В последних прошивках коммутатора D-link DES-3526 появилась возможность ограничивать полосу пропускания по портам. Итак цель &#8211; ограничить гостевым фирмам канал в интернет до 1мб. Реализация до нельзя простая:

<p style="padding-left: 180px;">
  Входяший   поток &#8211; <strong>#config bandwidth_control 9-11 rx_rate 1</strong>
</p>

<p style="padding-left: 180px;">
  Исходящий поток <strong>- #config bandwidth_control 9-11 tx_rate 1</strong>
</p>

Таким образом гостевые сети не смогут полностью загрузить канал. Просмотреть на каких портах коммутатора D-link DES-3526, какое ограничение можно коммандой: **  
**

<p style="padding-left: 180px;">
  <strong>#show bandwidth_control</strong>
</p>

Которая покажет ограничения на всех портах. Это простейший, но очень действенный способ ограничения пропускной способности. Правильность настройки проверял с помощью speedtest.net.  Стоит заметить что в прошивках 4-той версии эта функция отсутствует, поэтому стоит  обновить прошивку коммутатора, заказав ее на форуме [d-linka.][2]**  
**

 [1]: http://fevil.org.ru/network/rasshirenie-setevyx-interfejsov-pc-router-s-pomoshhyu-des-3526-i-vlan/
 [2]: http://forum.dlink.ru/viewtopic.php?f=2&t=92700
