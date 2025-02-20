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

Получение навыков настройки базовых и специальных прав доступа для групп
пользователей в операционной системе типа Linux.

# Задание

1. Прочитайте справочное описание man по командам chgrp, chmod, getfacl, setfacl.
2. Выполните действия по управлению базовыми разрешениями для групп
пользователей (раздел 3.3.1).
3. Выполните действия по управлению специальными разрешениями для групп
пользователей (раздел 3.3.2). 4. Выполните действия по управлению расширенными
разрешениями с использованием списков ACL для групп пользователей (раздел
3.3.3).

# Теоретическое введение

Основные права доступа в Linux в первую очередь определяются разрешениями для
файлов и каталогов. Эти разрешения обычно представлены тремя наборами
атрибутов rwx:
Разрешения пользователя (u): применяются к владельцу файла/каталога.
Групповые разрешения (g): применяются к членам группы файлов/каталогов.
Другие разрешения (o): применить ко всем остальным пользователям.
Каждому набору разрешений можно присвоить одно из трех значений:
Чтение (r): позволяет просматривать содержимое файла или просматривать
содержимое каталога.
Запись (w): позволяет изменять содержимое файла или добавлять/удалять
элементы в каталоге.
Выполнить (x): позволяет выполнить файл или перейти в каталог.
Эти разрешения объединяются в строку из 9 символов, первый символ которой
представляет тип файла (например, - для обычного файла, d для каталога).
Например, строка разрешения rw-r--r-- указывает:
Владелец имеет права на чтение/запись
Группа имеет разрешения только на чтениеДругие имеют разрешения только на чтение

# Выполнение лабораторной работы

1. Откройте терминал с учётной записью root: 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-11-25.png)

2. В корневом каталоге создайте каталоги /data/main и /data/third 
mkdir -p /data/main /data/third
Посмотрите, кто является владельцем этих каталогов. Для этого используйте:
ls -Al /data (рис. @fig:002)

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-11-53.png)

3. Прежде чем устанавливать разрешения, измените владельцев этих каталогов
с root на main и third соответственно: 
chgrp main /data/main
chgrp third /data/third
Посмотрите, кто теперь является владельцем этих каталогов:
ls -Al /data 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-12-03.png)

4. Установите разрешения, позволяющие владельцам каталогов записывать
файлы в эти каталоги и запрещающие доступ к содержимому каталогов всем
другим пользователям и группам: 
chmod 770 /data/main
chmod 770 /data/third
Проверьте установленные права доступа. 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-12-11.png)

5. В другом терминале перейдите под учётную запись пользователя bob
su - bob 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-12-32.png)

6. Под пользователем bob попробуйте перейти в каталог /data/main и создать
файл emptyfile в этом каталог 
cd /data/main
touch emptyfile
ls -Al 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-12-45.png)

7. Под пользователем bob попробуйте перейти в каталог /data/third и создать
файл emptyfile в этом каталоге. 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-12-56.png)

##Управление специальными разрешениями

1. Откройте новый терминал под пользователем alice

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-13-08.png)

2. Перейдите в каталог /data/main
cd /data/main
Создайте два файла, владельцем которых является alice:
touch alice1
touch alice2 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-13-22.png)

3. В другом терминале перейдите под учётную запись пользователя bob
(пользователь bob является членом группы main, как и alice):
su - bob 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-13-34.png)

4. Перейдите в каталог /data/main: 
cd /data/main
и в этом каталоге введите:
ls -l 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-13-45.png)

5. Создайте два файла, которые принадлежат пользователю bob:
touch bob1
touch bob2 



6. В терминале под пользователем root установите для каталога /data/main бит
идентификатора группы, а также stiky-бит для разделяемого (общего)
каталога группы: 
chmod g+s,o+t /data/main 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-13-54.png)

7. В терминале под пользователем alice создайте в каталоге /data/main файлы
alice3 и alice4: 
touch alice3
touch alice4
ls -l 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-14-03.png)

##Управление расширенными разрешениями с
##использованием списков ACL

1. Откройте терминал с учётной записью root
su -
y
2. Установите права на чтение и выполнение в каталоге /data/main для
группы third и права на чтение и выполнение для группы main в каталоге
/data/third:
setfacl -m g:third:rx /data/main
setfacl -m g:main:rx /data/third

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-14-10.png){#fig:0014 width=70%}

3. Используйте команду getfacl, чтобы убедиться в правильности установки
разрешений:
getfacl /data/main
getfacl /data/third 

![su –](/home/lupupachileshe/work/study2/2023-2024/OAOC/study_2023_2024_oaoc/Labs second semester/Lab03/report/image/Screenshot from 2025-02-18 16-14-51.png){#fig:0015 width=70%}

4. Создайте новый файл с именем newfile1 в каталоге /data/main:
touch /data/main/newfile1
Используйте
getfacl /data/main/newfile1

5. Установите ACL по умолчанию для каталога /data/main:
setfacl -m d:g:third:rwx /data/main



6. Добавьте ACL по умолчанию для каталога /data/third:
setfacl -m d:g:main:rwx /data/third



7. Убедитесь, что настройки ACL работают, добавив новый файл в каталог
/data/main:
touch /data/main/newfile2



8. Для проверки полномочий группы third в каталоге /data/third войдите в
другом терминале под учётной записью члена группы third: su - carol
Проверьте операции с файлами:
rm /data/main/newfile1
rm /data/main/newfile2
Проверьте, возможно ли осуществить запись в файл:
echo "Hello, world" >> /data/main/newfile1
echo "Hello, world" >> /data/main/newfile2

# Выводы

Я изучил получение функций для установки основных и специальных прав доступа
для групп пользователей в таких системах, как Linux.

