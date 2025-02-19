---
## Front matter
title: "Отчет по лабораторной работе №8"
subtitle: "Простейший вариант"
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

Получение навыков работы с планировщиками событий cron и at.

## Выполнение лабораторной работы

1. Запустите терминал и получите полномочия администратора:
su –

2. Посмотрите статус демона crond:
systemctl status crond -

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-14-42.png)

3. Посмотрите содержимое файла конфигурации
/etc/crontab:
cat /etc/crontab

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-14-50.png)

4. Посмотрите список заданий в расписании:
crontab -l

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-14-59.png)

5. Откройте файл расписания на редактирование:
crontab -e
Команда запустит интерфейс редактора (по умолчанию используется vi). Добавьте
следующую строку в файл расписания (запись сообщения в системный журнал),
используя Ins для перехода в vi в режим ввода:
*/1 * * * * logger This message is written from root cron

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-15-08.png)

6. Посмотрите список заданий в расписании:
crontab -l

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-15-18.png)

7. Не выключая систему, через некоторое время (2–3 минуты) просмотрите журнал
системных событий:
grep written /var/log/messages

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-15-36.png)

8. Измените запись в расписании crontab на следующую:
0 */1 * * 1-5 logger This message is written from root cron

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-15-26.png)

9. Посмотрите список заданий в расписании:
crontab -l

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-15-54.png)

10. Перейдите в каталог /etc/cron.hourly и создайте в нём файл сценария с именем
eachhour:
cd /etc/cron.hourly
touch eachhour

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-16-03.png)

11. Откройте файл eachhour для редактирования и пропишите в нём следующий
 скрипт (запись сообщения в системный журнал):
 #!/bin/sh
 logger This message is written at $(date)

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-16-10.png)

12. Сделайте файл сценария eachhour исполняемым:
chmod +x eachhour

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-16-19.png)

13. Теперь перейдите в каталог /etc/crond.d и создайте в нём файл с расписанием
eachhour:
cd /etc/cron.d touch eachhour
Откройте этот файл для редактирования и поместите в него следующее
содержимое:
11 * * * * root logger This message is written from /etc/cron.d

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-16-28.png)

14. Не выключая систему, через некоторое время (2–3 часа) просмотрите журнал
системных событий: grep written /var/log/messages По журналу определите, был ли
осуществлён запуск сценария eachhour в соответствии с заданным расписанием.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/report/image/Screenshot from 2025-02-19 12-16-38.png)

## Теоретическое введение

1. Запустите терминал и получите полномочия администратора:
su –
2. Проверьте, что служба atd загружена и включена:
systemctl status atd
3. Задайте выполнение команды logger message from at в 9:30 (или замените на
любое другое время, когда вы работаете над этим упражнением). Для этого введите
at 9:30 Затем введите
logger message from at
Используйте Ctrl + d , чтобы закрыть оболочку.
4. Убедитесь, что задание действительно запланировано:
atq
С помощью команды grep 'from at' /var/log/messages посмотрите, появилось ли
соответствующее сообщение в лог-файле в указанное вами время.


