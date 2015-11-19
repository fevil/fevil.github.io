---
id: 244
title:
  - 'conky - метеосводка на виду'
author: fevil
layout: post
guid: http://fevil.org.ru/?p=244
permalink: /?p=244
robotsmeta:
  - index,follow
keywords:
  - conky, fevil, linux, системное администрирование
post_views_count:
  - 7
categories:
  - desktop
tags:
  - apt
  - conky
  - gkrellm
  - Linux
  - ubuntu
  - десктоп
  - Песочница
---
<p style="text-align: justify;">
  В последнее время зачистил с активным отдыхом по выходным, в связи с чем, очень часто стал посещать ресурсы с прогнозом погоды. Каждый раз заходить и выбирать нужный город, да и попросту выполнять постоянно одинаковые действия &#8211; не по душе, поэтому решил отображать метеосводку в уголке своего рабочего стола. Посмотрим как это выглядело.<!--more-->В голове крутились названия двух инструментов, с помощью которых возможно реализовать задуманное &#8211; gkrellm и conky. Оба являются системным монитором, которые позволяют отображать различную информацию на рабочем столе. Первым делом установил  gkrellm, стандартным способом:
</p>

<p style="text-align: center;">
  <strong>:~$ sudo apt-get install gkrellm</strong>
</p>

<p style="text-align: left;">
  И к нему дополнительно расширение под названием<em> gkrellweather</em>
</p>

<p style="text-align: center;">
  <strong>:~$ sudo apt-get install gkrellweather</strong>
</p>

<p style="text-align: left;">
  которое необходимо дополнительно включить в настройках. Найти ближайшую метеостанцию по ссылке, которая приводиться в окне настроек, ориентиром служить ближайший аэропорт. Расширение рабочее, но малоинформативное, да не лежала изначально у меня душа к  <em>gkrell</em>. Поэтому перешел к установке и настройке  <em>conky</em>, так как видел очень красивые снимки экрана с ним.
</p>

<p style="text-align: left;">
  Установка стандартная: для начала:
</p>

<p style="text-align: center;">
  <strong>sudo apt-get install conky, </strong>
</p>

<p style="text-align: left;">
  <strong> </strong>а следом копируем конфигурационный файл в домашнюю директорию пользователя под которым работаем:
</p>

<p style="text-align: center;">
  <strong>cat /etc/conky/conky.conf > </strong><strong>~/.conkyrc.</strong>
</p>

<p style="text-align: justify;">
  Теперь можно первый раз запустить системный монитор, он выведет нам информацию о расходовании дискового пространства, загрузки процессора, расходовании оперативной памяти и раздела подкачки, время работы системы и т.п., при этом будет жуткое мерцание, от которого необходимо избавиться добавив в конфигурационный файл <em>.conkyrc</em> параметр:
</p>

<p style="text-align: center;">
  <strong>double_buffer yes</strong>
</p>

<p style="text-align: left;">
  Мерцание исчезло. Начались поиски способа, которым будет достигнута основная цель &#8211; отображение метеосводки на рабочем столе. Первым делом попробовал как написано<a href="http://www.nixp.ru/articles/%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%BD%D1%8B%D0%B9-%D0%BC%D0%BE%D0%BD%D0%B8%D1%82%D0%BE%D1%80-Conky-%D0%BF%D1%80%D0%BE%D1%81%D1%82%D0%BE%D1%82%D0%B0-%D0%B8-%D0%BC%D0%BE%D1%89%D1%8C.html" target="_blank"><strong> </strong>тут</a>, только с некоторыми доработками, а именно &#8211; переменная CURL в скрипте приобрела следующий вид<strong>:</strong>
</p>

<p style="text-align: center;">
  <strong>CURLURL=&#8221;http://xoap.weather.com/weather/local/$LOCID?cc=*&prod=xoap&par=1004517364&key=a29796f587f206b2&dayf=3&unit=m&#8221;</strong>
</p>

