---
## Front matter
lang: ru-RU
title: Отчет по лабораторной работе №4
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

Получить навыки работы с репозиториями и менеджерами пакетов.

# Выполнение лабораторной работы

## cd /etc/yum.repos.d

- Перейдите в каталог /etc/yum.repos.d и изучите содержание каталога и файлов
  репозиториев:
  cd /etc/yum.repos.d
  ls
  
![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-42-08.png)

## cat название_репозитория.repo

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-42-17.png)

## dnf repolist

- Выведите на экран список репозиториев:
  dnf repolist

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-42-25.png)

## dnf search user

- Выведите на экран список пакетов, в названии или описании которых есть слово
  user:
  dnf search user

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-42-39.png)

## dnf search nmap

- Установите nmap, предварительно изучив информацию по имеющимся пакетам:
  dnf search nmap

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-42-50.png)
  
## dnf info nmap

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-42-57.png)

## dnf install nmap

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-43-08.png)

## dnf install nmap\*

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-43-21.png)


## dnf remove nmap

Удалите nmap:
dnf remove nmap

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-43-31.png)

## dnf remove nmap\*

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-43-41.png)


## dnf groups list

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-43-51.png)

## dnf groups info "RPM Development Tools"

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-44-10.png)

## dnf groupinstall "RPM Development Tools"

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-44-20.png)

## dnf groupremove "RPM Development Tools"

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-44-47.png)

## dnf history

- Посмотрите историю использования команды dnf:
 dnf history

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-45-01.png)

## dnf history undo 6

  
![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/presentation/image/Screenshot from 2025-02-18 19-45-08.png) 
 


