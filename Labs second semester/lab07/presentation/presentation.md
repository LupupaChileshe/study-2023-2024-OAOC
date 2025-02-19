---
## Front matter
lang: ru-RU
title: Отчет по лабораторной работе №7
subtitle: Отчет о мониторинге и настройке системных журналов
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

## Цель работ

Основными задачами этой лаборатории были:
Отслеживайте журналы системных событий в режиме реального времени.
Настройте rsyslog для регистрации ошибок веб-сервера.
Используйте журналctl для эффективного мониторинга журналов.
Включите постоянное хранилище для журналов Journald.

# Мониторинг системных журналов в режиме реального времени


## tail -f /var/log/messages

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-22-03.png)

## FAILED SU (to root)

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-22-21.png)

## logger hello

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-22-29.png)

# Настройка rsyslog для ведения журнала веб-сервера

## веб-сервер Apache:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-22-48.png)

## Запустил и включил службу:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-22-56.png)

## Проверенные журналы ошибок с:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-23-04.png)

## local1.* -/var/log/httpd-error.log

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-23-17.png)

## Перезапустил rsyslog и Apache:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-23-26.png)

#Ведение журнала отладки

## /etc/rsyslog.d/debug.conf

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-23-34.png)

## systemctl restart rsyslog.service

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-23-26.png)

## tail -f /var/log/messages-debug

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-23-44.png)

## logger -p daemon.debug "Daemon Debug Message"

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-23-52.png)

## Journalctl

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab07/presentation/image/Screenshot from 2025-02-19 11-24-11.png)

# Результаты и наблюдения

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


