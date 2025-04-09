

### 1. 정의

**인터페이스는 클래스가 구현해야 할 동작(메서드)의 집합을 정의한 틀이다.**  
즉, **어떤 기능을 제공해야 한다는 "약속"만 정하고, 구현은 하지 않는다.**

---

### 2. 문법 구조

```java
public interface Animal {
    void sound();  // 추상 메서드 (구현 없음)
}
```

→ 이 인터페이스를 사용하는 클래스는 반드시 `sound()` 메서드를 **구현**해야 한다.

```java
public class Dog implements Animal {
    @Override
    public void sound() {
        System.out.println("멍멍");
    }
}
```

---

### 3. 왜 사용하는가? (인터페이스의 목적)

|목적|설명|
|---|---|
|유연성|구현체를 쉽게 바꿀 수 있음|
|확장성|새로운 기능을 추가해도 기존 코드를 건드리지 않음|
|결합도 낮춤|인터페이스에 의존하고, 구현은 바꿔치기 가능|
|테스트 용이|가짜(Mock) 구현체를 만들어 테스트 가능|

---

### 4. 인터페이스와 클래스의 차이점

|구분|클래스|인터페이스|
|---|---|---|
|상태|필드(변수) 가질 수 있음|상태 없음 (상수만 선언 가능)|
|메서드|구현 포함 가능|기본적으로 구현 없음 (Java 8부터 default 가능)|
|상속|하나의 클래스만 상속 가능|여러 인터페이스 구현 가능|

---

### 5. 스프링에서의 활용 예

스프링에서는 인터페이스를 적극적으로 사용해서 **DI(의존성 주입)** 을 구현한다.

```java
public interface OrderRepository {
    void save(String order);
}
```

```java
@Repository
public class MemoryOrderRepository implements OrderRepository {
    @Override
    public void save(String order) {
        System.out.println("메모리에 저장: " + order);
    }
}
```

```java
@Service
public class OrderService {
    private final OrderRepository orderRepository;

    public OrderService(OrderRepository orderRepository) {
        this.orderRepository = orderRepository;
    }
}
```

→ `OrderService`는 인터페이스만 보고 코딩했기 때문에,  
→ 구현체만 바꾸면 유닛 테스트, DB 변경 등 다양한 상황에 쉽게 대응할 수 있음.

---

### 6. Java 8 이후 변화

자바 8부터 인터페이스에도 일부 **구현이 가능**해졌다.

```java
public interface Animal {
    default void breathe() {
        System.out.println("숨을 쉰다");
    }
}
```

- `default` 메서드: 구현 포함 가능 (오버라이딩 선택)
    
- `static` 메서드: 인터페이스 이름으로 호출 가능
    

---

### 7. 요약

```
📌 자바 인터페이스란?
- 메서드 시그니처만 정의하고, 구현은 하지 않는 추상적인 타입
- 다형성을 이용한 설계, 유연하고 확장 가능한 구조를 만들 수 있음
- 구현체를 교체해도 사용 코드는 그대로 유지됨
- 스프링에서는 의존성 주입을 위해 인터페이스가 매우 자주 사용됨
```


