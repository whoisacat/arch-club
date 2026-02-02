[prev](page7.md)
# Деньги (Money)

## Пример
```java
public class Money implements Comparable<Money>, Serializable {
    
    private Long amount;
    private Currency currency;
    private String currencyCode;
    private int roundingMode = ROUND_HALF_UP;

    public Money() {
        if (!StringUtils.isEmpty(currencyCode)) {
            setCurrency(Currency.getInstance(currencyCode));
        }
    }

    public Money(Money money) {
        this.amount = money.getAmount();
        this.currency = money.getCurrency();
        this.roundingMode = money.getRoundingMode();
        this.currencyCode = money.getCurrencyCode();
    }

    public Money(Long amount, Currency currency) {
        setCurrency(currency);
        setAmount(amount);
    }

    public Money(BigDecimal amount, String currency) {
        this(amount, Currency.getInstance(currency));
    }
    ...
}
```
[next](page9.md)