# Persistence Context
- 영속성 컨텍스트라고 불리며 ```Entity```를 영구적으로 저장하는 환경을 뜻한다.
- 어플리케이션과 DB 사이에서 ```Entity``` 객체를 보관하는 가상의 DB
- ```Persistence Context```는 ```Entity``` CRUD 시 ```Entity Manager```를 생성하여 ```Entity```객체를 보관하고 관리한다.
- ```Spring```에서는 보통 ```Entity Manager```를 주입하여 사용하고 같은 트랜잭션 범위에 있는 ```Entity Manager```는 같은 ```Persistence Context```에 접근하게 된다.

## 비영속(new/transient)
- 객체만 생성한 상태
```java
Member member = new Member(1L, "vision");
```
## 영속(managed)

## 준영속(detached)

# Persistence Unit
- EntityManager 인스턴스에 의해 관리되는 모든 엔티티 클래스 집합을 정의한다.