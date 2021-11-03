---
title: Тестовое задание на позицию Junior DevOps
layout: single-copy
classes: wide
author_profile: true
author: Pavel Shiryaev
---

## Введение

Задание направлено в первую очередь на проверку умений: `python`, `bash`, `git`.

Рекомендуемое время выполнения: **3 часа**.

Ожидаемый результат: репозиторий на GitHub, либо git репозиторий упакованный в архив.

Можно выполнить любой объём задания.

## Задача

Написать утилиту, которая обходит файлы/каталоги проекта рекурсивно, и вставляет в начало определенных исходных файлов лицензию как комментарий.

Хочется чтобы получилось 2 скрипта: 

 - `tree_license` - обходит дерево и вставляет лицензию если нужно
 - `render` - отрисовщик лицензии по шаблону

Один из этих скриптов нужно написать на `shell`, другой на `python3`. Выбор какой на чем - за вами.

**Сигнатура tree_license:**

```bash
./tree_license [-h] [-f путь_к_лицензии] [-l путь_к_лог_файлу] путь_к_проекту
``` 

Скрипт должен запускаться через командную строку, c указанием пути к проекту в качестве единственного обязательного аргумента.

Должна быть возможность указать путь к файлу лицензии через опциональный параметр (ключ `-f`), если его нет, то значение брать из переменной окружения `LICENSE_FILE_PATH`.
Если и она пустая, то упасть в ошибку.
Должна быть возможность указать путь к лог файлу через ключ `-l`, если его нет, то пишем лог в текущую директорию в файл `license.log`

Для формирования текста лицензии он должен звать `render`

Если какой-то файл проекта уже содержит лицензию, дописывать еще одну лицензию не нужно - проверьте, есть ли в файле уже лицензия.

В конце, при успешном исполнении вывести количество измененных файлов в `stdout`, список измененных имен и путей в `log` файл.
При любой ошибке вывести красивое сообщение об ошибке в `stderr`.

**Пример вызова render:**

```bash
./render \
    --filename="имя_файла" \
    --root_folder="корневая папка проекта" \ 
    --year="текущий год" \
    --org_name="StackSoft" \
    /путь/к/файлу/лицензии
```

Через `--` указываются переменные для подстановки, они опциональны. Путь к лицензии - обязателен.
Если в шаблоне лицензии есть переменные, которых не было передано на вход, то они должны замениться на пустую строку.
Скрипт только заполняет шаблон, и возвращает текст шаблона в `STDOUT` со вставленными значениями переменных, за вставку готовой лицензии в файл отвечает `tree_license`.

### Требования

**Обязательные:**

 - Использовать `python3`
 - Использовать `bash`, или любой другой `POSIX-compliant shell`
 - Осмысленный контроль версий в `git`, не так что один царь-коммит и все :)
 - Приложение пишем с использованием встроенных в `python3` стандартных библиотек
 - Обработка `.py` и `.sh` файлов в проекте

**Дополнительные очки:**

 - Обработка `.html` и `.css` файлов в проекте
 - Простые юнит-тесты
 - Оформить как `pip`-пакет, с добавлением в `path` и возможностью запуска через консоль после установки (`setup.py`, `setuptools`, сделать `entrypoint`).
 - Поощряется кросс-платформенность, проверить на `linux` и `windows`.
 - `docker`-контейнер, опять же чистенький, с точкой входа, чтобы можно было запускать приложение через `docker run app`/`docker attach app`.
 - Подумайте над тем, как хранить данные (`docker-volume`, монтировать директорию).

### Технические детали 

По вставке лицензии и комментариям:

 - Для `sh` и `py` вставлять в начале файла со знаком комментария `#`, но не забываем про `hashbang`(об этом ниже) 
 - Для `html` файлов лицензия должна быть вставлена внури тэга `<head>` как комментарий `<!-- -->`
 - Для `css` просто в самое начало, комментарий `/* ... */`

Файлы проекта могут содержать `hashbang`, например, `#!/usr/bin/python`, `#!/bin/sh`.
Лицензия должна быть вставлена **после** `hashbang` и **до** всего остального кода.
Если `hashbang` отсутствует, то лицензия должна быть вставлена **в начало файла**.


## Входные данные

**Проект**

[Ссылка на скачивание архива с проектом](Cufflinks-master.tar.gz)
 
**Шаблон лицензии проекта**


Cодержание шаблона:

    File: ${filename}
    Project: ${root_folder}
    
    Copyright (c) ${year} ${org_name}

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.

Как не трудно догадаться, переменные оформлены как `${...}`


