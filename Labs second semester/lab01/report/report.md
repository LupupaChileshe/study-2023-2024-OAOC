---
## Front matter
title: "Шаблон отчёта по лабораторной работе"
subtitle: "Установка и конфигурация операционной системы на виртуальную машину"
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

Целью данной работы является приобретение практических навыков установки операционной системы на виртуальную машину, настройки минимально необходимых для
дальнейшей работы сервисов.

# Введение


Rocky Linux — это дистрибутив операционной системы на базе Linux, который является преемником CentOS. Он предназначен для серверного использования и обеспечивает стабильность и безопасность. В этом отчете описывается процесс установки Rocky Linux на сервер.

1. Скачивание образа ISO
Перейдите на официальный сайт Rocky Linux и выберите нужную версию. Скачайте ISO-образ на ваш компьютер.

2. Создание загрузочного USB или DVD
Если вы используете USB-накопитель, воспользуйтесь программами, такими как Rufus (для Windows) или Etcher (для Windows, macOS и Linux), чтобы создать загрузочный USB. Если вы используете DVD, запишите ISO-образ на диск с помощью программы для записи дисков.

3. Настройка BIOS/UEFI
Перезагрузите компьютер и войдите в настройки BIOS/UEFI. Убедитесь, что ваш компьютер настроен на загрузку с USB или DVD. Установите соответствующий приоритет загрузки.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab01/report/image/5888892199020644177.jpg)

4. Запуск установщика
Вставьте загрузочный USB или DVD и перезагрузите компьютер. Вы должны увидеть меню установки Rocky Linux. Выберите "Install Rocky Linux" и нажмите Enter.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab01/report/image/5888892199020644178.jpg)

5. Выбор языка и раскладки клавиатуры
На первом экране выберите язык установки и раскладку клавиатуры. Нажмите "Continue".


6. Настройка параметров установки
На следующем экране вы увидите несколько параметров:

Date & Time: Установите правильный часовой пояс.
Keyboard: Проверьте раскладку клавиатуры.
Installation Destination: Выберите диск для установки. Вы можете выбрать автоматическую разметку или настроить ее вручную.
Network & Hostname: Настройте сетевое подключение и задайте имя хоста.
После настройки всех параметров нажмите "Begin Installation".

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab01/report/image/5888892199020644179.jpg)

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab01/report/image/5888892199020644180.jpg)

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab01/report/image/5888892199020644181.jpg)


7. Установка пользователя и пароля
Во время установки вам будет предложено создать пользователя и задать пароль для администратора (root). Заполните необходимые поля.

8. Завершение установки
После завершения установки вы увидите сообщение об успешной установке. Удалите загрузочный носитель и перезагрузите компьютер.

9. Первоначальная настройка
После перезагрузки войдите в систему, используя созданные учетные данные. Вы можете выполнить дополнительные настройки, такие как установка обновлений и необходимых пакетов.

## Заключение
Установка Rocky Linux — это простой и интуитивно понятный процесс. Следуя вышеописанным шагам, вы сможете успешно установить и настроить Rocky Linux на своем сервере или компьютере. Этот дистрибутив обеспечит вам стабильную и безопасную среду для работы.

