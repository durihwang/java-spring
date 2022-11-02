# JPA 조인 전략

## 조인 전략
```InheritanceType.JOINED```

## 단일 테이블 전략
```InheritanceType.SINGLE_TABLE```

## 구현 클래스 테이블 전략
```InheritanceType.TABLE_PER_CLASS```

## @MappedSuperClass
- BaseEntity의 개념으로 공통적으로 사용할 컬럼 속성이 필요할 때 사용한다.
- 설계상 추상 클래스로 만드는 것이 좋다.