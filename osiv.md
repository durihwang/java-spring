# OSIV (open-session-in-view)
- open session in view (하이버네이트)
  - jpa가 생기기 전까지는 ```entityManager```를 ```session```으로 불렀다.
- open entityManager in view (JPA)
  - jpa가 생기고 ```osiv```는 ```oeiv```로 바뀌었지만 관례상 ```osiv```로 불린다.

## OSIV ON
![img_10.png](img_10.png)
> 출처: [실전! 스프링 부트와 JPA 활용2 - API 개발과 성능 최적화](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-API%EA%B0%9C%EB%B0%9C-%EC%84%B1%EB%8A%A5%EC%B5%9C%EC%A0%81%ED%99%94/dashboard)


## OSIV OFF
![img_12.png](img_12.png)
> 출처: [실전! 스프링 부트와 JPA 활용2 - API 개발과 성능 최적화](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-API%EA%B0%9C%EB%B0%9C-%EC%84%B1%EB%8A%A5%EC%B5%9C%EC%A0%81%ED%99%94/dashboard)