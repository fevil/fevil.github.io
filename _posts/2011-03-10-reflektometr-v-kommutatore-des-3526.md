---
id: 25
title:
  - 'Интересная функция коммутатора DES-3526 '
author: fevil
layout: post
guid: http://fevil.org.ru/reflektometr-v-kommutatore-des-3526
permalink: /reflektometr-v-kommutatore-des-3526
description:
  - После обновления прошивки Dlink DES-3526 появилась возможность использовать его как рефлектометр.
keywords:
  - Dlink DES-3526, network, сети, системный администратор
robotsmeta:
  - index,follow
post_views_count:
  - 2
categories:
  - Network
tags:
  - D-link
  - Network
  - Плюшки
---
Обнаружил любознательную плюшку, работающую на последних прошивках коммутаторов  D-link DES-3526. Оказывается можно померить длину подключенного к порту кабеля или вычислить расстояние до обрыва.

<!--more-->

делается это все по команде:  **cable_diag ports N**, где **N**-номер порта. Если указать **all** то измерение пройдет на всех портах. Взял стандартный 5-ти метровый коммутационный кабель и попробовал измерить его длину, результат ниже на картинке.

* *

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/03/Снимок.png"><img class="size-full wp-image-26  aligncenter" title="cable_diag ports " src="http://fevil.org.ru/wp-content/uploads/2011/03/Снимок.png" alt="cable_diag ports 2" width="496" height="165" /></a>
</p>

* *

Если запустить команду, без кабеля, то как и следовало ожидать увидем надпись  &#8211; No Cable. На комбо-портах тоже команда не работает. Если кабель целый, без обрывов, и второй конец подключен к активному оборудованию, измерение имеет погрешности. Поначалу этот факт ввел меня в замешательство, но после прочтения принципов работы рефлектометра, все стало на свои места.

Интересная плюшка будет полезна для поиска места, где мышки прогрызли кабель, либо для определения  длин случайных огрызков витой пары. Молодцы ребята из D-link.

* *

*  
*
