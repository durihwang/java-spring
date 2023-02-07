# Spring JPA @OneToOne Lazy Loading

# 목표
JPA 연관관계 사용 시 헷갈렸던 부분을 확인해보자.
```@OneToOne```과 ```@ManyToOne```에서의 Lazy Loading의 차이를 이해하자.

# Lazy Loading
## 내용
@OneToOne 연관 관계에서 ```Lazy Loading```이 안되는 경우에 대해서 알아보자.

## @OneToOne 에서의 Lazy Loading
### 예제
<img src="https://velog.velcdn.com/images/hwangduli515/post/e01765a6-49e2-4f3b-a376-44bf2009c40c/image.png">
<img src="https://velog.velcdn.com/images/hwangduli515/post/98775f92-23a0-40e7-bbd5-5f3f64576d21/image.png">


### 연관 관계의 주인(mappedBy의 반대쪽이자 위 예제에서는 Price)
<img src="https://velog.velcdn.com/images/hwangduli515/post/b629130c-5f84-4551-b1f3-9449028ce10f/image.png">
<img src="https://velog.velcdn.com/images/hwangduli515/post/875121ed-6f2b-4b69-bfa1-11da4c047e67/image.png">

- entity에 보이는 것처럼 Lazy로 설정을 했고 price만 조회가 되고 있다.

### 연관 관계의 주인 반대편(member)
<img src="https://velog.velcdn.com/images/hwangduli515/post/6904a59f-d29b-4fe1-b165-61d711c7d5f3/image.png">
<img src="https://velog.velcdn.com/images/hwangduli515/post/e415e553-3a43-48a7-ae41-42272e04ab8c/image.png">

- entity를 보면 알겠지만 Lazy로 설정했음에도 불구하고 price까지 같이 조회하고 있다.

### 이유
- price에는 member의 id를 확인할 수 있는 member_id 컬럼이 있지만 member는 price의 id를 확인할 수 있는 컬럼이 없기 때문에 select를 해서 알아올 수 밖에 없다.


### @ManyToOne 에서의 Lazy Loading
- 결론적으로 @ManyToOne은 mappedBy도 Lazy Loading이 가능하다.
- 그 이유는 컬럼이 없는 entity쪽에는 Collection 형태로 들어가기 때문에 null 형태로 가져올 수 있기 때문이다.

### 해결 방법
1. Shared PK
2. 주인 테이블에서 id 관리

### 정리
- 결론적으로는 @ManyToOne으로 사용이 가능하면 @ManyToOne을 쓰자.
- 그럼에도 이 내용을 정리한 이유는 @ManyToOne과 다르기 때문에 알고 쓰는 것과 모르고 쓰는 것은 차이가 있기 때문이다.