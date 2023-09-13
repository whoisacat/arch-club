# Выбор типа интерфейса для инструмента для работы с пользователями KeyCloak

* Status: *proposed*
* Deciders: Цыпляшов А.Н.
* Date: 2023.09.12

Technical Story:
Реализовать скрипт на Python для удаления неактивный пользователей из Keycloack (Realm Greendata)
Задача https://jiradev.int.gazprombank.ru/jira/browse/URRP-7264

## Context and Problem Statement

Реализовать скрипт на Python для удаления неактивный пользователей из Keycloack (Realm Greendata):

1. Определить в БД Keycloack user_entity перечень пользователей у которых отсуствуют роли или группы в Realm
2. Удалить данных пользователей через API Keycloack

Должен быть справочник в который в рамках пункта 1 можно будет добавлять / удалять проверяемые роли.

Приложением надо управлять, желательно интерактивно. Нужно недорогое средство и удобное управления приложением.

## Decision Drivers <!-- optional -->

* Скорость разработки
* Простота пользования
* Возможность доработки

## Considered Options

* WEB интерфейс
* CLI со Spring Shell
* CLI без интерактивности

## Decision Outcome

Chosen option: "CLI со Spring Shell", because ...

### Positive Consequences <!-- optional -->

* [e.g., improvement of quality attribute satisfaction, follow-up decisions required, …]
* …

### Negative Consequences <!-- optional -->

* [e.g., compromising quality attribute, follow-up decisions required, …]
* …

## Pros and Cons of the Options <!-- optional -->

### WEB интерфейс

Обычное веб приложение с веб интерфейсом. Пока не потребуется интерактивный веб можно пользоваться интерфейсом Swagger

* Good, because Работающее и хорошо знакомое средство
* Good, because Дает гибкие возможности для реализации тонких клиентов
* Bad, because Самое затратное
* Bad, because Нужно дополнительно настраивать безопасность
* Bad, because Для реализации интеактивности нужен отдельный клиент

### CLI со Spring Shell

Консольное приложение выполняющее команды последовательно с возможностью интерактивного взаимодействия

* Good, because Относительно простое решение, не долго делать
* Good, because Безопасность не обеспечивается так как работает в пределах одной сессии
* Bad, because более треудозатратно чем взаимодействие через аргументы функции `main(Strin[] args...)`
* Нужно заносить зависимости в контур безопасности

### CLI без интерактивности

Самое простое приложение работающее через аргументы функции `main(Strin[] args...)` и выполняющее по одной задаче за запуск

* Good, because Самое дешевое и быстро реализуемое
* Bad, because Усложнена организация работы через функцию `main(Strin[] args...)`
* Bad, because Интерактивность очень сложно организовать
* Bad, because Развивать никто рне будет
* Bad, because Самое сложное в использовании (из-за необходимости постоянно запускать программу)

