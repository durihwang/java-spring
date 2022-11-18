# Spring Test

스프링에서 테스트를 작성하는 방법은 여러가지가 있다.

이중에서 내가 사용했던 방식을 정리해 보려고 한다.

## 통합 테스트

- ```@SpringBootTest```를 이용하여서 전체적인 플로우 테스트
- 모든 bean을 등록하기 때문에 전체적인 시간이 오래 걸린다.

## Controller 테스트

- ```@WebMvcTest```를 이용하여 컨트롤러와 연관된 bean만 제한적으로 등록

## Service 테스트

- ```@ExtendWith(MockitoExtension.class)```를 이용하여 Mock 객체를 생성한 후 테스트를 진행한다.
- ```@Mock```
    - 객체에 해당 어노테이션을 설정하면 ```mock```객체로 생성된다.
- ```@InjectMocks```
    - 해당 어노테이션이 붙은 객체에 주입이 필요한 객체가 있으면 ```null```로 주입시켜 준다.
- Mockito vs BDDMockito
    - ```mock```객체를 이용하여 테스트 시에는 ```Mockito```보다는 ```BDDMockito```를 사용해주자.
    - 이유는 아래 코드를 보면 이해할 수 있다.
- Mockito
    ```java
    //given
    when(seller.askForBread()).thenReturn(new Bread());
    
    //when
    Goods goods = shop.buyBread();
    
    //then
    assertThat(goods, containBread());
    ```
    - ```given```에 해당하는 부분에 ```when``` 메소드를 사용해야 함.
- BDDMockito
    ```java
    //given  
    given(seller.askForBread()).willReturn(new Bread());
    
    //when
    Goods goods = shop.buyBread();
    
    //then
    assertThat(goods, containBread());
    ```
    - ```given```에 해당하는 부분에 ```given``` 메소드를 넣어 주어 이해하기 쉽다.

## Repository 테스트

- ```@DataJpaTest```를 이용하여 ```@Entity```가 있는 객체들만 스캔하여 ```TestEntityManager```를 생성 및 설정한다.
- ```@AutoConfigureTestDatabase```
    - ```@DataJpaTest```를 이용하면 기본 인메모리 db로 실행하는데 다른 db를 사용하고 싶을 때 쓴다.
    - ```@AutoConfigureTestDatabase(replace = Replace.NONE)```
- repository 구현체에 어노테이션을 안붙이는 이유
    - ```@DataJpaTest```로 테스트를 할 때 ```lombok``` 어노테이션을 사용하면 ```bean``` 등록이 안된 클래스가 있을 수 있어서 가능하면 직접 생성자를
      생성해서 사용한다.

## Debug

- 이건 ```IntelliJ```에서만 해당되지만 ```local```테스트 시에는 항상 ```debug``` 모드를 활성화 하면 조금 더 편하게 개발을 할 수 있다.