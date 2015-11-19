---
id: 269
title:
  - DES-3526 прошиваем используя TFTP
author: fevil
layout: post
guid: http://fevil.org.ru/kak-proshit-d-link-des-3526-chast-2
permalink: /kak-proshit-d-link-des-3526-chast-2
keywords:
  - D-link DES-3526, fevil, системный администратор, download firmware_fromTFTP
robotsmeta:
  - index,follow
post_views_count:
  - 65
categories:
  - Network
tags:
  - D-link
  - md5sum
  - Песочница
---
[Ранее][1] рассматривался вопрос о прошивке коммутатора через интерфейсный кабель, а в заметке[ о сохранении конфигурации][2] коммутатора D-link DES-3526, был рассмотрен вопрос об поднятии tftp-сервера,поэтому рассмотрим теперь, как можно обновить программное обеспечение коммутатора D-link DES-3526 с  его помощью. <!--more-->Для этого необходимо запросить новую прошивку на русскоязычном форуме производителя. После обработки запроса модератором на почтовый ящик будет выслан архив с прошивкой и контрольной суммой прошивки. Чтобы убедится в том, что целостность прошивки не нарушена сверим контрольные суммы. Для этого распакуем архив

* DES3526R6_6.10-B23.zip* (на момент написания заметки был такой) ,  в рабочую директорию нашего tftp-сервера  */home/tftp*, затем перейдем в нее и выполним команду:

<p style="padding-left: 300px;">
  <strong>md5sum -c  md5sum.txt</strong>
</p>

Успешное завершение которой соответствует выводу на экран имени файла прошивки коммутатора и слова OK, подтверждая целостность данных.  Файл *md5sum.txt* можно удалить и приступить к обновлению программного обеспечения коммутатора.

Заходим в консоль управления коммутатором D-link DES-3526 по сети либо через интерфейс RS-232, и выполняем комману:

<p style="text-align: center;">
  <strong>DES-3526:admin#download firmware_fromTFTP 172.16.0.33 DES3526R6_6.10-B23.had image_id 1</strong>
</p>

<p style="text-align: left;">
  в результате выполнения которой скачается образ <em>DES3526R6_6.10-B23.had </em>с TFTP сервера 172.16.0.33. Теперь необходимо указать загрузку с этого образа и сохранить изменения:
</p>

<p style="text-align: left; padding-left: 150px;">
  <strong>DES-3526:admin#config firmware image_id 1 boot_up</strong>
</p>

<p style="text-align: left; padding-left: 150px;">
  <strong>DES-3526:admin#save</strong>
</p>

<p style="text-align: left;">
  Перезагружаем коммутатор D-link DES-3526 и смотрим версию программного обеспечения.<strong><br /> </strong>
</p>

<p style="text-align: left; padding-left: 150px;">
  <p style="text-align: left; padding-left: 150px;">

 [1]: http://fevil.org.ru/network/kak-proshit-d-link-des-3526/ "Как прошить коммутатор DES-3526"
 [2]: http://fevil.org.ru/network/kak-proshit-d-link-des-3526/
