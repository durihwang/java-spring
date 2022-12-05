# 객체지향 쿼리

## JPQL

## JPA Criteria

## Querydsl
- 정적 타입을 이용해서 SQL과 같은 쿼리를 생성할 수 있도록 해주는 프레임워크

### OrderSpecifier
- ```orderBy``` 메소드를 사용하기 위해서는 ```OrderSpecifier``` 클래스를 구현하여 파라미터로 넣어 주어야 한다.
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

            // sort의 순서가 ASC인지 DESC인지 확인
            Order direction = sort.getDirection().isAscending() ? Order.ASC : Order.DESC;
            
            // 프로퍼티에 따라서 오더링 기준 컬럼을 넣어 OrderSpecifier를 생성한다.
            return switch (sort.getProperty()) {
                case "seqno" -> new OrderSpecifier(direction, billTaxInfo.seqNo);
                case "alias" -> new OrderSpecifier(direction, billTaxInfo.alias);
                default -> new OrderSpecifier(direction, billTaxInfo.seqNo);
            };

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
- 위처럼 ```getSort()``` 메소드의 ```getProperty()```를 직접 ```OrderSpecifier``` 클래스에 넣어주지 않고 ```Qclass```를 사용한 이유는 ```@QueryProjection```을 이용하여 ```select```를 하는 경우에는 ```entity```와 ```querydto```가 연결이 안되기 때문이다.
- ```selectFrom()```메소드를 사용하는 경우라면 ```OrderSpecifier``` 생성 시 ```sort```로 전달 받은 프로퍼티 값을 그대로 넣어주어도 무방하다.

## 네이티브 SQL

## JDBC API