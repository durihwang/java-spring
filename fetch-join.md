# 페치 조인(Fetch Join)
- ```JPQL``` 에서 성능 최적화를 위해 제공하는 기능
- 연관된 ```Entity```나 ```Collection```을 한번에 조회하는 기능

## ```fetch join``` 시에 별칭 및 ```on``` 사용
- 일대다 관계 ```fetch join``` 시에 ```on``` 절을 사용하게 되면 ```entity```와 ```db``` 사이에 데이터 불일치가 발생한다.
- A와 B 관계가 ```1:N```이라고 가정할때 A에는 B의 데이터가 모두 들어가 있다. 그런데 ```on```으로 조건을 변경하여 B에 예상하는 데이터가 없는 경우 데이터 일관성이 깨지게 된다.
- 따라서 ```fetch join``` 조건이 필요할 때에는 ```dto```를 이용해서 조회해야 한다.
## 컬렉션 ```fetch join```
- 일대다 관계에서 ```fetch join```을 하게 되는 경우 다 기준으로 데이터가 생성되기 때문에 ```distinct```를 이용하여 중복제거를 해준다.
- ```with-clause not allowed on fetched association``` 에러가 발생

## ```fetch join```의 한계
- 컬렉션 ```fetch join``` 시에는 페이징을 사용할 수 없다.