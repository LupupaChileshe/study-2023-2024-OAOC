---
## Front matter
lang: ru-RU
title: Отчет по лабораторной работе №9
subtitle: Отчет о мониторинге и настройке системных журналов
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

Цель данной лабораторной работы – изучение основ управления режимами SELinux,
восстановления контекста безопасности файлов, настройки нестандартного
расположения файлов веб-сервера и работы с переключателями SELinux. В ходе
выполнения работы студенты научатся изменять режимы работы SELinux,
корректировать контексты безопасности с помощью restorecon, настраивать SELinux
для работы веб-сервера и управлять SELinux-переключателями.

# Управление режимами SELinux

## Просмотр состояния SELinux

Команда sestatus -v вывела информацию:

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-06-35.png)

SELinux status: показывает, включена ли SELinux.
Current mode: текущий режим (Enforcing, Permissive, Disabled).
Policy version: используемая политика безопасности.
Loaded policy: загруженный набор правил безопасности.
Mode from config file: режим, установленный в конфигурации

## Определение текущего режима работы

Команда getenforce показала Enforcing (принудительный режим).

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-06-46.png)

## Изменение режима на Permissive

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-06-54.png)

setenforce 0 изменил режим на Permissive.
getenforce подтвердил изменение.


## Отключение SELinux через конфигурационный файл

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-07-03.png)

В файле /etc/sysconfig/selinux установлено SELINUX=disabled.
После перезагрузки система подтвердила отключение (getenforce вернул Disabled).

## Попытка включения SELinux без перезагрузки

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-07-22.png)

setenforce 1 не сработал, так как отключенный SELinux требует перезагрузки.

## Возвращение режима Enforcing

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-07-34.png)

В файле /etc/sysconfig/selinux установлено SELINUX=enforcing.
После перезагрузки система запустилась в режиме Enforcing, возможно с
предупреждением о необходимости восстановления меток.

# Использование restorecon для восстановления контекста безопасности



## Просмотр контекста файла /etc/hosts

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-07-49.png)

ls -Z /etc/hosts показал net_conf_t.


## Копирование файла и изменение контекста

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-07-57.png)

cp /etc/hosts ~/ создал копию с контекстом admin_home_t.


## Перемещение файла обратно и проверка контекста

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-08-05.png)

mv ~/hosts /etc сохранило admin_home_t.

## Исправление контекста

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-08-14.png)

restorecon -v /etc/hosts восстановил net_conf_t.


## Массовое исправление контекста

touch /.autorelabel и перезагрузка инициировали перемаркировку файловой системы

# Настройка контекста для нестандартного расположения веб-файлов



## Установка Apache и текстового браузера

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-08-32.png)

dnf -y install httpd lynx.

## Создание каталога и конфигурация Apache

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-08-43.png)

mkdir /web, добавлен index.html.

## В /etc/httpd/conf/httpd.conf изменен DocumentRoot на /web.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-08-50.png)


## Запуск Apache и тестирование через lynx

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-09-01.png)

systemctl start httpd, но страница по умолчанию не отображала новый контент.

## Изменение контекста безопасности

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-09-09.png)

semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?".
restorecon -R -v /web восстановил контекст.


## Повторное тестирование через lynx

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-09-20.png)

После перезагрузки веб-страница Welcome to my web-server отобразилась успешно.

## Общие рекомендации

# Работа с переключателями SELinux

## Просмотр переключателей для FTP

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-09-31.png)

getsebool -a | grep ftp показал ftpd_anon_write off.

## Просмотр переключателей с пояснениями

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab09/presentation/image/Screenshot from 2025-02-19 13-09-42.png)

semanage boolean -l | grep ftpd_anon подтвердил временное изменение.

## Установка постоянного значения
  setsebool -P ftpd_anon_write on сохранил изменение после перезагрузки.
  
## Проверка состояния после перезагрузки
  semanage boolean -l | grep ftpd_anon подтвердил on для ftpd_anon_write.







