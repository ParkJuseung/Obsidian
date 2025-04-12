
## 🔐 1. **변수에 사용하는 `final`**

### ✅ 의미

- 변수(필드, 지역변수, 매개변수)에 `final`을 붙이면 **값을 한 번만 할당**할 수 있어요.
    
- 즉, **값을 변경할 수 없는 상수**가 됩니다.
    

### 🧪 예시

```java
final int age = 30;
age = 40; // ❌ 컴파일 에러: final 변수는 다시 값을 할당할 수 없음
```

> 단, 객체의 참조는 바꿀 수 없지만, 객체의 내부 상태는 바뀔 수 있어요:

```java
final List<String> list = new ArrayList<>();
list.add("hi");       // ✅ 가능 (내부 상태 변경)
list = new ArrayList<>(); // ❌ 에러 (참조 변경 불가)
```

---

## 🧱 2. **메서드에 사용하는 `final`**

### ✅ 의미

- `final` 메서드는 **오버라이드(재정의) 불가**입니다.
    
- 주로 상속 방지 목적에 사용돼요.
    

### 🧪 예시

```java
class Parent {
    public final void print() {
        System.out.println("Hello");
    }
}

class Child extends Parent {
    // public void print() { } // ❌ 에러! final 메서드는 오버라이드할 수 없음
}
```

---

## 🏰 3. **클래스에 사용하는 `final`**

### ✅ 의미

- `final` 클래스는 **상속이 불가능**합니다.
    
- 예: `String`, `Integer` 같은 Java의 핵심 클래스들.
    

### 🧪 예시

```java
final class Animal {
    // ...
}

// class Dog extends Animal {} // ❌ 에러! final 클래스는 상속 불가
```

---

## ⚠️ 정리하면

|사용 위치|의미|
|---|---|
|변수|값 변경 불가 (한 번만 초기화 가능)|
|메서드|오버라이드 금지|
|클래스|상속 금지|

---

Java에서 `final`은 **불변성(immutability)** 을 지킬 때 아주 중요한 역할을 해요.  
특히 Spring에서는 `final` 필드 + 생성자 주입 (`@RequiredArgsConstructor`) 조합이 널리 쓰이죠.

더 궁금한 거 있나요? `final` 관련해서 언제 쓰면 좋은지도 알려줄 수 있어요! 😊