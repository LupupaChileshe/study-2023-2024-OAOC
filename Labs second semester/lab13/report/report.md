---
## Front matter
title: "Отчет по лабораторной работе №13"
subtitle: "Отчет о выполнении лабораторной работы по управлению брандмауэром с помощью firewall-cmd"
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

Получить навыки настройки пакетного фильтра в Linux.
Целью этой лабораторной работы было понять и попрактиковаться в управлении
брандмауэром Linux с помощью утилиты firewall-cmd. Это включало проверку
конфигураций, изменение правил и понимание различий между динамическими и
постоянными конфигурациями.

# Управление брандмауэром с помощью firewall-cmd

__Получение административных привилегий:__
- Command: su –
- Успешно переключился на пользователя root. Этот шаг обеспечил нам наличие
  необходимых разрешений для управления брандмауэром.
__Определение зоны по умолчанию:__
 Команда: firewall-cmd --get-default-zone
- Вывод: была отображена зона по умолчанию (например, «публичная»).
- На этом этапе проверялась зона, которую система использует для неуправляемых
 подключений.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-44-39.png)

__Список доступных зон:__

- Команда: firewall-cmd --get-zones
- Вывод: был отображен список зон (например, «блокировать dmz, удалить внешний
  дом, внутреннюю общедоступную доверенную работу»)
- Подтверждены зоны, доступные для настройки сетевых интерфейсов

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-44-30.png)

__Просмотр доступных услуг:__

- Команда: firewall-cmd --get-services
- Вывод: отобразился список предопределенных служб, которыми можно управлять
  с помощью брандмауэра.
- Это было важно для понимания спектра сервисов, поддерживаемых firewalld.

__Листинговые услуги в текущей зоне:__

- Команда: firewall-cmd --list-services
- Вывод: список активных служб в текущей зоне по умолчанию.
- Проверено, какие службы уже разрешены через брандмауэр.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-44-22.png)

__Сравнение результатов команд --list-all:__

- Команды: firewall-cmd --list-all и firewall-cmd --list-all --zone=public
- Вывод: обе команды отображали аналогичную информацию, показывая активные
  службы, порты и интерфейсы для «общедоступной» зоны.
- Это продемонстрировало, как просмотреть подробные сведения о конфигурациях
  брандмауэра для конкретных зон.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-44-10.png)

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-43-57.png)

__Добавление службы VNC-сервера:__

- Команда: firewall-cmd --add-service=vnc-server
- Команда выполнена успешно. Служба vnc-сервера была добавлена в
  конфигурацию среды выполнения.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-43-48.png)

__Проверка добавления VNC-сервера:__
- Команда: firewall-cmd --list-all
- Вывод: подтверждено, что служба vnc-сервера указана в списке активных
  служб.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-43-40.png)

__Перезапускаем firewalld:__

- Команда: systemctl перезапустить firewalld
- Служба firewalld успешно перезапущена.
- Команда: firewall-cmd --list-all
- Вывод: служба vnc-сервера больше не отображается.
 
- Объяснение: Это произошло потому, что в конфигурацию среды выполнения было
  внесено предыдущее дополнение, которое сбрасывается при перезапуске службы.
 
 ![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-43-29.png)
 
__Перезагрузка конфигурации firewalld:__
- Команды: firewall-cmd --reload и firewall-cmd --list-all
- Вывод: После перезагрузки в рантайм-конфигурации появился сервис vnc-сервера.
- Этот шаг подчеркнул необходимость перезагрузки firewalld, чтобы постоянные
  изменения вступили в силу. 

__Добавление TCP-порта 2022 в постоянную конфигурацию:__

- Команда: firewall-cmd --add-port=2022/tcp --permanent
- Порт успешно добавлен в постоянную конфигурацию. 

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-43-19.png)
- Это подтвердило, что порт был правильно добавлен и активен как во время
  выполнения, так и в постоянной конфигурации. 
 
# Управление брандмауэром с помощью firewall-config

__Запускаем конфигурацию брандмауэра__

__Команда:__ firewall-config

__Объяснение:__ Команда firewall-config запускает графический интерфейс
пользователя (GUI) для управления брандмауэром. Этот интерфейс упрощает
процесс настройки. Если инструмент firewall-config не установлен, система
предложит пользователю установить его. Для управления брандмауэром
необходимы права администратора, поэтому пользователь должен указать пароль
root. 
 
![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-43-09.png)

__Переключиться на постоянную конфигурацию__

__Действие:__ выберите «Постоянно» в раскрывающемся меню «Конфигурация».

__Объяснение:__ Параметр конфигурации определяет, будут ли изменения
применяться временно (во время выполнения) или постоянно. Если выбрать
«Постоянно», любые внесенные изменения сохранятся даже после перезагрузки
системы. Это гарантирует, что правила брандмауэра остаются согласованными и
их не нужно повторно применять вручную.

__Включите службы HTTP, HTTPS и FTP__

__Действие:__ В "общедоступной" зоне включите службы http, https и ftp.

__Пояснение:__ Зоны в брандмауэре определяют уровень доверия для сетевых
подключений. "Общедоступная" зона обычно используется для ненадежных сетей,
таких как Интернет. Включив эти службы, брандмауэр разрешает входящие
подключения для веб-трафика (HTTP/HTTPS) и передачи файлов (FTP) в
общедоступной зоне.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-43-00.png)

__Проверьте текущую конфигурацию брандмауэра__

__Команда:__ firewall-cmd --list-all

__Пояснение:__ Эта команда отображает текущую конфигурацию брандмауэра,
включая активные зоны, разрешенные службы, порты и протоколы. Поскольку
изменения были внесены в постоянную конфигурацию, они еще не отражены в
конфигурации среды выполнения.

 ![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab13/report/image/Screenshot from 2025-02-19 18-42-45.png)
 
## Вывод

Заключение Лабораторная работа позволила получить практический опыт работы с
firewall-cmd и лучше понять правила управления брандмауэром в системе Linux. Различие
между конфигурациями во время выполнения и постоянными конфигурациями и их
соответствующими вариантами использования является фундаментальной концепцией,
обеспечивающей эффективное управление брандмауэром.
В этой лабораторной работе было продемонстрировано, как настроить брандмауэр с
помощью графического интерфейса firewall-config. Благодаря включению определенных
служб, добавлению портов и внесению изменений сетевая безопасность системы была
адаптирована к конкретным требованиям. Различие между конфигурациями во время
выполнения и постоянными конфигурациями обеспечивает гибкость и контроль над
настройками брандмауэра.
 
 

