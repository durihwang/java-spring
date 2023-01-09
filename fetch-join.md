# 페치 조인(Fetch Join)
- ```JPQL``` 에서 성능 최적화를 위해 제공하는 기능
- 연관된 ```Entity```나 ```Collection```을 한번에 조회하는 기능


## 컬렉션 ```fetch join```
- 일대다 관계에서 ```fetch join```을 하게 되는 경우 다 기준으로 데이터가 생성되기 때문에 ```distinct```를 이용하여 중복제거를 해준다.
## ```fetch join```의 한계