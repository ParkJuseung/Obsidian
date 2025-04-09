#### 정의
스프링 컨테이너는 스프링 프레임워크의 핵심 구성 요소로, 애플리케이션에서 사용하는 객체(Bean)을 생성하고, 관리하고, 의존성을 주입하는 주체이다.
즉, IoC와 DI를 실제로 구현하고 실행하는 존재이다.

#### 주요 역할
- 객체 생성    : 클래스 인스턴스를 직접 생성함 (new 안씀)
- 객체 관리    : 생성한 객체들을 메모리에 보관하고 관리
- 의존성 주입 : 생성자 또는 필드 등을 통해 필요한 의존성을 주입
- 라이프 사이클 관리 : 객체 생성, 초기화, 소멸까지 생명 주기 관리

#### 3. 컨테이너의 종류

스프링에는 다양한 컨테이너가 존재하지만, 가장 많이 사용하는 건 다음 두 가지다.

|컨테이너 종류|설명|
|---|---|
|**ApplicationContext**|가장 일반적인 컨테이너. 실무에서 주로 사용됨|
|**BeanFactory**|ApplicationContext의 상위 인터페이스. 기본 기능만 제공|

→ 대부분의 경우 **ApplicationContext를 사용**하면 된다.


#### 4. 동작 흐름
>[!tip]
>1. 애플리케이션 실행 (SpringApplication.run)
>2. 컨테이너가 시작됨
>3. @ComponentScan으로 클래스들을 스캔
>4. @Component, @Service, @Repository 등을 가진 클래스들을 찾아 Bean 등록
>5. 객체를 생성하고, 필요하면 DI 수행
>6. 컨테이너는 Bean들을 내부에서 관리함



#### 5. 예제 코드
```java
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        ApplicationContext context = SpringApplication.run(MyApp.class, args);

        OrderService orderService = context.getBean(OrderService.class);
        orderService.placeOrder("사과");
    }
}

```
- `SpringApplication.run()` → 스프링 컨테이너(ApplicationContext)를 생성하고 실행
- `getBean()` → 컨테이너에서 필요한 Bean을 꺼내서 사용


#### 6. 요약 
스프링 컨테이너란?
 - 객체를 생성하고, 의존성을 주입하고, 생명 주기를 관리하는 주체
 - 스프링에서 IoC와 DI를 실현하는 핵심 시스템
 - 대표 컨테이너는 ApplicationContext

