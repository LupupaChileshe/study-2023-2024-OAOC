---
## Front matter
title: "Отчет по лабораторной работе №9"
subtitle: "Отчет о мониторинге и настройке системных журналов"
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

Цель данной лабораторной работы – изучение основ управления режимами SELinux,
восстановления контекста безопасности файлов, настройки нестандартного
расположения файлов веб-сервера и работы с переключателями SELinux. В ходе
выполнения работы студенты научатся изменять режимы работы SELinux,
корректировать контексты безопасности с помощью restorecon, настраивать SELinux
для работы веб-сервера и управлять SELinux-переключателями.


# Выполнение лабораторной работы

## Управление режимами SELinux
1. Запуск терминала и получение прав администратора
   Выполнена команда su.

2. Просмотр состояния SELinux
   Команда sestatus -v вывела информацию:
  
![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-06-35.png)  
   
- SELinux status: показывает, включена ли SELinux.
- Current mode: текущий режим (Enforcing, Permissive, Disabled).
- Policy version: используемая политика безопасности.
- Loaded policy: загруженный набор правил безопасности.
- Mode from config file: режим, установленный в конфигурации

3. Определение текущего режима работы
   Команда getenforce показала Enforcing (принудительный режим).

4. Изменение режима на Permissive

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-06-54.png)

setenforce 0 изменил режим на Permissive.
getenforce подтвердил изменение.

5. Отключение SELinux через конфигурационный файл

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-07-03.png)

В файле /etc/sysconfig/selinux установлено SELINUX=disabled.
После перезагрузки система подтвердила отключение (getenforce вернул Disabled).

6. Попытка включения SELinux без перезагрузки

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-07-22.png)

 setenforce 1 не сработал, так как отключенный SELinux требует перезагрузки.

7. Возвращение режима Enforcing

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-07-34.png)

В файле /etc/sysconfig/selinux установлено SELINUX=enforcing.
После перезагрузки система запустилась в режиме Enforcing, возможно с
предупреждением о необходимости восстановления меток.


# Использование restorecon для восстановления контекста безопасности

1. Просмотр контекста файла /etc/hosts

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-07-49.png)

ls -Z /etc/hosts показал net_conf_t.

2. Копирование файла и изменение контекста

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-07-57.png)

cp /etc/hosts ~/ создал копию с контекстом admin_home_t.

3. Перемещение файла обратно и проверка контекста

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-08-05.png)

mv ~/hosts /etc сохранило admin_home_t.

4. Исправление контекста

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-08-14.png)

restorecon -v /etc/hosts восстановил net_conf_t.

5. Массовое исправление контекста

touch /.autorelabel и перезагрузка инициировали перемаркировку файловой системы

# Настройка контекста для нестандартного расположения веб-файлов

1. Установка Apache и текстового браузера 

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-08-32.png)

  dnf -y install httpd lynx.

2. Создание каталога и конфигурация Apache

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-08-43.png)

   mkdir /web, добавлен index.html.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-08-50.png)

  В /etc/httpd/conf/httpd.conf изменен DocumentRoot на /web.

3. Запуск Apache и тестирование через lynx

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-09-01.png)

  systemctl start httpd, но страница по умолчанию не отображала новый контент.

4. Изменение контекста безопасности

  semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?".
  restorecon -R -v /web восстановил контекст.

5.Повторное тестирование через lynx

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-09-20.png)

  После перезагрузки веб-страница Welcome to my web-server отобразилась успешно.
 
# Работа с переключателями SELinux

1. Просмотр переключателей для FTP

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-09-31.png)

 getsebool -a | grep ftp показал ftpd_anon_write off.

2. Просмотр переключателей с пояснениями

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/report/image/Screenshot from 2025-02-19 13-09-42.png)

  semanage boolean -l | grep ftpd_anon подтвердил временное изменение.

3. Установка постоянного значения
    setsebool -P ftpd_anon_write on сохранил изменение после перезагрузки.
4. Проверка состояния после перезагрузки
    semanage boolean -l | grep ftpd_anon подтвердил on для ftpd_anon_write.





