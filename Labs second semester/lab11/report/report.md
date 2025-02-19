---
## Front matter
title: "Отчет по лабораторной работе №11"
subtitle: "Отчет о настройке GRUB2 и процедурах восстановления системы"
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

## Цель работы

Получить навыки работы с загрузчиком системы GRUB2.

## Введение

В этом отчете описаны шаги, необходимые для управления конфигурациями
загрузчика GRUB2, диагностики системных проблем, а также восстановления или
сброса пароля root в дистрибутивах Linux на основе Red Hat. Эти задачи необходимы
системным администраторам для обеспечения стабильности системы, устранения
ошибок и восстановления доступа, когда учетные данные недоступны.

## Конфигурация GRUB2

Загрузчик GRUB2 играет решающую роль в управлении процессом загрузки в Linux.
Настройка его параметров позволяет оптимизировать и эффективный запуск
системы.

1. Изменение тайм-аута GRUB:
- Тайм-аут по умолчанию для отображения меню GRUB можно настроить в
файле /etc/default/grub, установив для параметра GRUB_TIMEOUT желаемое
значение (например, 10 секунд).
- Изменения применяются с помощью команды:
grub2-mkconfig -o /boot/grub2/grub.cfg
- Это гарантирует, что у пользователей будет достаточно времени для
выбора параметров загрузки во время запуска.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab11/report/image/Screenshot from 2025-02-19 16-41-47.png)

2. Отображение загрузочных сообщений:

- Удалив параметры rhgb (графическая загрузка Red Hat) и quiet из строки
GRUB_CMDLINE_LINUX в файле конфигурации GRUB, можно включить
подробные загрузочные сообщения. Это полезно для диагностики проблем
во время процесса загрузки.

# Процедуры восстановления системы

Режимы восстановления системы, такие как режим восстановления и аварийный
режим, жизненно важны для устранения сбоев загрузки и других критических
проблем.

1. Rescue Mode:
- Режим восстановления — это минимально функциональная среда,
позволяющая администраторам диагностировать и устранять проблемы.
- Доступ включается путем редактирования записи GRUB во время загрузки,
добавления systemd.unit=rescue.target к строке ядра и нажатия Ctrl + X для
продолжения загрузки.
- Такие команды, как systemctl list-units и systemctl show-environment,
предоставляют информацию о загруженных сервисах и переменных среды.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab11/report/image/Screenshot from 2025-02-19 16-42-06.png)

2. Emergency Mode:
- Этот режим предоставляет минимальную оболочку, в которую загружаются
только самые основные системные ресурсы. Он используется, когда
проблемы не позволяют системе загрузиться в режиме восстановления.
- Как и в режиме восстановления, доступ включается добавлением
systemd.unit=emergency.target к строке ядра.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab11/report/image/Screenshot from 2025-02-19 16-42-19.png)

# Сброс пароля root

Распространенным сценарием системного администрирования является потеря
пароля root. Следующие шаги описывают процедуру его сброса:
1. Доступ к Initramfs:
- При добавлении rd.break к строке ядра в GRUB и загрузке система
  останавливается на этапе initramfs перед монтированием корневой
- файловой системы.
2. Перемонтирование файловой системы для доступа на чтение/запись:
Корневая файловая система перемонтируется для доступа на запись с помощью:
mount -o remount,rw /sysroot
chroot /sysroot
3. Установка нового пароля:
- Команда passwd используется для назначения нового пароля пользователю
  root.
4. Восстановление контекста SELinux:
Поскольку на этом этапе политики SELinux не загружаются, контекст теневого
файла необходимо исправить вручную:
load_policy -i
chcon -t shadow_t /etc/shadow
![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab11/report/image/Screenshot from 2025-02-19 16-42-32.png)

5. Перезагрузка системы:
Система перезагружается с помощью команды restart -f, гарантируя, что
изменения будут применены.


# Заключение

Понимание и управление конфигурациями GRUB2, использование режимов
восстановления и сброс пароля root являются критически важными навыками
для поддержания доступности и безопасности системы. Эти знания позволяют
администраторам эффективно реагировать на чрезвычайные ситуации, сводя к
минимуму время простоя и обеспечивая надежность системы.
Этот отчет служит справочником по систематическому выполнению этих задач,
подчеркивая важность тщательного выполнения для предотвращения
дальнейших осложнений.




