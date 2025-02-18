---
## Front matter
lang: ru-RU
title: Отчет по лабораторной работе №4
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

- Получить навыки управления системными службами операционной системы
посредством systemd.

## systemctl status vsftpd

- Получите полномочия администратора
  su –
- Проверьте статус службы Very Secure FTP:
  systemctl status vsftpd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-36-20.png)

## dnf -y install vsftpd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-36-32.png)

## systemctl start vsftpd systemctl status vsftpd

Вывод команды должен показать, что служба в настоящее время работает, но не
будет активирована при перезапуске операционной системы.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-36-42.png)

## ls /etc/systemd/system/multi-user.target.wants

- Должно отобразиться, что ссылка на vsftpd.service не существует.

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-37-13.png)

## systemctl enable vsftpd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-36-53.png)

## systemctl status vsftpd

Теперь вы увидите, что для файла юнита состояние изменено с disabled на enabled.e`

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-37-36.png)

## systemctl list-dependencies vsftpd

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-37-47.png)

## systemctl list-dependencies vsftpd –reverse

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-37-57.png)

# Конфликты юнитов


## dnf -y install iptables\*

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-38-12.png)

## systemctl status firewalld

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-38-23.png)

## systemctl status iptables

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-38-34.png)

## systemctl start firewalld systemctl start iptables

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-38-34.png)

## cat /usr/lib/systemd/system/firewalld.service


![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-38-43.png)

## cat /usr/lib/systemd/system/iptables.service

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-38-43.png)

## systemctl stop iptables и загрузите службу firewalld systemctl start firewalld

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-39-01.png)

## systemctl mask iptables

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-39-12.png)

## systemctl enable iptables

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/lab05/presentation/image/Screenshot from 2025-02-19 00-39-21.png)


