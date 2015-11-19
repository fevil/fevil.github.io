---
id: 55
title: Как прошить D-link DES-3526 ?
author: fevil
layout: post
guid: http://fevil.org.ru/kak-proshit-d-link-des-3526
permalink: /kak-proshit-d-link-des-3526
robotsmeta:
  - index,follow
post_views_count:
  - 9
categories:
  - Network
---
Для того чтобы прошить коммутатор D-link DES-3526, необходимо подключить его по RS-232, настроить программу  связи через последовательный порт (minicom либо hyperterminal), и в момент загрузки коммутатора нажать **Shift+3**.

<p style="text-align: center;">
  <!--more-->Выставляем Image Option: <Create  >, Download Protocol: <Z Modem> и для ускорения процесса прошивки во времени ставим Baud Rate <115200 >. Применяем изменения и перезагружаем коммутатор D-link DES-3526. 
  
  <a href="http://fevil.org.ru/wp-content/uploads/2011/03/boot_des-3526.png"><img class="aligncenter size-full wp-image-56" title="boot_des-3526" src="http://fevil.org.ru/wp-content/uploads/2011/03/boot_des-3526.png" alt="boot_des-3526" width="381" height="176" /></a>
</p>

Далее необходимо изменить скорость подключения, для этого заходим в настройки minicom, нажатием Ctrl+A O . Выбираем пункт &#8211; &#8220;Настройка последовательного порта&#8221; и в нем, нажав клавишу &#8211; &#8220;E&#8221; выбираем нашу скорость.

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/03/minicom-115200.png"><img class="aligncenter size-full wp-image-57" title="minicom-115200" src="http://fevil.org.ru/wp-content/uploads/2011/03/minicom-115200.png" alt="minicom-115200" width="385" height="179" /></a> Следующим этапом, жмем Ctrl+A S, выбираем протокол zmodem, после чего выбираем директорию, на локальном диске, где лежит прошивка, и пишем название.
</p>

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/03/DES3526_5.01-B52.png"><img class="aligncenter size-full wp-image-59" title="DES3526_5.01-B52" src="http://fevil.org.ru/wp-content/uploads/2011/03/DES3526_5.01-B52.png" alt="DES3526_5.01-B52.had" width="425" height="31" /></a>
</p>

Нажимаем &#8211; &#8220;Enter&#8221;  и пошел процесс прошивки.

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/03/zmodem-отправка.png"><img class="aligncenter size-full wp-image-60" title="zmodem-отправка" src="http://fevil.org.ru/wp-content/uploads/2011/03/zmodem-отправка.png" alt="" width="385" height="107" /></a> В конце нажимаем любую клавишу &#8230; и снова попадаем в знакомое нам меню конфигурации загрузки коммутатора D-link DES-3526.  На этот раз выбираем Image Option: <Set_Boot>,  Select Image: <2   >, Baud Rate <9600   >. Применяем. Перезагружаем.Жмем Shift+6. Выполняем  reset factory. Готово!!
</p>
