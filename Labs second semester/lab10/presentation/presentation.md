---
## Front matter
lang: ru-RU
title: Отчет по лабораторной работе №10
subtitle: Отчет по лабораторной работе Управление модулями ядра из командной строки
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

Цель данной лабораторной работы заключается в изучении управления модулями
ядра Linux с помощью командной строки. В рамках работы необходимо
ознакомиться с командами для просмотра, загрузки и выгрузки модулей ядра, а
также с обновлением ядра операционной системы.

## lspci -k

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/presentation/image/Screenshot from 2025-02-19 14-30-48.png)

Команда отобразила список всех устройств PCI в системе и соответствующих драйверов
ядра

## lsmod | sort

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/presentation/image/Screenshot from 2025-02-19 14-31-00.png)

Вывод показал список загруженных модулей, отсортированный по алфавиту.

## lsmod | grep ext4

Если модуль не загружен, в выводе ничего не отображается.

# Загрузка и выгрузка модулей

## lsmod | grep ext4`

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/presentation/image/Screenshot from 2025-02-19 14-31-00.png)

## modinfo ext4

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/presentation/image/Screenshot from 2025-02-19 14-31-25.png)

Вывод команды содержит сведения о версии, лицензии, описании модуля и
поддерживаемых устройствах. Обратите внимание, что у данного модуля нет параметров
настройки.

## modprobe -r ext4

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/presentation/image/Screenshot from 2025-02-19 14-31-37.png)

Если модуль используется, система может потребовать повторного выполнения команды
или отказать в выгрузке

# Работа с Bluetooth-модулями

- Проверка, загружен ли модуль bluetooth:
lsmod | grep bluetooth
- Загрузка модуля bluetooth:
modprobe bluetooth
- Просмотр списка модулей, связанных с Bluetooth:
lsmod | grep bluetooth

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/presentation/image/Screenshot from 2025-02-19 14-32-07.png)

## modinfo bluetooth

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/presentation/image/Screenshot from 2025-02-19 14-32-18.png)

В выводе можно увидеть доступные параметры, такие как настройка дебаг-режима или
управление энергопотреблением.


## modprobe -r bluetooth

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/presentation/image/Screenshot from 2025-02-19 14-32-28.png)


#  Обновление ядра системы

Rocky Linux является дистрибутивом, базирующимся на RHEL, поэтому
обновление ядра проходит стабильно.

## uname -r

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/presentation/image/Screenshot from 2025-02-19 14-32-42.png)

## dnf list kernel

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab10/presentation/image/Screenshot from 2025-02-19 14-32-58.png)

## Обновление ядра системы

- Обновление всех существующих пакетов перед обновлением ядра:
dnf upgrade --refresh
- Обновление ядра и системы:
- dnf update kernel
- dnf update
dnf upgrade --refresh
- Перезагрузка системы и выбор нового ядра при загрузке.
- Проверка версии нового ядра:
uname -r
hostnamectl

## Выводы
В ходе лабораторной работы были освоены команды управления модулями ядра:
просмотр, загрузка, выгрузка и получение информации. Также была выполнена
процедура обновления ядра операционной системы. Полученные знания позволяют
администрировать систему на более глубоком уровне и эффективно управлять
модулями ядра.





