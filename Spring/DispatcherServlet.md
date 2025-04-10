
##  DispatcherServlet의  역할

`DispatcherServlet`은 Spring MVC에서 **프론트 컨트롤러(Front Controller)** 패턴을 구현한 서블릿

> 모든 웹 요청을 가장 먼저 받고,  
> 요청에 따라 어떤 컨트롤러를 호출할지 결정하고,  
> 응답을 어떤 형태로 돌려줄지도 결정하는 중심 역할

---

## 🔍 요청 처리 흐름 예시

예를 들어 브라우저에서 `/members`라는 URL로 요청이 왔다고 가정

### 흐름은 이렇게 돼:

```
1. 클라이언트 → /members 요청
2. DispatcherServlet이 요청 받음
3. HandlerMapping에서 어떤 Controller인지 찾음
4. 해당 Controller 호출
5. Controller가 Model에 데이터 담고 View 이름 리턴
6. ViewResolver가 View 이름으로 실제 뷰(JSP 등) 찾음
7. 최종 결과를 HTML 등으로 렌더링해서 응답
```

---

## ⚙ DispatcherServlet의 주요 구성요소

|구성요소|역할|
|---|---|
|**HandlerMapping**|URL 요청에 맞는 Controller를 찾아줌|
|**HandlerAdapter**|Controller를 실제 실행시켜주는 어댑터|
|**ViewResolver**|Controller가 리턴한 View 이름을 진짜 View 파일(JSP, Thymeleaf 등)로 변환|
|**ModelAndView**|데이터(Model) + View 이름을 함께 담는 객체|

---

## 📁 실무에서 자주 보게 될 설정들

Spring Boot에서는 `DispatcherServlet`이 자동으로 등록되고, `/` 경로로 모든 요청을 받아 처리해줘.  
기본적으로 `application.properties`에서 설정하거나, 커스터마이징도 가능해.

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    // 필요한 설정을 여기에 추가 가능 (인터셉터, 뷰리졸버 등)
}
```

---

## 💡 정리

- ==`DispatcherServlet`은 **Spring MVC의 중심** 역할==
    
- 모든 HTTP 요청을 받아서 적절한 **Controller에 연결하고**,  
    그 결과를 **뷰로 변환해서 응답**까지 책임짐
    
- 이 흐름을 이해하면 Spring MVC 전체 구조가 머릿속에 정리돼
    
---
