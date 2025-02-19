---
## Front matter
lang: ru-RU
title: Отчет по лабораторной работе №6
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

Получить навыки управления процессами операционной системы.

## dd if=/dev/zero of=/dev/null &

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/presentation/image/Screenshot from 2025-02-19 01-35-32.png)

## jobs


![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/presentation/image/Screenshot from 2025-02-19 01-35-52.png)

## bg 3

Для продолжения выполнения задания 3 в фоновом режиме введите
bg 3
С помощью команды jobs посмотрите изменения в статусе заданий.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/presentation/image/Screenshot from 2025-02-19 01-36-03.png)

## fg 1

Для перемещения задания 1 на передний план введите
fg 1

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/presentation/image/Screenshot from 2025-02-19 01-36-11.png)

## top

На другом терминале под учётной записью своего пользователя запустите top Вы
увидите, что задание dd всё ещё запущено. Для выхода из top используйте q .

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/presentation/image/Screenshot from 2025-02-19 01-36-57.png)

## top,k

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/presentation/image/Screenshot from 2025-02-19 01-37-09.png)

# Управление процессами

## dd if=/dev/zero of=/dev/null &

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/presentation/image/Screenshot from 2025-02-19 01-37-20.png)


## ps aux | grep dd

Это показывает все строки, в которых есть буквы dd. Запущенные процессы dd идут
последними.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/presentation/image/Screenshot from 2025-02-19 01-37-31.png)

## ps fax | grep -B5 dd

Параметр -B5 показывает соответствующие запросу строки, включая пять строк до
этого. Поскольку ps fax показывает иерархию отношений между процессами, вы
также увидите оболочку, из которой были запущены все процессы dd, и её PID

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/presentation/image/Screenshot from 2025-02-19 01-37-46.png)

## kill -9

Найдите PID корневой оболочки, из которой были запущены процессы dd, и
введите
kill -9
(заменив на значение PID оболочки). Вы увидите, что ваша корневая оболочка
закрылась, а вместе с ней и все процессы dd. Остановка родительского процесса —
простой и удобный способ остановить все его дочерние процессы.


