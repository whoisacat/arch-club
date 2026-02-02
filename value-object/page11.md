[prev](page10.md)
# QualitativeImpact

## Другой пример 

```java
@Slf4j
@Getter
@EqualsAndHashCode
public class QualitativeImpact {

public static final String INVALID_DATA_MESSAGE =
            "Invalid data. The quantitative assessment can only take values that are powers of two.";

    private final Integer value;

    public QualitativeImpact(Integer dbData) {
        if (dbData != null && !isPowerOfTwo(dbData)) {
            log.error("Invalid data - {} is not a power of 2", dbData);
            throw new CustomException(INVALID_DATA_MESSAGE);
        }
        this.value = dbData;
    }

    private boolean isPowerOfTwo(int n) {
        return (n != 0) && ((n & (n - 1)) == 0);
    }

    @Override
    public String toString() {
        return ofNullable(value).map(Object::toString).orElse("null");
    }
}
```
[next](page12.md)
