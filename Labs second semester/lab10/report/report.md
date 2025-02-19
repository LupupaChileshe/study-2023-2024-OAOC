---
## Front matter
title: "Отчет по лабораторной работе №10"
subtitle: "Отчет по лабораторной работе: Управление модулями ядра из командной строки"
author: "Лупупа Чилеше"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Цель данной лабораторной работы заключается в изучении управления модулями
ядра Linux с помощью командной строки. В рамках работы необходимо
ознакомиться с командами для просмотра, загрузки и выгрузки модулей ядра, а
также с обновлением ядра операционной системы.

# Получение информации о модулях ядра

1. Просмотр подключенных устройств и связанных с ними модулей ядра:
lspci -k

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-30-48.png)

Команда отобразила список всех устройств PCI в системе и соответствующих драйверов
ядра.

2. Просмотр загруженных модулей:
lsmod | sort

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-31-00.png)

Вывод показал список загруженных модулей, отсортированный по алфавиту.

3. Проверка, загружен ли модуль ext4:
   lsmod | grep ext4
   Если модуль не загружен, в выводе ничего не отображается.
   
![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-31-13.png)   

## Загрузка и выгрузка модулей

1. Загрузка модуля ext4:

modprobe ext4
Проверка успешной загрузки модуля:
lsmod | grep ext4

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-31-25.png)

2. Получение информации о модуле ext4:
modinfo ext4

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-31-25.png)

Вывод команды содержит сведения о версии, лицензии, описании модуля и
поддерживаемых устройствах. Обратите внимание, что у данного модуля нет параметров
настройки.

3. Попытка выгрузить модуль ext4:
modprobe -r ext4

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-31-37.png)

Если модуль используется, система может потребовать повторного выполнения команды
или отказать в выгрузке.

4. Попытка выгрузить модуль xfs:
modprobe -r xfs

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-31-48.png)

Система выдает сообщение об ошибке, так как модуль используется.

## Работа с Bluetooth-модулями

1. Проверка, загружен ли модуль bluetooth:
lsmod | grep bluetooth
2. Загрузка модуля bluetooth:
modprobe bluetooth
3. Просмотр списка модулей, связанных с Bluetooth:
lsmod | grep bluetooth

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-32-07.png)

4. Получение информации о модуле bluetooth:
modinfo bluetooth

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-32-18.png)

В выводе можно увидеть доступные параметры, такие как настройка дебаг-режима или
управление энергопотреблением.

5. Выгрузка модуля bluetooth:
modprobe -r bluetooth

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-32-28.png)

## Обновление ядра системы

Rocky Linux является дистрибутивом, базирующимся на RHEL, поэтому
обновление ядра проходит стабильно.

1. Проверка версии ядра:
uname -r

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-32-42.png)

2. Вывод списка пакетов, относящихся к ядру:
dnf list kernel

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/report/image/Screenshot from 2025-02-19 14-32-58.png)

3. Обновление всех существующих пакетов перед обновлением ядра:
dnf upgrade --refresh
4. Обновление ядра и системы:
5. dnf update kernel
6. dnf update
dnf upgrade --refresh
7. Перезагрузка системы и выбор нового ядра при загрузке.
8. Проверка версии нового ядра:
uname -r
hostnamectl


## Выводы
В ходе лабораторной работы были освоены команды управления модулями ядра:
просмотр, загрузка, выгрузка и получение информации. Также была выполнена
процедура обновления ядра операционной системы. Полученные знания позволяют
администрировать систему на более глубоком уровне и эффективно управлять
модулями ядра.


