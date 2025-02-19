---
## Front matter
lang: ru-RU
title: Отчет по лабораторной работе №13
subtitle: Отчет о выполнении лабораторной работы по управлению брандмауэром с помощью firewall-cmd
author:
  - Чилеше . Л
institute:
  - Российский университет дружбы народов, Москва, Россия
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

Получить навыки настройки пакетного фильтра в Linux.
Целью этой лабораторной работы было понять и попрактиковаться в управлении
брандмауэром Linux с помощью утилиты firewall-cmd. Это включало проверку
конфигураций, изменение правил и понимание различий между динамическими и
постоянными конфигурациями.


## firewall-cmd --get-default-zone

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/presentation/image/Screenshot from 2025-02-19 18-42-06.png)

## firewall-cmd --get-zones

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/presentation/image/Screenshot from 2025-02-19 18-42-28.png)

## firewall-cmd --list-services

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/presentation/image/Screenshot from 2025-02-19 18-42-45.png)


## firewall-cmd --list-all

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/presentation/image/Screenshot from 2025-02-19 18-43-00.png)

# Добавление службы VNC-сервера:


## firewall-cmd --add-service=vnc-server

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/presentation/image/Screenshot from 2025-02-19 18-43-19.png)

## firewall-cmd --list-all`

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/presentation/image/Screenshot from 2025-02-19 18-43-29.png)

## Перезапускаем firewalld:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/presentation/image/Screenshot from 2025-02-19 18-43-40.png)



## Вывод

Заключение Лабораторная работа позволила получить практический опыт работы с
firewall-cmd и лучше понять правила управления брандмауэром в системе Linux. Различие
между конфигурациями во время выполнения и постоянными конфигурациями и их
соответствующими вариантами использования является фундаментальной концепцией,
обеспечивающей эффективное управление брандмауэром.
В этой лабораторной работе было продемонстрировано, как настроить брандмауэр с
помощью графического интерфейса firewall-config. Благодаря включению определенных
служб, добавлению портов и внесению изменений сетевая безопасность системы была
адаптирована к конкретным требованиям. Различие между конфигурациями во время
выполнения и постоянными конфигурациями обеспечивает гибкость и контроль над
настройками брандмауэра.


