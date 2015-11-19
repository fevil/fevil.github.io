---
id: 284
title: Системные сообщения через внешний сервер.
author: fevil
layout: post
guid: http://fevil.org.ru/sistemnye-soobshheniya-cherez-vneshnij-server
permalink: /sistemnye-soobshheniya-cherez-vneshnij-server
robotsmeta:
  - index,follow
description:
  - локальная почта, внешний сервер
post_views_count:
  - 2
categories:
  - Linux
---
Практически всегда, на любом, сервере есть необходимость одной или нескольким службам отправлять почтовые сообщения. Рассмотрим отправку сообщений через почтовый сервер с smtp авторизацией. <!--more-->Исторически сложилось так, что на большинстве обслуживаемых мною почтовых серверов используется postfix, поэтому решение поставленной задачи представлено с его помощью.

<img class="aligncenter size-full wp-image-286" title="localpost" src="http://fevil.org.ru/wp-content/uploads/2011/12/postman1.gif" alt="" width="142" height="150" />

Если еще не стоит, то устанавливаем штатными средствами postfix. На вопросы конфигуратора (актуально для дистрибутива debian) отвечаем &#8211; без конфигурации, а в файл **/etc/postfix/main.cf**   добавляем нужную нам конфигурацию:

<p style="padding-left: 90px;">
  relayhost = [mx.server.example]:25<br /> smtp_sasl_auth_enable = yes<br /> smtp_sasl_security_options = noanonymous<br /> smtp_sasl_password_maps = hash:/etc/postfix/passwd<br /> smtp_generic_maps=hash:/etc/postfix/name<br /> smtp_sasl_mechanism_filter = login
</p>

На этапе отладки конфигурации упорно возникала справедливая ошибка, письма отправлялись от несуществующего на почтовом сервере логина.  Для исключения этого в файле  **/etc/postfix/name**  делаем сопоставление имен локальных пользователей с учетной записью на сервере:

<p style="padding-left: 90px;">
  user@localhost.localdomain       user@server.example
</p>

localhost.localdomain и server.example берется из реальных условий. После внесения изменений в файл выполняем команду postmap.

<p style="padding-left: 90px;">
  postmap /etc/postfix/name
</p>

Аналогичным образом прописываем реквизиты доступа к почтовому серверу в файле /etc/postfix/passwd.

<p style="padding-left: 90px;">
  mx.server.example user:passwd
</p>

И снова выполняем команду postmap:

<p style="padding-left: 90px;">
  postmap /etc/postfix/passwd
</p>

Перезапускаем postfix и можно проверять работоспособность нашего решения. Сделать это можно отправив тестовое письмо с помощью консольной утилиты mail. Отмечу что задача решена наиболее универсальным способом, который позволит слать сообщения даже при отсутствии собственного почтового сервера, используя сервер провайдера или любой бесплатный.

<p style="padding-left: 90px;">
