### HandlerMapping은 왜 안보일까?
`HandlerMapping`은 우리가 직접 만드는 게 아니라,  
Spring이 **시작할 때 내부적으로 빈(bean)으로 자동 등록**해주는 **스프링 컨테이너 속 컴포넌트**야.

그래서 일반적인 프로젝트에서는 `HandlerMapping`이라는 이름을 가진 클래스를  
**직접 만들거나 눈으로 보지 않아도** 동작하는 거야.

## 🔍 예를 들면 이런 클래스들이 있어

Spring 내부에는 실제로 여러 종류의 `HandlerMapping`이 존재해:

|HandlerMapping 구현체|설명|
|---|---|
|`RequestMappingHandlerMapping`|우리가 가장 많이 쓰는 `@RequestMapping` 기반 매핑 담당|
|`SimpleUrlHandlerMapping`|단순한 URL → 핸들러 매핑에 사용|
|`BeanNameUrlHandlerMapping`|빈 이름으로 URL 매핑|

우리가 자주 사용하는 `@Controller`, `@RequestMapping`, `@GetMapping` 같은 애너테이션은  
→ **`RequestMappingHandlerMapping`** 이라는 구현체가 분석해서 처리해줘.

---
## 📍 그럼 어디서 확인할 수 있을까?

만약 확인하고 싶다면,

### 방법 1: 디버깅 or 로그에서 확인

Spring Boot 앱을 실행할 때 `HandlerMapping`이 등록되는 로그가 찍힐 수 있어.

또는, 아래처럼 전체 등록된 핸들러 매핑 빈을 콘솔에 출력할 수도 있어:

```java
@Autowired
private List<HandlerMapping> handlerMappings;

@PostConstruct
public void printHandlerMappings() {
    for (HandlerMapping mapping : handlerMappings) {
        System.out.println("Registered Mapping: " + mapping.getClass().getName());
    }
}

```