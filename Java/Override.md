
## 🔁 **Override란?**

**부모 클래스(또는 인터페이스)의 메서드를 자식 클래스에서 다시 정의하는 것**을 말해요.

즉, 이미 존재하는 메서드를 **재정의(override)** 해서 **자식 클래스의 동작을 바꾸는 것**입니다.

---

## 💡 왜 쓰는 걸까?

- 상속받은 메서드의 **기본 동작을 바꾸고 싶을 때**
    
- **다형성(polymorphism)** 을 위해 필요해요.
    

---

## ✅ 예시

```java
class Animal {
    public void sound() {
        System.out.println("동물이 소리를 낸다");
    }
}

class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("멍멍!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.sound(); // 👉 "멍멍!" 출력 (Dog의 메서드가 실행됨)
    }
}
```

### 🔎 설명:

- `Dog` 클래스가 `Animal`의 `sound()` 메서드를 **override** 했어요.
    
- 부모 클래스에는 `"동물이 소리를 낸다"`가 있지만,
    
- 자식 클래스인 `Dog`는 `"멍멍!"`으로 바꿔서 실행돼요.
    

---

## 🧷 @Override 어노테이션

```java
@Override
public void sound() { ... }
```

- 꼭 안 써도 되지만, **쓰는 걸 강력히 추천**해요!
    
- 부모 클래스에 없는 메서드를 실수로 오버라이드하려고 하면 **컴파일 에러**가 납니다.
    
- 예) 오타, 메서드 시그니처 불일치 등 실수 방지
    

---

## 🚫 오버라이드가 안 되는 경우

- 메서드가 `final`이면 오버라이드 불가능
    
- `private`이나 `static` 메서드도 오버라이드 불가능
    

---

## 🔄 오버로딩(Overloading)과 헷갈리지 마세요!

- **오버라이드**: 상속받은 메서드 이름을 **같이 쓰면서 구현을 바꿈**
    
- **오버로딩**: 같은 이름의 메서드를 **매개변수 다르게 해서 여러 개 정의**
    

필요하면 이것도 자세히 알려드릴게요 😄

---

궁금한 부분 더 있나요? 예제 더 보고 싶으면 말해줘요!