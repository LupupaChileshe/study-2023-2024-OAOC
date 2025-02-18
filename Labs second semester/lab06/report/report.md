---
## Front matter
title: "Отчет по лабораторной работе №6"
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

Получить навыки управления процессами операционной системы.

## Управление заданиями

Здесь приводится описание задания в соответствии с рекомендациями
методического пособия и выданным вариантом.

1. Получите полномочия администратора
su –

2. Введите следующие команды:
sleep 3600 &
dd if=/dev/zero of=/dev/null &
sleep 7200

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-35-32.png)

3. Поскольку вы запустили последнюю команду без & после неё, у вас есть 2 часа,
прежде чем вы снова получите контроль над оболочкой. Введите Ctrl + z , чтобы
остановить процесс.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-35-43.png)

4. Введите
jobs

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-35-52.png)

5. Для продолжения выполнения задания 3 в фоновом режиме введите
bg 3
С помощью команды jobs посмотрите изменения в статусе заданий.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-36-03.png)

6. Для перемещения задания 1 на передний план введите
fg 1

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-36-11.png)

7. Введите Ctrl + c , чтобы отменить задание 1. С помощью команды jobs посмотрите
изменения в статусе заданий.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-36-22.png)

8. Проделайте то же самое для отмены заданий 2 и 3.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-36-41.png)

9. Откройте второй терминал и под учётной записью своего пользователя введите в
нём: dd if=/dev/zero of=/dev/null &

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-37-20.png)

10. Введите exit, чтобы закрыть второй терминал.

11. На другом терминале под учётной записью своего пользователя запустите top Вы
увидите, что задание dd всё ещё запущено. Для выхода из top используйте q .

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-36-57.png)

12. Вновь запустите top и в нём используйте k , чтобы убить задание dd. После этого
выйдите из top.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-37-09.png)

## Управление процессами

1. Получите полномочия администратора
su –
2. Введите следующие команды:
dd if=/dev/zero of=/dev/null &
dd if=/dev/zero of=/dev/null &
dd if=/dev/zero of=/dev/null &

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-37-20.png)

3. Введите
ps aux | grep dd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-37-31.png)

4. Используйте PID одного из процессов dd, чтобы изменить приоритет. Используйте
renice -n 5

![]()

5. Введите
ps fax | grep -B5 dd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab06/report/image/Screenshot from 2025-02-19 01-37-46.png)

6. Найдите PID корневой оболочки, из которой были запущены процессы dd, и
введите
kill -9

![]()

