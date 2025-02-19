---
## Front matter
title: "Отчет по лабораторной работе №7"
subtitle: "Отчет о мониторинге и настройке системных журналов"
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

Основными задачами этой лаборатории были:
Отслеживайте журналы системных событий в режиме реального времени.
Настройте rsyslog для регистрации ошибок веб-сервера.
Используйте журналctl для эффективного мониторинга журналов.
Включите постоянное хранилище для журналов Journald.

## Мониторинг системных журналов в режиме

1. Запустил три терминальные сессии.
Получил root-права на каждом терминале с помощью su.
Во втором терминале инициирован мониторинг в реальном времени с помощью:
tail -f /var/log/messages

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-22-03.png)

2. Проверено сообщение журнала событий «FAILED SU (to root)», появляющееся
в контролируемом терминале.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-22-21.png)

3. Зарегистрировал пользовательское сообщение, используя:
logger hello

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-22-29.png)

## Настройка rsyslog для ведения журнала веб-сервера

1. Установленный веб-сервер Apache:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-22-48.png)
 
2. Запустил и включил службу:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-22-56.png)

3. Проверенные журналы ошибок с:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-23-04.png)

4. Создал собственный файл конфигурации rsyslog /etc/rsyslog.d/httpd.conf: local1.* -/var/log/httpd-error.log

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-23-17.png)

5. Перезапустил rsyslog и Apache:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-23-26.png)

## Ведение журнала отладки

1. Создал и настроил файл журнала отладки /etc/rsyslog.d/debug.conf:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-23-34.png)

2. Verified debug log monitoring: tail -f /var/log/messages-debug

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-23-44.png)

3. Протестировано с: logger -p daemon.debug "Daemon Debug Message"

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-23-52.png)

## Мониторинг с помощью Journalctl

1. Просмотрел полные логи: Journalctl

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/report/image/Screenshot from 2025-02-19 11-24-11.png)

2. Мониторинг журналов в режиме реального времени: journalctl -f


## Результаты и наблюдения

Успешно отслеживал системные события и входы пользователей в режиме
реального времени.
Настроен rsyslog для регистрации ошибок веб-сервера Apache.
Проверено правильность хранения отладочных и пользовательских сообщений
журнала.
Включено и протестировано постоянное ведение журналов.


## Заключение

В ходе этой лабораторной работы был предоставлен практический опыт
мониторинга системных журналов, настройки пользовательских правил ведения
журналов и эффективного управления системными журналами с помощью Journald
и rsyslog. Овладение этими методами необходимо для эффективного системного
администрирования и устранения неполадок.

















