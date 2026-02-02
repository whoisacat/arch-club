[prev](page8.md)
# Деньги (Money)

## Пример
```java
    public boolean equals (Object other) {
        return (other instanceof Money) && equals ((Money) other);
    }

    public boolean equals (Money other) {
        return currency, equals (other. currency) && (amount *= other.amount);
    }

    public int hashCode() {
        return (int) (amount ^ (amount >>> 32));
    }
```
[next](page10.md)