# TIL - JAVA 책: Java의 신

- **날짜:** 2026-06-23
- **분야:** `개발` 

## 배운 것
자바의 어노테이션

## 왜 중요한가?
코드에 대한 가독성이 좋아지게 만들 수 있다.
이 코드가 어떻게 다뤄져야 하는지를 표현하는 수단이다.

# 새롭게 알게 된 정보
1. 미리 정해져 있는 어노테이션은 3개뿐이다.
2. @SuppressWarnings 어노테이션 선언과 적용 범위


## 예제 

1. 미리 정해져 있는 어노테이션은 3개
```java
// ① @Override — 부모 메서드를 재정의한다는 표시. 컴파일러가 실제로 재정의인지 검증해줌
class Parent {
    public String hello() { return "hello"; }
}

class Child extends Parent {
    @Override
    public String hello() { return "hi"; }  // OK

    @Override
    public String wrongName() { return "hi"; }  // 컴파일 에러! 부모에 없는 메서드
}

// ② @Deprecated — 더 이상 쓰지 말라는 표시. 이 메서드를 호출하면 컴파일러가 경고를 띄움
class OldApi {
    @Deprecated
    public void oldMethod() {
        System.out.println("구버전 메서드");
    }

    public void newMethod() {
        System.out.println("신버전 메서드");
    }
}

// ③ @SuppressWarnings — 컴파일러 경고를 억제함
class Example {
    @SuppressWarnings("deprecation")
    public void useOldApi() {
        OldApi api = new OldApi();
        api.oldMethod();  // @Deprecated 메서드 호출이지만 경고 안 뜸
    }
}
```
2. @SuppressWarnings 선언 위치에 따른 적용 범위

```java
@SuppressWarnings("unchecked")   // ① 클래스 전체에 적용 — 모든 메서드, 필드 다 억제됨
public class ScopeExample {

    @SuppressWarnings("deprecation")  // ② 이 필드 선언에만 적용
    private OldApi fieldApi = new OldApi();

    // ③ 아무것도 안 붙인 메서드 — 클래스 레벨 ①의 "unchecked"는 여기도 적용됨
    public void methodA() {
        List list = new ArrayList();             // unchecked 경고 억제됨 (①때문에)
        OldApi api = new OldApi();
        api.oldMethod();                         // deprecation 경고는 여기선 뜸!
    }

    @SuppressWarnings("deprecation")  // ④ 이 메서드 안에만 적용
    public void methodB() {
        List list = new ArrayList();             // unchecked 경고 억제됨 (①때문에)
        OldApi api = new OldApi();
        api.oldMethod();                         // deprecation 경고도 억제됨 (④때문에)
    }

    public void methodC() {
        @SuppressWarnings("deprecation")         // ⑤ 이 지역변수 선언 부분에만 적용
        OldApi localApi = new OldApi();          // deprecation 경고 억제됨
        localApi.oldMethod();                    // 여기선 이미 억제 범위 벗어나서 경고 뜸!
    }
}
```
실무에서는 클래스 전체에 붙이는 건 피하고, 가능한 한 좁은 범위에 붙이는 게 권장된다.

## 출처 (17장. 어노테이션이라는 것도 알아야 한다.)
