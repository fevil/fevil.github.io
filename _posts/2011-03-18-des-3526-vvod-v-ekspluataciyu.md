---
id: 31
title: DES-3526 ввод в эксплуатацию
author: fevil
layout: post
guid: http://fevil.org.ru/?p=31
permalink: /?p=31
robotsmeta:
  - index,follow
post_views_count:
  - 9
categories:
  - Network
tags:
  - D-link
  - Network
  - Песочница
---
При увеличении пользователей сети приходится вводить в эксплуатацию новое коммутационное оборудование. Происходит это не очень часто, поэтому каждый раз приходиться вспоминать некоторые тривиальные вещи. Для сохранности времени, ниже, опишу последовательность действий для ввода в эксплуатацию коммутатора D-link DES-3526, хотя они будут справедливы для большинства коммутаторов этой фирмы.

<!--more-->

Для настройки параметров подключаемся консольным кабелем к порту RS-232.  Запускаем** minicom -s** и настраиваем последовательный порт[<img class="aligncenter size-full wp-image-32" title="Настройка_порта_minicom" src="http://fevil.org.ru/wp-content/uploads/2011/03/Настройка_порта_minicom.png" alt="Настройка последовательного порта minicom" width="387" height="211" />][1]

выбираем: Последовательный порт &#8211; /dev/ttyS0 (просмотр возможных **dmesg | grep ttyS **);  Скорость/Четность/Биты &#8211; 9600 8N1.

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/03/Настройка_порта_minicom_результат-.png"><img class="aligncenter size-full wp-image-33" title="Настройка_порта_minicom_результат" src="http://fevil.org.ru/wp-content/uploads/2011/03/Настройка_порта_minicom_результат-.png" alt="Настройка последовательного порта в minicom - результат" width="482" height="153" /></a>
</p>

Нажимаем Enter, Сохраняем настройки, например как 3526. Далее  выходим, и запускаем  нашу конфигурацию **minicom 3526**, чтобы в будущем настраивать коммутаторы DES-3526, необходимо вводить эту команду, без предварительной настройки.

Итак собственно ввод в эксплуатацию  DES-3526. Первым делом сбросим конфигурацию до заводской, выполнив команду:** reset config**,

**[<img class="aligncenter size-full wp-image-34" title="reset_config_des-3526" src="http://fevil.org.ru/wp-content/uploads/2011/03/reset_config_des-3526.png" alt="" width="400" height="70" />][2]**дадим согласие и через несколько секунд у нас коммутатор DES-3526 с заводскими настройками.

Следующим пунктом пропишем сетевые настройки нашему устройству командой:  **config ipif System ipaddress 172.16.0.250/24**

<p style="text-align: center;">
  <strong><a href="http://fevil.org.ru/wp-content/uploads/2011/03/des3526_config_ipif_System.png"></a><a href="http://fevil.org.ru/wp-content/uploads/2011/03/des3526_config_ipif_System1.png"><img class="aligncenter size-full wp-image-36" title="des3526_config_ipif_System" src="http://fevil.org.ru/wp-content/uploads/2011/03/des3526_config_ipif_System1.png" alt="DES-3526:admin#config ipif System ipaddress 172.16.0.250/24" width="469" height="66" /></a><br /> </strong>и задаем iлюз по умолчанию: <strong>create iproute default 172.16.0.1</strong>
</p>

<p style="text-align: center;">
  <strong><a href="http://fevil.org.ru/wp-content/uploads/2011/03/create_iproute_default.png"><img class="aligncenter size-full wp-image-37" title="des-3526_create_iproute_default" src="http://fevil.org.ru/wp-content/uploads/2011/03/create_iproute_default.png" alt="DES-3526:admin#create iproute default 172.16.0.1  " width="467" height="58" /></a><br /> </strong>
</p>

<p style="text-align: left;">
  Сбор статистики и мониторинг состояния, в  DES-3526 удобно делать по <em>snmp</em> поэтому следующими командами настроим, имя коммутатора &#8211;  <strong> config snmp system_name</strong>
</p>

<p style="text-align: center;">
  <strong><a href="http://fevil.org.ru/wp-content/uploads/2011/03/des-3526_config_snmp_system_name.png"><img class="aligncenter size-full wp-image-38" title="des-3526_config_snmp_system_name" src="http://fevil.org.ru/wp-content/uploads/2011/03/des-3526_config_snmp_system_name.png" alt="" width="447" height="51" /></a></strong>условное расположение: <strong> config snmp system_location</strong>
</p>

<p style="text-align: center;">
  <strong><a href="http://fevil.org.ru/wp-content/uploads/2011/03/des-3526_config_snmp_system_location.png"><img class="aligncenter size-full wp-image-39" title="des-3526_config_snmp_system_location" src="http://fevil.org.ru/wp-content/uploads/2011/03/des-3526_config_snmp_system_location.png" alt="DES-3526:admin#config snmp system_location manager_room" width="448" height="56" /></a></strong>Для того, чтобы, событие протоколируемое в системный журнал было записано во время его возникновения, настроим синхронизацию с сервером времени: <strong>config sntp</strong>
</p>

<p style="text-align: left;">
  <strong><a href="http://fevil.org.ru/wp-content/uploads/2011/03/des-3526_config_sntp.png"><img class="aligncenter size-full wp-image-40" title="des-3526_config_sntp" src="http://fevil.org.ru/wp-content/uploads/2011/03/des-3526_config_sntp.png" alt="DES-3526:admin#config sntp primary 172.16.0.140" width="449" height="150" /></a></strong>Выберем часовой пояс: <strong>config time_zone operator + hour 3 min 0</strong>
</p>

[<img class="aligncenter size-full wp-image-42" title="des-3526_time_zone" src="http://fevil.org.ru/wp-content/uploads/2011/03/des-3526_time_zone1.png" alt="DES-3526:admin#config time_zone operator + hour 3 min 0" width="550" height="65" />][3]Включаем sntp: **enable sntp**

**[<img class="aligncenter size-full wp-image-43" title="des-3526_enable_sntp" src="http://fevil.org.ru/wp-content/uploads/2011/03/des-3526_enable_sntp.png" alt="" width="545" height="64" />][4]**

Напоследок заведем пользователя под которым будем администрировать коммутатор DES-3526: **create account admin admin **

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/03/DES-3526_create_account_admin.png"><img class="aligncenter size-full wp-image-44" title="DES-3526_create_account_admin" src="http://fevil.org.ru/wp-content/uploads/2011/03/DES-3526_create_account_admin.png" alt="DES-3526:admin#create account admin admin " width="497" height="86" /></a>Первичная настройка коммутатора  DES-3526  на этом окончена. Осталось сохранить изменения и подключать новых пользователей к сети.
</p>

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/03/admin_save.png"><img class="aligncenter size-full wp-image-45" title="admin_save" src="http://fevil.org.ru/wp-content/uploads/2011/03/admin_save.png" alt="" width="494" height="71" /></a>
</p>

 [1]: http://fevil.org.ru/wp-content/uploads/2011/03/Настройка_порта_minicom.png
 [2]: http://fevil.org.ru/wp-content/uploads/2011/03/reset_config_des-3526.png
 [3]: http://fevil.org.ru/wp-content/uploads/2011/03/des-3526_time_zone1.png
 [4]: http://fevil.org.ru/wp-content/uploads/2011/03/des-3526_enable_sntp.png