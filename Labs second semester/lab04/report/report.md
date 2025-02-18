---
## Front matter
title: "Шаблон отчёта по лабораторной работе"
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
	- babelshorthands=
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

Получить навыки работы с репозиториями и менеджерами пакетов.


# Выполнение лабораторной работы

1. В консоли перейдите в режим работы суперпользователя (используйте команду su-).
Перейдите в каталог /etc/yum.repos.d и изучите содержание каталога и файлов
репозиториев:
cd /etc/yum.repos.d
ls

![cd /etc/yum.repos.d](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-42-08.png){#fig:001 width=70%}

2. cat название_репозитория.repo

![cat](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-42-17.png){#fig:001 width=70%}

3. Выведите на экран список репозиториев:
dnf repolist
и поясните полученную информацию.

![Название рисунка](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-42-25.png){#fig:001 width=70%}

4. Выведите на экран список пакетов, в названии или описании которых есть слово
user:
dnf search user
и поясните полученную информацию

![dnf search user](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-42-39.png){#fig:001 width=70%}

5. Установите nmap, предварительно изучив информацию по имеющимся пакетам:
dnf search nmap

![dnf search nmap](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-42-50.png){#fig:001 width=70%}

6. dnf info nmap

![ dnf info nmap](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-42-57.png){#fig:001 width=70%}

7. dnf install nmap

![dnf install nmap](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-43-08.png){#fig:001 width=70%}

8. dnf install nmap\*

![dnf install nmap\*](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-43-21.png){#fig:001 width=70%}

9. Удалите nmap:
dnf remove nmap

![dnf remove nmap](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-43-31.png){#fig:001 width=70%}

10. dnf remove nmap\*

![dnf remove nmap\*](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-43-41.png){#fig:001 width=70%}

11. Получите список имеющихся групп пакетов, затем установите группу пакетов RPM
Development Tools:
dnf groups list

![dnf groups list](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-43-51.png){#fig:001 width=70%}

LANG=C dnf groups list
dnf groups info "RPM Development Tools"

12. dnf groupinstall "RPM Development Tools"

![dnf groupinstall](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-44-10.png){#fig:001 width=70%}

13. Для удаления группы пакетов RPM Development Tools можно воспользоваться
командой
dnf groupremove "RPM Development Tools"

![dnf groupremove](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-44-20.png){#fig:001 width=70%}

14. 
Посмотрите историю использования команды dnf:
dnf history

![dnf history](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-45-01.png){#fig:001 width=70%}

15. и отмените последнее, например шестое по счёту, действие:
dnf history undo 6

![dnf history undo 6](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-45-08.png){#fig:001 width=70%}

## Предположим, что требуется установить текстовый браузер lynx из rpm-пакета.

1. Скачайте rpm-пакет lynx:
dnf list lynx
dnf install lynx --downloadonly

![dnf list lynx](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-45-19.png){#fig:001 width=70%}


2. Найдите каталог, в который был помещён пакет после загрузки:
find /var/cache/dnf/ -name lynx*

![find ](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-45-28.png){#fig:001 width=70%}

3. Перейдите в этот каталог и затем установите rpm-пакет:
rpm -Uhv lynx-.rpm

![rpm](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-45-37.png){#fig:001 width=70%}

4. Определите расположение исполняемого файла:
which lynx

![which lynx](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-45-44.png){#fig:001 width=70%}

5. Используя rpm, определите по имени файла, к какому пакету принадлежит lynx:
rpm -qf $(which lynx)
и получите дополнительную информацию о содержимом пакета, введя:
rpm -qi lynx

![rpm -qi lynx](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-45-53.png){#fig:001 width=70%}

6. Получите список всех файлов в пакете, используя:
rpm -ql lynx

![rpm -ql lynx](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 20-01-00.png){#fig:001 width=70%}

7. Выведите на экран перечень и месторасположение конфигурационных файлов
пакета:
rpm -qc lynx

![rpm -qc lynx](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-46-42.png){#fig:001 width=70%}


8. Выведите на экран расположение и содержание скриптов, выполняемых при
установке пакета:
rpm -q --scripts lynx

![rpm -q --scripts lynx](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-46-50.png){#fig:001 width=70%}

9. В отдельном терминале под своей учётной записью запустите текстовый браузер
lynx, чтобы проверить корректность установки пакета.
10. Вернитесь в терминал с учётной записью root и удалите пакет:rpm -e lynx
ls

![rpm -e lynx ls](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-47-02.png){#fig:001 width=70%}

## Предположим, что требуется из rpm-пакетов установить dnsmasq (DNS-, DHCP- и TFTPсервер).

1. Установите пакет dnsmasq:
dnf list dnsmasq
dnf install dnsmasq
![dnf list dnsmasq](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-47-09.png){#fig:001 width=70%}

и определите расположение исполняемого файла:
which dnsmasq

![which dnsmasq](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-47-17.png){#fig:001 width=70%}

2. Определите по имени файла, к какому пакету принадлежит dnsmasq:
rpm -qf $(which dnsmasq)

![rpm -qf](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-47-24.png){#fig:001 width=70%}

и получите дополнительную информацию о содержимом пакета:
rpm -qi dnsmasq

![rpm -qi dnsmasq](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 19-47-24.png){#fig:001 width=70%}

3. Получите список всех файлов в пакете:
rpm -ql dnsmasq
а также выведите перечень файлов с документацией пакета:
rpm -qd dnsmasq

![rpm -qd dnsmasq](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab04/report/image/Screenshot from 2025-02-18 20-01-00.png){#fig:001 width=70%}








