
### 1. 정의

**Bean은 스프링 컨테이너가 생성하고 관리하는 객체(인스턴스)를 말한다.**  
개발자가 직접 `new`로 만드는 게 아니라,  
**스프링이 대신 생성하고, 이름을 붙이고, 주입까지 해주는 객체**가 Bean이다.

즉, **스프링 컨테이너에 등록된 객체 = Bean**

---

### 2. 왜 Bean이라는 용어를 쓰는가?

- Java EE 시대부터 쓰던 전통적인 용어다.
- EJB(고전)시절 객체를 Bean이라고 불렀다.
- 원래는 "재사용 가능한 구성요소"라는 의미에서 시작됨.
- 스프링에서는 특별히 **“컨테이너가 관리하는 자바 객체”** 를 의미함.

---

### 3. Bean 등록 방법 (2가지)

#### ✅ (1) 자동 등록 - 어노테이션 사용

```java
@Component   // 일반 컴포넌트
@Service     // 서비스 계층
@Repository  // 데이터 계층
@Controller  // 웹 컨트롤러 계층
```

예:

```java
@Component
public class OrderService {
    ...
}
```

- `@Component`가 붙은 클래스는 스프링이 자동으로 스캔해서 Bean으로 등록함
- 등록된 이름은 클래스명에서 앞글자만 소문자로 바뀜 (orderService)

#### ✅ (2) 수동 등록 - @Configuration + @Bean 사용

```java
@Configuration
public class AppConfig {

    @Bean
    public OrderService orderService() {
        return new OrderService(orderRepository());
    }

    @Bean
    public OrderRepository orderRepository() {
        return new MemoryOrderRepository();
    }
}
```

- 개발자가 직접 Bean 생성 로직을 정의함
    
- 테스트나 명확한 의존성 관리가 필요할 때 사용
    

---

### 4. Bean의 특징

| 특징           | 설명                         |
| ------------ | -------------------------- |
| 스프링이 생성 및 관리 | 개발자가 new로 만들지 않음           |
| 의존성 주입 가능    | 다른 Bean을 주입받을 수 있음 (DI)    |
| [[싱글톤]]이 기본  | 기본 설정에서 Bean은 하나만 생성되어 공유됨 |
| 이름으로 관리 가능   | getBean("이름")으로 꺼낼 수 있음    |

---

### 5. Bean을 꺼내 쓰는 방법 (예시)

```java
ApplicationContext context = SpringApplication.run(MyApp.class, args);

OrderService orderService = context.getBean(OrderService.class);
orderService.placeOrder("사과");
```

- `getBean()` 메서드로 컨테이너에서 Bean을 꺼내 쓸 수 있음
    
- 하지만 보통은 주입(@Autowired, 생성자 주입) 방식으로 사용하는 것이 일반적임
    

---

### 6. 요약

```
📌 Bean이란?
- 스프링 컨테이너가 생성하고 관리하는 객체
- 개발자는 new로 만들지 않고, 스프링이 대신 생성함
- 자동 등록 (@Component 등) 또는 수동 등록 (@Bean) 가능
- IoC/DI 구조에서 중심이 되는 요소
```

---

이제 전체 개념이 완성됐다:

```
Bean → 컨테이너가 관리함 → DI로 주입됨 → 이 모든 제어 흐름이 IoC
```

---

필요하다면 전체 개념 흐름을 한 장의 도식으로 정리해줄 수도 있어.  
혹시 시각적으로 한눈에 정리된 그림이 필요할까?
















EJB -> 객체를 bean이라고 표현 

Hong hong = (Hong)context.getBean("hong");
오브젝트로 받기 때문에 다운캐스팅이 필요함 


xml > constructor-arg 태그


@Autowired ?? 