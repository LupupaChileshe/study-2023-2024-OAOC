---
## Front matter
lang: ru-RU
title: Отчет по лабораторной работе №7
subtitle: Простейший шаблон
author:
  - Чилеше . Л
institute:
  - Российский университет дружбы народов, Москва, Россия
  - Объединённый институт ядерных исследований, Дубна, Россия
date: 27 января 2003

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
---

# Информация

## Докладчик

:::::::::::::: {.columns align=center}
::: {.column width="70%"}

  * Лупупа Чилеше
  * Студент
  * Студент Группы НПИбд-03-23
  * Российский университет дружбы народов
:::
::: {.column width="30%"}



:::
::::::::::::::

# Вводная часть

## Цель работы

Получение навыков работы с планировщиками событий cron и at.

# Выполнение лабораторной работы 

## systemctl status crond -l

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-14-42.png)

## cat /etc/crontab

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-14-50.png)

## crontab -l

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-14-59.png)

## */1 * * * * logger This message is written from root cron

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-15-08.png)

## crontab -l

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-15-18.png)

## grep written /var/log/messages

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-15-36.png)

## 0 */1 * * 1-5 logger This message is written from root cron

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-15-08.png)

## crontab -l

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-15-45.png)

## cd /etc/cron.hourly

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-16-03.png)

## logger This message is written at $(date)

Откройте файл eachhour для редактирования и пропишите в нём следующий
 скрипт (запись сообщения в системный журнал):
 #!/bin/sh
 logger This message is written at $(date)

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-16-10.png)

## chmod +x eachhour

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-16-19.png)

## 11 * * * * root logger This message is written from /etc/cron.d

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-16-28.png)

## grep written /var/log/messages

Не выключая систему, через некоторое время (2–3 часа) просмотрите журнал
системных событий: grep written /var/log/messages По журналу определите, был ли
осуществлён запуск сценария eachhour в соответствии с заданным расписанием.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab08/presentation/image/Screenshot from 2025-02-19 12-16-38.png)

# Планирование заданий с помощью at

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



