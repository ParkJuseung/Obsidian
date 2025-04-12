
### 1. 사용자 요청 단계

1. **사용자 요청**: 브라우저에서 URL을 통해 요청 (예: `/m2.do?seq=1`)
2. **[[DispatcherServlet]]** : 모든 요청을 가장 먼저 받는 프론트 컨트롤러로, `web.xml`이나 Java 구성을 통해 매핑됨

### 2. 컨트롤러 처리 단계
1. **[[HandlerMapping]]**: 요청 URL을 분석하여 적절한 컨트롤러 메서드를 결정
2. **컨트롤러 실행**: `@GetMapping`이나 `@PostMapping` 등 어노테이션으로 정의된 메서드가 실행됨
   지금까지 확인한 정보를 바탕으로 Spring MVC + MyBatis + JSP 구조에서의 데이터 흐름을 자세히 설명해 드리겠습니다.

# Spring MVC + MyBatis + JSP 구조에서의 데이터 흐름

## 1. 사용자 요청 단계

사용자가 웹 브라우저를 통해 URL로 요청을 보내면 다음과 같은 순서로 데이터가 흐릅니다:

### 1) 클라이언트 요청

- 사용자가 브라우저에서 URL을 입력하거나 링크를 클릭합니다 (예: `http://localhost:8080/m2.do?seq=5`)
- HTTP 요청이 서버로 전송됩니다.

### 2) DispatcherServlet

- Spring MVC의 핵심 컴포넌트인 **DispatcherServlet**이 모든 요청을 가장 먼저 받습니다.
- web.xml에 정의된 URL 패턴에 따라 요청을 받아들입니다.
- 이 서블릿이 프론트 컨트롤러(Front Controller) 역할을 담당합니다.

### 3) HandlerMapping

- DispatcherServlet은 **HandlerMapping**을 통해 요청 URL에 매핑된 컨트롤러를 찾습니다.
- `@GetMapping`, `@PostMapping` 등의 어노테이션이 있는 메서드를 찾습니다.

## 2. 컨트롤러 처리 단계

### 4) 컨트롤러 실행

- 위 코드에서는 `MyBatisController` 클래스의 메서드가 실행됩니다.
- 예를 들어 `/m2.do?seq=5` 요청이 들어오면:

```java

	@GetMapping(value="/m2.do")
	public String m2(Model model, String seq) {    
		int result = this.dao.m2(seq);    
		model.addAttribute("result", result);    
		return "result";}
```

- 파라미터 값(`seq=5`)이 자동으로 메서드 파라미터에 바인딩됩니다.
- `@RequiredArgsConstructor`를 통해 MyBatisDAO가 자동 주입됩니다.

### 5) 서비스 계층 (선택적)

- 일반적으로 컨트롤러와 DAO 사이에 서비스 계층이 존재합니다.
- 예제 코드에서는 서비스 계층이 생략되었으나, 실제 프로젝트에서는 비즈니스 로직을 처리합니다.

## 3. MyBatis 처리 단계

### 6) DAO 호출

- 컨트롤러는 `MyBatisDAO` 인터페이스의 메서드를 호출합니다.
- `private final MyBatisDAO dao;`를 통해 주입된 객체를 사용합니다.

### 7) MyBatis Mapper 실행

- `MyBatisDAOImpl` 클래스가 `MyBatisDAO` 인터페이스를 구현합니다.
- DAO 구현체는 SQL 문을 실행하기 위해 MyBatis의 **SqlSession**을 사용합니다.
- XML Mapper 파일에 정의된 SQL문을 실행합니다 (예: mapper.xml).

### 8) 데이터베이스 작업

- MyBatis가 PreparedStatement를 생성하고 [^1]파라미터를 바인딩합니다.
- 데이터베이스에 쿼리를 실행하고 결과를 받아옵니다.
- MyBatis는 결과를 자동으로 Java 객체(DTO)로 매핑합니다.

## 4. 결과 처리 단계

### 9) 결과 반환

- 데이터베이스 작업 결과가 DAO를 통해 컨트롤러로 반환됩니다.
- 컨트롤러는 결과 데이터를 Model 객체에 추가합니다:

```
model.addAttribute("result", result);
```

### 10) 뷰 이름 반환

- 컨트롤러는 논리적 뷰 이름을 반환합니다 (예: `return "result";`).
- DispatcherServlet은 ViewResolver를 통해 논리적 뷰 이름을 실제 JSP 파일 경로로 변환합니다.

## 5. 응답 생성 단계

### 11) JSP 처리

- ViewResolver는 `result`라는 논리적 뷰 이름을 `/WEB-INF/views/result.jsp`와 같은 실제 경로로 변환합니다.
- JSP가 실행되고, 모델에 담긴 데이터에 접근합니다 (예: `${result}`).
- JSTL과 EL(Expression Language)을 사용하여 동적 콘텐츠를 생성합니다.

### 12) 응답 전송

- 생성된 HTML이 HTTP 응답으로 클라이언트(브라우저)에게 전송됩니다.
- 브라우저는 받은 HTML을 렌더링하여 사용자에게 보여줍니다.

## 예시 시나리오 (m2.do 요청 흐름)

1. 사용자가 `http://localhost:8080/m2.do?seq=5` 접속
2. DispatcherServlet이 요청 수신
3. `/m2.do` URL에 매핑된 `MyBatisController.m2()` 메서드 호출
4. 파라미터 `seq=5`가 메서드의 `String seq` 파라미터에 바인딩
5. `dao.m2(seq)` 호출하여 MyBatis를 통해 DB 작업 수행
6. 작업 결과를 `model.addAttribute("result", result)`로 모델에 저장
7. `return "result"`로 뷰 이름 반환
8. ViewResolver가 `result.jsp` 파일 찾기
9. JSP에서 `${result}` 등으로 모델 데이터 사용하여 HTML 생성
10. 생성된 HTML이 클라이언트에게 반환되어 화면에 표시

이러한 구조는 관심사의 분리(Separation of Concerns)를 통해 유지보수가 용이하고 확장성이 높은 웹 애플리케이션을 개발할 수 있게 해줍니다.

[^1]: #{}, ${}자리에 값을 끼워넣는 것  
