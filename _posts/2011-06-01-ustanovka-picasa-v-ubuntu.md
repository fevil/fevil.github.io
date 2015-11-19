---
id: 239
title:
  - 'picasa - наводим порядок в фотографиях'
author: fevil
layout: post
guid: http://fevil.org.ru/?p=239
permalink: /?p=239
robotsmeta:
  - index,follow
keywords:
  - picasa ubuntu, picasa debian, linux, fevil, fevilorgru
post_views_count:
  - 4
categories:
  - desktop
tags:
  - apt
  - Linux
  - ubuntu
  - Песочница
---
<p style="text-align: justify;">
  Недавно, в поисках свободного места, разбирал завалы на жестком диске своего ноутбука и обнаружил что есть несколько копий одних и тех же фотографий, в результате решил все фотографии упорядочить и систематизировать при помощи продукта от google &#8211; picasa. Чтобы его установить в Ubuntu, необходимо подключить дополнительные репозитории.
</p>

<p style="text-align: justify;">
  <!--more-->
</p>

<p style="text-align: justify;">
  Делаем это следующими командами:
</p>

<p style="text-align: justify; padding-left: 120px;">
  ~$ sudo add-apt-repository &#8220;deb http://dl.google.com/linux/deb/ testing non-free&#8221;
</p>

<p style="text-align: justify;">
  Чтобы исключить ошибку <em>NO_PUBKEY A040830F7FAC5991:</em>
</p>

<p style="text-align: justify; padding-left: 120px;">
  ~$ wget -q -O &#8211;  https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
</p>

<p style="text-align: justify;">
  В заключение обновить информацию о пакетах в репозиториях:
</p>

<p style="text-align: justify; padding-left: 120px;">
  ~$ sudo apt-get update
</p>

<p style="text-align: justify;">
  И установить picasa:
</p>

<p style="text-align: justify; padding-left: 120px;">
  ~$ sudo apt-get install picasa
</p>

&nbsp;