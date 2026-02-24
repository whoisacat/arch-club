# Паттерны offline конкурентного доступа
###### Patterns of Enterprise Application Architecture
###### By Martin Fowler, David Rice, Matthew Foemmel, Edward Hieatt, Robert Mee, Randy Stafford
###### Pub Date : November 05, 2002
###### Перевод названия главы — Типовые решения для обработки задач автономного параллелизма. Перевод offline как автономная мне тут кажется неудачным.
## Типовые _online_ решения
1. Optimistic Concurrency Control
```java
    @Version Long version;
```
2. Pessimistic Locking
```sql
    SELECT * FROM PUBLIC.RISK FOR UPDATE;
```
3. MVCC (Multiversion Concurrency Control)

<code>это способ, которым база данных хранит и читает строки.</code>

[next](page2.md)