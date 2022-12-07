# 객체지향 쿼리

## JPQL

## JPA Criteria

## Querydsl
- 정적 타입을 이용해서 SQL과 같은 쿼리를 생성할 수 있도록 해주는 오픈 소스

### OrderSpecifier
- ```orderBy``` 메소드를 사용하기 위해서는 ```OrderSpecifier``` 클래스를 구현하여 파라미터로 넣어 주어야 한다.
- 파라미터로 넘어온 Pageable 인터페이스를 이용해 동적으로 orderBy를 구현하기 위해서는 아래와 같이 사용해주면 된다.
```java
/**
 * 파라미터로 전달 받은 sort 동적 쿼리 생성
 * @param pageable
 * @return
 */
private OrderSpecifier[] getAllOrder(Pageable pageable) {

    // OrderSpecifier 클래스는 1~N개로 구현 가능하기 때문에 []로 생성해준다.
    OrderSpecifier[] orderSpecifiers = null;

    // Pageable 인터페이스에서 sort 관련 파라미터가 존재하는 경우 OrderSpecifier 클래스를 구현해준다.
    if (!pageable.getSort().isEmpty()) {
    orderSpecifiers = pageable.getSort().stream().map(sort -> {

    Order direction = sort.getDirection().isAscending() ? Order.ASC : Order.DESC;
    
    // orderBy를 할 entity의 Q class에 Pageable 인터페이스의 Sort 클래스 파라미터로 넘어온 컬럼을 이용하여 생성해준다.
    return new OrderSpecifier(direction, new QBillTaxInfo(sort.getProperty()));

    }).toArray(OrderSpecifier[]::new);
    }

    // sort 파라미터가 없는 경우에는 기본 order 조건을 넣어준다. (null은 허용하지 않기 때문)
    if (orderSpecifiers == null) {
        orderSpecifiers = Stream.of(new OrderSpecifier(Order.DESC, billTaxInfo.seqNo))
            .toArray(OrderSpecifier[]::new);
    }

    return orderSpecifiers;
}
```

## 네이티브 SQL

## JDBC API