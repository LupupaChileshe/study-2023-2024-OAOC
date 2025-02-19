---
## Front matter
lang: ru-RU
title: Отчет по лабораторной работе №12
subtitle: Отчет о настройке сети в Linux
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

Получить навыки настройки сетевых параметров системы.

## ip -s link

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-22-55.png)

__Пояснение:__ Интерфейс enp0s3 активно передаёт и принимает данные. Ошибок
и потерь пакетов нет.

## ip route show 

__Пояснение:__
default via 10.0.2.2: Основной шлюз для выхода в Интернет.
10.0.2.0/24: Локальная сеть, связанная с интерфейсом enp0s3.

## ip addr show

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-23-07.png)

__Пояснение:__ Интерфейс enp0s3 имеет IPv4-адрес 10.0.2.15 с маской /24. Это
динамически назначенный адрес.



## ping -c 4 8.8.8.8

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-23-17.png)

__Вывод:__ Подключение к Интернету успешно работает.

## p addr add 10.0.0.10/24 dev enp0s3

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-23-27.png)

## ip addr show

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-23-35.png)

## ifconfig

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-23-46.png)

## ss -tul

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-23-53.png)

# РУправление сетевыми подключениями с помощью nmcli

## nmcli connection

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-24-03.png)


## Добавление соединения DHCP

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-24-13.png)


## . Добавление статического соединения:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-24-21.png)

## nmcli connection up

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-24-31.png)

## nmcli connection up

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-24-42.png)

# Изменение параметров соединения с помощью nmcli

## Отключение автоподключения:
 Команда nmcli connection modify "static"
connection.autoconnect no.

## Добавление DNS-сервера: 
Команда nmcli connection modify "static" ipv4.dns
10.0.0.10.

## Добавление второго DNS-сервера: 
Команда nmcli connection modify "static"
+ipv4.dns 8.8.8.8.

## Изменение IP-адреса: 
Команда nmcli connection modify "static" ipv4.addresses
10.0.0.20/24.

## Добавление другого IP-адреса: 
Команда nmcli connection modify "static"
+ipv4.addresses 10.20.30.40/16.

## Активация соединения: 
Команда nmcli connection up "static" активирует
соединение. Проверка:
![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/presentation/image/Screenshot from 2025-02-19 17-24-52.png)

## Вывод

Проведены настройки сети согласно заданию. Основные действия включают
просмотр текущего состояния интерфейсов, добавление IP-адресов и
управление соединениями через nmcli. Проверка показала успешность
выполнения операций.



