# JPA N+1 정리

EAGER
- findById같은 메소드는 문제가 없지만 findAll같은 메소드를 실행하면 자식 메소드까지 영속화 하기 위해서 N+1만큼의 쿼리가 실행되게 된다.
- Eager loading의 경우 findById(@ID)를 사용하는 경우는 자체적으로 inner join 형태의 쿼리를 만들어서 조회하기 때문에 n+1 문제가 발생하지 않는다.

LAZY
- 어떤 메소드를 사용하던 쿼리는 한번만 실행되겠지만, 자식 메소드(현재 프록시 객체)를 사용하게 되는 순간 N+1의 쿼리가 실행되게 된다.

즉시로딩
- jpql을 우선적으로 select하기 때문에 즉시로딩을 이후에 보고 또다른 쿼리가 날아가 N+1

지연로딩
- 지연로딩된 값을 select할 때 따로 쿼리가 날아가 N+1

fetch join
- 지연로딩의 해결책
- 사용될 때 확정된 값을 한번에 join에서 select해서 가져옴
- Pagination이나 2개 이상의 collection join에서 문제가 발생

Pagination
- fetch join 시 limit, offset을 통한 쿼리가 아닌 인메모리에 모두 가져와 application단에서 처리하여 OOM 발생
- BatchSize를 통해 필요 시 배치쿼리로 원하는 만큼 쿼리를 날림 > 쿼리는 날아가지만 N번 만큼의 무수한 쿼리는 발생되지 않음
  
2개 이상의 Collection join
- List 자료구조의 2개 이상의 Collection join(~ToMany관계)에서 fetch join 할 경우 MultipleBagFetchException 예외 발생
- Set자료구조를 사용한다면 해결가능 (Pagination은 여전히 발생)
- BatchSize를 사용한다면 해결가능 (Pagination 해결)