<p style="text-align: left;">
  и файл <em>weather.xslt </em>был скачан <a href="http://malcolm.ru/weather.xslt" target="_blank">отсюда</a>. Убрав из .conkyrc лишние датчики дописал в самый конец вывод погоды:
</p>

<p style="text-align: center;">
  <strong>${color #ffff00}${execi 1800 ~/.config/conky/weather.sh}</strong>
</p>

<p style="text-align: center;">
  <a href="http://fevil.org.ru/wp-content/uploads/2011/06/conky_weather1.png"><img class="aligncenter size-full wp-image-247" title="conky_weather1" src="http://fevil.org.ru/wp-content/uploads/2011/06/conky_weather1.png" alt="conky_weather1" width="330" height="123" /></a>
</p>

<p style="text-align: left;">
  Погода представляется в текстовом виде, цель достигнута, но удовлетворения нет. Хочется графики. Продолжаю поиски и пробую как написано <a href="http://zenux.ru/articles/8/" target="_blank">тут</a>, только захватываю  и вывожу две картинки, погоду и график температур<strong>, </strong>дописав в самый низ <em>.conkyrc </em>следующие несколько строчек<strong>:</strong>
</p>

<p style="text-align: left; padding-left: 150px;">
  <strong>$hr</strong><br /> <strong>${color #ffffff}${execi 600 wget -O ~/.conkyweather.gif http://informer.gismeteo.ru/new/5106-36.GIF}</strong><br /> <strong>${image ~/.conkyweather.gif -p 0,635 -f 300}</strong>
</p>

<p style="text-align: left; padding-left: 150px;">
  <p>
    <strong>${color #ffffff}${execi 600 wget -O ~/.conkyweather2.gif http://informer.gismeteo.ru/new/G34720-2.GIF}</strong><br /> <strong>${image ~/.conkyweather2.gif -p 0,735 -f 300}</strong>
  </p>
  
  <p style="text-align: center;">
    <a href="http://fevil.org.ru/wp-content/uploads/2011/06/conky_weather2.png"><img class="aligncenter size-full wp-image-248" title="conky_weather2" src="http://fevil.org.ru/wp-content/uploads/2011/06/conky_weather2.png" alt="conky_weather2" width="323" height="427" /></a>
  </p>
  
  <p style="text-align: left;">
    Результат получился графический, но чего то  не хватает, по-прежнему душа не радуется. Пробую forecast &#8211; сценарий, написанный на языке python  для вывода погоды монитором conky. Для этого добавляю репозитории:
  </p>
  
  <p style="text-align: center;">
    <strong>:~$ sudo add-apt-repository ppa:conky-companions/ppa </strong>
  </p>
  
  <p style="text-align: left;">
    Обновляю информацию о пакетах<strong>:</strong>
  </p>
  
  <p style="text-align: center;">
    <strong>:~$ sudo apt-get update</strong>
  </p>
  
  <p style="text-align: left;">
    И устанавливаю <em>forecast:</em>
  </p>
  
  <p style="text-align: center;">
    <em> </em> <strong>:~$ sudo apt-get install conkyforecast</strong>
  </p>
  
  <p style="text-align: left;">
    Копирую конфигурационный файл:
  </p>
  
  <p style="text-align: center;">
    <strong>cp /usr/share/conkyforecast/conkyForecast.config ~/.conkyForecast.config</strong>
  </p>
  
  <p style="text-align: center;">
    <p style="text-align: center;">
      <a href="http://fevil.org.ru/wp-content/uploads/2011/06/conky_weather3.png"><img class="aligncenter size-full wp-image-250" title="conky_weather3" src="http://fevil.org.ru/wp-content/uploads/2011/06/conky_weather3.png" alt="conky_weather3" width="248" height="199" /></a>
    </p>
    
    <p style="text-align: left;">
      В итоге поставленная цель достигнута и душа удовлетворена.
    </p>
    
    <p style="text-align: left;">
      <p style="text-align: left;">
        <strong><br /> </strong>
      </p>
      
      <p style="text-align: left;">