# Выбор языка для реализации инструмента для работы с пользователями KeyCloak

* Status: *accepted*
* Deciders: Зиновьев А.Н., Цыпляшов А.Н.
* Date: 2023.09.08

Technical Story:
Реализовать скрипт на Python для удаления неактивный пользователей из Keycloack (Realm Greendata)
Задача https://jiradev.int.gazprombank.ru/jira/browse/URRP-7264

## Context and Problem Statement

Реализовать скрипт на Python для удаления неактивный пользователей из Keycloack (Realm Greendata):

1. Определить в БД Keycloack user_entity перечень пользователей у которых отсуствуют роли или группы в Realm
2. Удалить данных пользователей через API Keycloack

Должен быть справочник в который в рамках пункта 1 можно будет добавлять / удалять проверяемые роли.

## Decision Drivers

* Скорость разработки
* Простота пользования
* Возможность доработки

## Considered Options

* Написать на Python
* Написать на Bash
* Написать на Java

## Decision Outcome

Chosen option: "Написать на Java", because:
1. Синтаксис языка и библиотеки для реализации знакомы исполнителю, что позволит выполнить проект быстрее, чем на других языках.
2. В данном варианте возможно использование без деплоя (выполнение с виртуалки при доступных портах и копирование jar файла при работе с сервера)
3. Возможности доработки завсят только от ресурсов.

### Positive Consequences

* Синтаксис языка и библиотеки для реализации знакомы исполнителю, что позволит выполнить проект быстрее, чем на других языках.
* В данном варианте возможно использование без деплоя (выполнение с виртуалки при доступном хосте и копирование jar файла при работе с сервера)
* При необходимости доработки есть большое количество исполнителей, которые могут ее реализовать (разработчики)

### Negative Consequences

* Необходима сборка из исходного кода и установленная java определенной версии
* Некоторых зависимостей нет в контуре, сборка возможна только с занесенными зависимостями
* Для доработки сложно будет задействовать специалистов по эксплуатации

## Pros and Cons of the Options

### Написать на Python

* Good, because Простой язык с простым синтаксисом и низким порогом входа, широко распространен в среде поддержки
* Good, because Интерпретируемый язык, не зависит от операционной системы
* Good, because Интерпритатор установлен на большинстве серверов
* Good, because Для запуска утилиты не нужна сборка, достаточно создать и запустить текстовый файл с программой
* Bad, because Исполнитель не знаком с библиотеками и фреймворками для реализации задачи, что увеличит время на разработку инструмента 
* Bad, because Для запуска может понадобиться загрузка библиотек определенных версий, что может привести к конфликтам в уже работающих на машинах программах
* Bad, because На некоторых машинах придется установить интерпритатор

### Написать на Bash

* Good, because Bash установлен на всех серверах
* Good, because Язык примерно одинаково знаком и разработчикам и специалистам по эксплуатации
* Good, because Для запуска утилиты не нужна сборка, достаточно создать и запустить текстовый файл с программой
* Good, because Большое количество утилит которые можно использовать при написании программы уже установлено на машинах
* Bad, because На рабочих станциях разработчиков операционная система Windows, интерпритатор может отличаться от серверного
* Bad, because Сложный язык не лучшее решение для написания сложных программ с дальнейшей поддержкой

### Написать на Java

* Good, because Синтаксис языка и библиотеки для реализации знакомы исполнителю, что позволит выполнить проект быстрее, чем на других языках.
* Good, because В данном варианте возможно использование без деплоя (выполнение с виртуалки при доступном хосте и копирование jar файла при работе с сервера)
* Good, because При необходимости доработки есть большое количество исполнителей, которые могут ее реализовать (разработчики)
* Bad, because Необходима сборка из исходного кода и установленная java определенной версии
* Bad, because Некоторых зависимостей нет в контуре, сборка возможна только с занесенными зависимостями
* Bad, because Не все разработчики, поэтому для доработки сложно будет задействовать специалистов по эксплуатации

## Links 
