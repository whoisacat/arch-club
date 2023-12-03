# Определение составных частей системы

## Выделение агрегатов и связей между ними

### Outgoing/Incoming
`BalanceSheet
BalanceItem
TotalItem
PayDays?
Payments`

1. Изменяет собственный баланс
2. Изменяет состояние Accounts (async к [Accounts]())
3. Оповещает о перерасходах (async к [Notification]())
4. Изменяет состояние в cb-service (async к [Cash-back]())

### Reallocation

1. Изменяет финальное распределение средств бюджетных категорий

### Accounts
`BalanceSheet
BalanceItem (Account)
TotalItem`

1. Хранит состояние счетов, считает переводы между счетами
2. Оповещение при снижении и превышении уровня какого-то из тотал (async к [Notification]())

### Debt
`DebtItem`

1. Хранит список долгов с суммами и датой истечения срока долга
2. Оповещение об истечении срока (async к [Notification]())
3. предлагает занести доход или просто изменить [Accounts]() (async к [Incoming]() или [Accounts]())
4. предлагает занести расход или просто изменить [Accounts]() (async к [Outgoing]() или [Accounts]())

### RegularSettings
`OutgoingBalanceSheetSetting
OutgoingBalanceItemSetting
OutgoingTotalItemSetting
IncomingBalanceSheetSetting
IncomingBalanceItemSetting
IncomingTotalItemSetting
AccountsBalanceSheetSetting
AccountsBalanceItemSetting
AccountsTotalItemSetting
InternalBalanceSheetSetting
InternalBalanceItemSetting
InternalTotalItemSetting`

1. хранит и отдает настройки для бюджетных периодов, категорий и единиц (sync от любого)
2. создает по расписанию бюджетные периоды (async)
3. напоминает о регулярных платежах (async к [Notification]())


### WishList

1. Хранит список покупок с приоритетами
2. При закрытии элемента должна предложить занести расход (async к [Outgoing]())
3. Должна содержать статью расхода и предполагаемую дату
4. совместное редактирование
5. Оповещения об изменении (async к [Notification]())


### Cash-back
Хранит категории кэшбэка по банкам со сроками их окончания и предельными суммами
1. напоминает об окончании срока кэшбэка (async к [Notification]())
2. напоминает выбрать кэшбэк в новом периоде (async к [Notification]())
3. оповещает о достижении максимальной суммы кэшбэка (async к [Notification]())

### Notification

1. рассылает оповещения на различные клиенты
2. реализует логику доставки сообщений exact once

### History
1. принимает объекты и хранит их первоначальное состояние, дифы и признак удаления с временем изменения (async от любого)

### Analytics

Расширяемый список аналитики (async от любого):
- кредитный потенциал
- частота перераспределений средств между статьями
- скорость накопления средств
- отчеты за периоды

## Связи между агрегатами
![Связи между агрегатами](https://github.com/whoisacat/arch-club/blob/cash-flow/CashFlow/pics/communication.png?raw=true&sanitize=true#gh-light-mode-only)
![Связи между агрегатами](https://github.com/whoisacat/arch-club/blob/cash-flow/CashFlow/pics/communication-dark.png?raw=true&sanitize=true#gh-dark-mode-only)

## Группировка частей системы
Так как некоторые нефункциональные требования к системе можно отнести только к отдельным ее частям и на схеме связей 
компонентов системы преобладают асинхронные связи, то систему предполагается разделить на кванты, независимые 
компоненты системы с высокой внутренней связностью и низкой связанностью с другими частями системы. Компоненты с 
синхронными связями (синхронной динамической конасценцией) определяют отдельный квант, компоненты без синхронных связей
(с асинхронной динамической конасценцией) и со схожими нефункциональными требованиями определяют остальные кванты.

> [!NOTE]
> Сервис по аутентификации и авторизации на схеме не показан и не участвует в определении структуры системы из-за большой неопределенности деталей его реализации и принятие решения о его влияния на структуру сдвигается на этап реализации

## Структура Квант - Компонент
- Бюджетирование:
  - Outgoing
  - Incoming
  - Reallocation
  - Accounts
  - RegularSettings
- Инструменты учета:
  - Debt
  - WishList
  - Cash-back
- Оповещение (Notification)
  - Все возможные каналы связи с пользователями
- Аудит (History)
- Аналитика
