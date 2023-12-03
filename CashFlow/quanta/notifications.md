# Квант Оповещения
![Квант Бюджетирование](https://github.com/whoisacat/arch-club/blob/cash-flow/CashFlow/pics/notification-quanta.png?raw=true&sanitize=true#gh-light-mode-only)
![Квант Бюджетирование](https://github.com/whoisacat/arch-club/blob/cash-flow/CashFlow/pics/notification-quanta-dark.png?raw=true&sanitize=true#gh-dark-mode-only)

## Компоненты и их функционал

1. рассылает оповещения на различные клиенты
2. реализует логику доставки сообщений exact once

Состоит из сервиса оповещения, базы данных для реализации логики доставки сообщений exact once и клиентов провайдеров 
доставки сообщений.

## Ведущие архитектурные характеристики

### Топ 3
- Agility
- Simplicity
- Security
- Workflow

### Другие характеристики
- Configurability
- Scalability
- Performance
- Interoperability

## Архитектурный стиль

![Таблица выбора архитектурного стиля](https://github.com/whoisacat/arch-club/blob/cash-flow/CashFlow/pics/notification-style.jpeg?raw=true&sanitize=true#gh-light-mode-only)
![Таблица выбора архитектурного стиля](https://github.com/whoisacat/arch-club/blob/cash-flow/CashFlow/pics/notification-style-dark.jpeg?raw=true&sanitize=true#gh-dark-mode-only)

Гибрид (Микросервисная совместно с Событийно управляемая)

## Компромиссы - стратегия смягчения последствий
[См. здесь](https://github.com/whoisacat/arch-club/blob/cash-flow/CashFlow/quanta/budgeting.md#%D0%BA%D0%BE%D0%BC%D0%BF%D1%80%D0%BE%D0%BC%D0%B8%D1%81%D1%81%D1%8B---%D1%81%D1%82%D1%80%D0%B0%D1%82%D0%B5%D0%B3%D0%B8%D1%8F-%D1%81%D0%BC%D1%8F%D0%B3%D1%87%D0%B5%D0%BD%D0%B8%D1%8F-%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D1%81%D1%82%D0%B2%D0%B8%D0%B9).
