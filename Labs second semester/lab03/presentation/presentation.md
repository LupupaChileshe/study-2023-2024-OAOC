---
## Front matter
lang: ru-RU
title: Структура научной презентации
subtitle: Простейший шаблон
author:
  - Чилеше . Л
institute:
  - Российский университет дружбы народов, Москва, Россия
  - Объединённый институт ядерных исследований, Дубна, Россия
date: 01 января 1970

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
  * Студеднт Группы НПИбд-03-23
  * Российский университет дружбы народов
  
:::
::: {.column width="30%"}



:::
::::::::::::::

# Вводная часть

## Цель работы

Получение навыков настройки базовых и специальных прав доступа для групп
пользователей в операционной системе типа Linux.


## Задание

- Прочитайте справочное описание man по командам chgrp, chmod, getfacl,
  setfacl.
- Выполните действия по управлению базовыми разрешениями для групп
  пользователей (раздел 3.3.1).
- Выполните действия по управлению специальными разрешениями для
  групп пользователей (раздел 3.3.2). 4. Выполните действия по управлению
  расширенными разрешениями с использованием списков ACL для групп
  пользователей (раздел 3.3.3).
  
## терминал с учётной записью root:
 
 su - 

## /data/main и /data/third mkdir -p

- В корневом каталоге создайте каталоги /data/main и /data/third mkdir -p
 /data/main /data/third Посмотрите, кто является владельцем этих каталогов.
 Для этого используйте: ls -Al /data

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/presentation/image/Screenshot from 2025-02-18 16-11-25.png)

## chgrp main /data/main chgrp third/data/third

- Прежде чем устанавливать разрешения, измените владельцев этих катало-
  гов с root на main и third соответственно: chgrp main /data/main chgrp third
  /data/third Посмотрите, кто теперь является владельцем этих каталогов: ls
  -Al /data
  
 ![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/presentation/image/Screenshot from 2025-02-18 16-11-53.png) 
  

##сhmod 770 /data/main chmod 770/data/third

- Установите разрешения, позволяющие владельцам каталогов записывать
  файлы в эти каталоги и запрещающие доступ к содержимому каталогов
  всем другим пользователям и группам: chmod 770 /data/main chmod 770
  /data/third Проверьте установленные права доступа.
  
![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/presentation/image/Screenshot from 2025-02-18 16-12-03.png)

## su - bob

 В другом терминале перейдите под учётную запись пользователя bob su -
bob

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/presentation/image/Screenshot from 2025-02-18 16-12-11.png)

## ls -Al

- Под пользователем bob попробуйте перейти в каталог /data/main и создать
- файл emptyfile в этом каталог cd /data/main touch emptyfile ls -Al

![]()

## перейти в каталог /data/third

- Под пользователем bob попробуйте перейти в каталог /data/third и создать
  файл emptyfile в этом каталоге.
  
![]()

## alice

- Откройте новый терминал под пользователем alice

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/presentation/image/Screenshot from 2025-02-18 16-12-45.png)

## touch alice1 touch alice2

- Перейдите в каталог /data/main cd /data/main Создайте два файла, владель-
  цем которых является alice: touch alice1 touch alice2
  
![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/presentation/image/Screenshot from 2025-02-18 16-12-56.png)
  
## Перейдите в каталог /data/main: cd /data/main и в этом каталоге введите: ls -l



![]()

## chmod g+s,o+t /data/main

- В терминале под пользователем root установите для каталога /data/main
  бит идентификатора группы, а также stiky-бит для разделяемого (общего)
  каталога группы: chmod g+s,o+t /data/main
  
![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/presentation/image/Screenshot from 2025-02-18 16-13-22.png)

## touch alice3 touch alice4 ls -l

- В терминале под пользователем alice создайте в каталоге /data/main файлы
  alice3 и alice4: touch alice3 touch alice4 ls -l

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/presentation/image/Screenshot from 2025-02-18 16-13-34.png)

## “Hello, world”

- Для проверки полномочий группы third в каталоге /data/third войдите в
  другом терминале под учётной записью члена группы third: su - carol Про-
  верьте операции с файлами: rm /data/main/newfile1 rm /data/main/newfile2
  Проверьте, возможно ли осуществить запись в файл: echo “Hello, world” »
  /data/main/newfile1 echo “Hello, world” » /data/main/newfile2

## “Hello, world”

![](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/presentation/image/Screenshot from 2025-02-18 16-14-51.png)

## Выводы

Я изучил получение функций для установки основных и специальных прав
доступа для групп пользователей в таких системах, как Linux.




