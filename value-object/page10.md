[prev](page9.md)
# Деньги (Money)

## Пример

    ...
    public Money add(Money other) {
        assertSameCurrencyAs(other);
        return newMoney(this.amount + other.amount);
    }

    public Money[] allocate(int n) {
        Money lowResult = newMoney(this.amount / n);
        Money highResult = newMoney(lowResult.amount + 1);
        Money[] results = new Money[n];
        int remainder = (int) this.amount.longValue() % n;
        for (int i = 0; i < remainder; i++) {
            results[i] = highResult;
        }
        for (int i = remainder; i < n; i++) {
            results[i] = lowResult;
        }
        return results;
    }

    public Money[] allocate(long[] ratios) {
        return allocate(ratios, false);
    }

    public Money[] allocate(long[] ratios, boolean byOrder) {
        long total = 0;
        List<IndexedValue> pairs = new ArrayList<>();
        for (int i = 0; i < ratios.length; i++) {
            total += ratios[i];
            pairs.add(new IndexedValue(i, ratios[i]));
        }
        long remainder = this.amount;
        Money results[] = new Money[ratios.length];
        for (int i = 0; i < results.length; i++) {
            results[i] = newMoney(this.amount * ratios[i] / total);
            remainder -= results[i].amount;
        }
        if (byOrder) {
            pairs.sort(reverseOrder());
        }
        for (int i = 0; i < remainder; i++) {
            results[pairs.get(i).index].amount++;
        }
        return results;
    }
    ...
