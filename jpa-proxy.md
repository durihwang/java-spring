# JPA Proxy

## getReference()
- Entity를 리턴하는 것이 아닌 프록시 객체를 리턴해준다.
- 해당 프록시 객체에서 실제로 값을 사용할 때에만 쿼리를 실행한다.
```ex) getReference().getId()```

## 초기화
- getReference()을 이용하여 프록시 객체를 생성한 이후 find() 함수를 실행해도 해당 객체는 Entity 객체로 바뀌지 않고 Entity 객체로의 접근이 가능해 지는 것이다.
- 이유는 JPA 구현체인 하이버네이트 매커니즘 상 기존 객체와의 동일성을 보장하기 위해서다.
- 때문에 타입 체크 시에는 ```==``` 비교가 아닌 ```instanceOf```로 비교해야 한다.
- 반대로 find() 함수로 Entity를 조회했으면 getReference()를 실행해도 프록시 객체가 아닌 Entity 객체가 반환된다.

## could not initialize proxy
- Exception 이름
    - ```LazyInitializationException```
- 영속성 컨텍스트에 해당하는 Entity가 없는 경우에 발생하는 예외
- 다시 말하면 영속성 컨텍스트는 보통 트랜잭션과 생명 주기를 같이 하는데 해당 예외가 일어난 곳에서 트랜잭션이 끝났을 가능성이 높다.
### 해결
1. 즉시 로딩으로 변경
    - 즉시 로딩으로 변경하여 프록시 객체가 아닌 실제 Entity 객체를 가져온다.
2. 트랜잭션
    - 예외가 발생한 곳에 트랜잭션을 선언하거나 트랜잭션 범위 안으로 로직을 이동시켜 준다.

## 프록시 객체 초기화 여부
- 사용
    - ```emf.getPersistenceUnitUtil().isLoaded(refMember)```
    - 프록시 객체의 초기화 여부를 알 수 있는 메소드