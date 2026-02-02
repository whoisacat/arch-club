[prev](page11.md)
# QualitativeImpact

## Использование

```java
public class QualitativeAssessment extends Auditable {

    public static final String INVALID_STATE = "Probability level and one of schedule level, cost level or performance level must be not null";
    private static final Set<Integer> REQUIRED_VALUES = Set.of(1, 2, 4, 8, 16);

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    Long id;
    @Convert(converter = QualitativeImpactConverter.class)
    QualitativeImpact probabilityLevel;
    @Convert(converter = QualitativeImpactConverter.class)
    QualitativeImpact scheduleLevel;
    ...
}

@Converter
public class QualitativeImpactConverter implements AttributeConverter<QualitativeImpact, Integer> {
    @Override
    public Integer convertToDatabaseColumn(QualitativeImpact attribute) {
        return ofNullable(attribute).map(QualitativeImpact::getValue).orElse(null);
    }

    @Override
    public QualitativeImpact convertToEntityAttribute(Integer dbData) {
        return new QualitativeImpact(dbData);
    }
}
```
