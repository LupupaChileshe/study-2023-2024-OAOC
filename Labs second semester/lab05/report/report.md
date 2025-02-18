---
## Front matter
title: "Отчет по лабораторной работе №5"
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

Получить навыки управления системными службами операционной системы
посредством systemd.

1. Получите полномочия администратора
su –
2. Проверьте статус службы Very Secure FTP:
systemctl status vsftpd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-36-20.png)

3. Установите службу Very Secure FTP:
dnf -y install vsftpd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-36-32.png)

4. Запустите службу Very Scure FTP:
systemctl start vsftpd e

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-36-42.png)

5. Проверьте статус службы Very Secure FTP:
systemctl status vsftpd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-37-36.png)

6. Добавьте службу Very Secure FTP в автозапуск при загрузке операционной
системы, используя команду systemctl enable. Затем проверьте статус службы.
Удалите службу из автозапуска, используя команду systemctl disable, и снова
проверьте её статус.

7. Выведите на экран символические ссылки, ответственные за запуск различных
сервисов:
ls /etc/systemd/system/multi-user.target.wants

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-37-13.png)

8. Снова добавьте службу Very Secure FTP в автозапуск:
systemctl enable vsftpd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-36-53.png)

9. Снова проверьте статус службы Very Secure FTP:
systemctl status vsftpd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-37-36.png)

10. Выведите на экран список зависимостей юнита:
systemctl list-dependencies vsftpd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-37-47.png)

11. Выведите на экран список юнитов, которые зависят от данного юнита:
systemctl list-dependencies vsftpd –reverse

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-37-57.png)

# Конфликты юнитов

1. Получите полномочия администратора. Установите iptables:
dnf -y install iptables\*

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-38-12.png)

2. Проверьте статус firewalld и iptables:
systemctl status firewalld

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-38-23.png)

3. Попробуйте запустить firewalld и iptables:
systemctl start firewalld
systemctl start iptables

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-38-34.png)

4. Введите
cat /usr/lib/systemd/system/firewalld.service

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-38-43.png)

5. Введите
cat /usr/lib/systemd/system/iptables.service

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-38-53.png)

6. Выгрузите службу iptables (на всякий случай, чтобы убедиться, что данная служба
не загружена в систему):
systemctl stop iptables
и загрузите службу firewalld
systemctl start firewalld

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-39-01.png)

7. Заблокируйте запуск iptables, введя:
systemctl mask iptables

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-39-12.png)

8. Попробуйте запустить iptables:
systemctl start iptables

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-39-21.png)

9. Попробуйте добавить iptables в автозапуск:
systemctl enable iptables


![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/report/image/Screenshot from 2025-02-19 00-39-21.png)



