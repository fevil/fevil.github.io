---
id: 64
title:
  - vlan on debian and des-3526
author: fevil
layout: post
guid: http://fevil.org.ru/?p=64
permalink: /?p=64
keywords:
  - '802.3ad, DES-3526, d-link, dlink, корпоротивные сети, vlan, настройка vlan, виланы '
robotsmeta:
  - index,follow
description:
  - 'обзор частного случая применения технологии vlan  '
post_views_count:
  - 3
categories:
  - Network
tags:
  - D-link
  - Debian
  - Linux
  - Network
  - ubuntu
  - Плюшки
---
Встала необходимость поделится имеющимся интернет каналом с соседними по зданию офисами. Решение казалось бы очевидное &#8211; добавить сетевую  карту в маршрутизатор, в роли которого выступает старенький PC, с установленным на него Debian GNU Linux, добавить правило на межсетевом экране и жить спокойно. Но свободного PCI-слота, для установки, не оказалось, следовательно необходимо было найти другое решение.

<!--more-->

Было решено рапсилить коммутатор D-link DES-3526 на несколько vlan. Получилась следующая схема.

[<img class="aligncenter size-full wp-image-76" title="network-vlan-fevil-org-ru" src="http://fevil.org.ru/wp-content/uploads/2011/04/network-vlan-fevil-org-ru.png" alt="network-vlan-fevil-org-ru" width="410" height="305" />][1]Настройки Linux-системы.

Первым делом устанавливаем пакет vlan:

<p style="text-align: center;">
  <strong>apt-get install vlan</strong>
</p>

<p style="text-align: justify;">
  Интерфейс который подключен к коммутатору  D-link DES-3526 &#8211; <strong>eth1</strong>. Для его настройки внесем следующие изменения в конфигурационный файл /etc/network/interfaces :
</p>

<p style="text-align: justify; padding-left: 120px;">
  auto eth1 vlan2 vlan3 vlan4 vlan5<br /> iface vlan2 inet static<br /> address 10.10.10.1<br /> netmask 255.255.252.0<br /> vlan_raw_device eth1
</p>

<p style="padding-left: 120px;">
  iface vlan3 inet static<br /> address 10.3.1.1<br /> netmask 255.255.255.248<br /> vlan_raw_device eth1
</p>

<p style="padding-left: 120px;">
  iface vlan4 inet static<br /> address 10.4.1.1<br /> netmask 255.255.255.240<br /> vlan_raw_device eth1
</p>

<p style="padding-left: 120px;">
  iface vlan5 inet static<br /> address 10.5.1.1<br /> netmask 255.255.255.0<br /> vlan_raw_device eth1
</p>

<p style="text-align: justify;">
  После сохранения изменений перезапускаем  службу сети командой &#8211;  /etc/init.d/networking restart. Теперь мы имеем поднятый интерфейс eth1, без присвоенного сетевого адреса и новые интерфейсы с именами vlan2, vlan3 &#8230; vlan5. Просмотреть можно выполнив в консоли команду ifconfig.
</p>

<p style="text-align: justify;">
  Настройки коммутатора D-link DES-3526:
</p>

<p style="text-align: justify;">
  Маршрутизатор, на базе Debian GNU Linux,  подключен в 25-ый порт коммутатора, он у нас будет тэгированным для всех.  В vlan  2 будут порты в которые, подключены сетевые устройства из моей сети. Для остальных офисов были выделены порты 9,10,11 и созданы vlan&#8217;ы 3,4,5. Ниже приводится листинг настройки коммутатора D-link DES-3526.
</p>

<p style="text-align: justify; padding-left: 120px;">
  &nbsp;
</p>

<p style="text-align: justify; padding-left: 120px;">
  config vlan vlanid 1 delete 1-26
</p>

<p style="text-align: justify; padding-left: 90px;">
  &nbsp;
</p>

<p style="text-align: justify; padding-left: 120px;">
  create vlan MyNet tag 2
</p>

<p style="text-align: justify; padding-left: 120px;">
  create vlan Office1 tag 3
</p>

<p style="text-align: justify; padding-left: 120px;">
  create vlan Office2 tag 4
</p>

<p style="text-align: justify; padding-left: 120px;">
  create vlan Office3 tag 5
</p>

<p style="text-align: justify; padding-left: 120px;">
  &nbsp;
</p>

&nbsp;

<p style="text-align: justify; padding-left: 120px;">
  config vlan vlanid 2 add untagged 1-8,12-24,26
</p>

<p style="text-align: justify; padding-left: 120px;">
  config vlan vlanid 2 add tagged 25
</p>

<p style="text-align: justify; padding-left: 120px;">
  &nbsp;
</p>

<p style="text-align: justify; padding-left: 120px;">
  config vlan vlanid 3 add untagged 9
</p>

<p style="text-align: justify; padding-left: 120px;">
  config vlan vlanid 3 add tagged 25
</p>

<p style="text-align: justify; padding-left: 120px;">
  &nbsp;
</p>

<p style="text-align: justify; padding-left: 120px;">
  config vlan vlanid 4 add untagged 10
</p>

<p style="text-align: justify; padding-left: 120px;">
  config vlan vlanid 4 add tagged 25
</p>

<p style="text-align: justify; padding-left: 120px;">
  &nbsp;
</p>

<p style="text-align: justify; padding-left: 120px;">
  config vlan vlanid 5 add untagged 11
</p>

<p style="text-align: justify; padding-left: 120px;">
  config vlan vlanid 5 add tagged 25
</p>

<p style="text-align: justify; padding-left: 120px;">
  save
</p>

<p style="text-align: justify;">
  Теперь если на коммутаторе выполнить команду show vlan, то можно увидеть результат выполненных действий. Чтобы была возможность управлять коммутатором DES-3526, из  моей сети, необходимо задать системный интерфейс в vlan&#8217;е 2:
</p>

<p style="text-align: justify; padding-left: 120px;">
  config ipif System vlan MyNet ipaddress 10.10.10.35/22 state enable
</p>

<p style="text-align: justify; padding-left: 120px;">
  delete iproute default
</p>

<p style="text-align: justify; padding-left: 120px;">
  create iproute default 10.10.10.1
</p>

<p style="text-align: justify;">
  Раздача интернета на данном этапе выполнена &#8220;натированием&#8221;, с помощью правил iptables. Следующим этапом планируется настроить балансировку канала между под-сетями и возможно внедрение прозрачного прокси сервера.
</p>

<p style="text-align: justify;">
  &nbsp;
</p>

<p style="text-align: justify;">
  &nbsp;
</p>

<p style="text-align: justify;">
  &nbsp;
</p>

<p style="text-align: justify; padding-left: 60px;">
  &nbsp;
</p>

<p style="text-align: justify; padding-left: 60px;">
  &nbsp;
</p>

<p style="text-align: justify; padding-left: 60px;">
  &nbsp;
</p>

<p style="text-align: justify;">
  &nbsp;
</p>

<p style="text-align: justify; padding-left: 120px;">
  &nbsp;
</p>

<p style="text-align: justify; padding-left: 120px;">
  &nbsp;
</p>

 [1]: http://fevil.org.ru/wp-content/uploads/2011/04/network-vlan-fevil-org-ru.png