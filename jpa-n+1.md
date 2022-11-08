# JPA N+1 정리

Eager loading의 경우 findById(@ID)를 사용하는 경우는 자체적으로 inner join 형태의 쿼리를 만들어서 조회하기 때문에 n+1 문제가 발생하지 않는다.