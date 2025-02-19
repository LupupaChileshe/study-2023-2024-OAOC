---
## Front matter
title: "Отчет по лабораторной работе №12"
subtitle: "Отчет о настройке сети в Linux"
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

Получить навыки настройки сетевых параметров системы.

##Проверка конфигурации сети
1. Получение полномочий администратора: Для выполнения заданий
используется команда su -, предоставляющая полномочия суперпользователя.
2. Просмотр информации о сетевых подключениях: Команда ip -s link
выводит статистику о сетевых интерфейсах:
- Количество отправленных и полученных пакетов.
- Ошибки передачи и получения данных.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-22-55.png)

__Пояснение:__ Интерфейс enp0s3 активно передаёт и принимает данные. Ошибок
и потерь пакетов нет.

3. Просмотр текущих маршрутов: Команда ip route show показывает таблицу
маршрутизации:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-23-07.png)

__Пояснение:__
default via 10.0.2.2: Основной шлюз для выхода в Интернет.
10.0.2.0/24: Локальная сеть, связанная с интерфейсом enp0s3.

4. Просмотр текущих адресов интерфейсов: Команда ip addr show
отображает IP-адреса и другие параметры:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-23-17.png)

__Пояснение:__ Интерфейс enp0s3 имеет IPv4-адрес 10.0.2.15 с маской /24. Это
динамически назначенный адрес.

5. Проверка подключения к Интернету: Команда ping -c 4 8.8.8.8 отправляет 4
пакета на указанный адрес.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-23-27.png)

Вывод: Подключение к Интернету успешно работает.

6. Добавление дополнительного IP-адреса: Команда ip addr add 10.0.0.10/24
dev enp0s3 добавляет адрес 10.0.0.10 к интерфейсу enp0s3.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-23-35.png)

7. Проверка добавленного адреса: Команда ip addr show подтверждает наличие
нового адреса:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-23-46.png)

8. Сравнение ip и ifconfig: Команда ifconfig также отображает информацию о
сетевых интерфейсах, но вывод менее подробен и не поддерживает
современные возможности, такие как настройка маршрутов.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-23-53.png)

9. Просмотр прослушиваемых портов: Команда ss -tul показывает список
прослушиваемых TCP и UDP портов:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-24-03.png)

# Управление сетевыми подключениями с помощью nmcli

1. Просмотр текущих соединений: Команда nmcli connection show отображает
активные соединения:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-24-13.png)

2. Добавление соединения DHCP: Команда:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-24-21.png)

3. Добавление статического соединения: Команда:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-24-31.png)

4. Переключение на статическое соединение: Команда nmcli connection up
"static" активирует статическое соединение. Проверка:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-24-42.png)

5. Переключение на DHCP: Команда nmcli connection up "dhcp" возвращает
DHCP.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-24-52.png)

# Изменение параметров соединения с помощью nmcli

1. __Отключение автоподключения:__ Команда nmcli connection modify "static"
connection.autoconnect no.
2. __Добавление DNS-сервера:__ Команда nmcli connection modify "static" ipv4.dns
10.0.0.10.
3. __Добавление второго DNS-сервера:__ Команда nmcli connection modify "static"
+ipv4.dns 8.8.8.8.
4. __Изменение IP-адреса:__ Команда nmcli connection modify "static" ipv4.addresses
10.0.0.20/24.
5. __Добавление другого IP-адреса:__ Команда nmcli connection modify "static"
+ipv4.addresses 10.20.30.40/16.
6. __Активация соединения:__ Команда nmcli connection up "static" активирует
соединение. Проверка:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-25-04.png)

7. Настройки через nmtui: Интерфейс nmtui предоставляет графический
способ управления настройками сети. Описание:
- Устройство enp0s3 с несколькими IP-адресами.
- Статические DNS-серверы указаны.

8. Настройки в графическом интерфейсе: Через GUI подтверждается
наличие статического адреса и добавленных DNS-серверов.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab12/report/image/Screenshot from 2025-02-19 17-25-24.png)

9. Возврат к DHCP: Команда nmcli connection up "dhcp" переключает обратно
на DHCP.

Вывод
Проведены настройки сети согласно заданию. Основные действия включают
просмотр текущего состояния интерфейсов, добавление IP-адресов и
управление соединениями через nmcli. Проверка показала успешность
выполнения операций.

























