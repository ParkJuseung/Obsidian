
#### 정의
DI는 **의존성 주입**을 의미한다. 즉, 객체가 의존하는 다른 객체를 직접 생성하지 않고, 외부에서 주입받는 방식이다. 스프링에서는 DI를 통해 IoC를 실현한다.


#### 왜 필요하지?
어떤 객체가 다른 객체를 직접 생성하면 두 객체는 강하게 결합되어 유연성이 떨어지게 된다. 하지만 DI를 사용하면 객체간의 결합도를 낮춰서 유지보수, 테스트, 확장이 쉬워진다.

### 3. DI의 종류

스프링에서 DI는 다음과 같은 방법으로 구현된다.

| ==**방법**== | ==**설명**==                | ==**예시**==   |
| :--------- | :------------------------ | :----------- |
| 생성자 주입     | 생성자를 통해 의존 객체를 주입         | 권장 방식        |
| 필드 주입      | 멤버 변수에 직접 주입 (@Autowired) | 간단하지만 테스트 불리 |
| 세터 주입      | setter 메서드를 통해 주입         | 선택적 의존성에 적합  |

- 생성자 주입 예시
```java
@Component
public class OrderService {
    private final OrderRepository orderRepository;

    public OrderService(OrderRepository orderRepository) {
        this.orderRepository = orderRepository;
    }
}

```


- 필드 주입 예시
```java
@Component
public class OrderService {
    @Autowired
    private OrderRepository orderRepository;
}

```


- 세터 주입 예시
```java
@Component
public class OrderService {
    private OrderRepository orderRepository;

    @Autowired
    public void setOrderRepository(OrderRepository orderRepository) {
        this.orderRepository = orderRepository;
    }
}

```









