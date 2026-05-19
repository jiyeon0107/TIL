# TIL - JAVA 책: Java의 신

- **날짜:** 2026-05-19
- **분야:** `개발` 

## 배운 것
interface와 abstract

## 왜 중요한가?
프로그램의 규모가 커지면 협업하기 위해서 공통적인 부분을 미리 선언하여 사용하기 위해서 중요하다.

# 새롭게 알게 된 정보
 interface vs abstract

## 공통점

- 둘 다 `*.java` 파일로 작성한다.
- 직접 객체 생성이 불가능하다. (반드시 구현/상속하는 클래스가 필요)
- 자식 클래스에게 특정 메서드 구현을 강제할 수 있다.

## 차이점

| 항목 | interface | abstract class |
|---|---|---|
| 메서드 구현 | 선언만 (default 메서드는 예외) | 선언 + 구현 모두 가능 |
| 사용 키워드 | `implements` | `extends` |
| 다중 적용 | 여러 개 가능 | 1개만 가능 |
| 의미 | "~할 수 있다" (능력) | "~이다" (정체성) |

---

## 예제 1: interface 여러 개 구현 + abstract 단일 상속

```java
// abstract 클래스 — 하나만 상속 가능
abstract class Animal {
    String name;

    Animal(String name) { this.name = name; }

    void sleep() {                      // 구현된 메서드
        System.out.println(name + " 잠");
    }

    abstract void cry();                // 선언만 (자식이 구현 강제)
}

// interface — 여러 개 구현 가능
interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

// Duck은 Animal을 상속받으면서, Flyable과 Swimmable 둘 다 구현
class Duck extends Animal implements Flyable, Swimmable {
    Duck(String name) { super(name); }

    @Override
    void cry() { System.out.println(name + " 꽥꽥"); }

    @Override
    public void fly() { System.out.println(name + " 날아간다"); }

    @Override
    public void swim() { System.out.println(name + " 헤엄친다"); }
}

public class Main {
    public static void main(String[] args) {
        Duck duck = new Duck("도널드");
        duck.sleep();   // Animal에서 상속받은 메서드
        duck.cry();     // Animal에서 강제한 메서드
        duck.fly();     // Flyable에서 강제한 메서드
        duck.swim();    // Swimmable에서 강제한 메서드
    }
}
```

**출력 결과**

```
도널드 잠
도널드 꽥꽥
도널드 날아간다
도널드 헤엄친다
```

**포인트**: `extends Animal`은 하나만, `implements Flyable, Swimmable`은 여러 개 가능하다.

---

## final 키워드

`final`은 "더 이상 바꿀 수 없다"는 의미의 예약어이다. 사용 위치에 따라 효과가 다르다.

| 사용 위치 | 효과 |
|---|---|
| 클래스 | 상속 불가 |
| 메서드 | 오버라이딩 불가 |
| 기본형 변수 | 값 변경 불가 |
| 참조형 변수 | 다른 객체로 재할당 불가 (단, 객체 내용은 변경 가능) |

## 예제 2: final 키워드 4가지 용법

```java
// 1. final 클래스 → 상속 불가
final class FinalClass {
    void hello() { System.out.println("hello"); }
}

// class SubClass extends FinalClass { }  // ❌ 컴파일 에러

// 2. final 메서드 → 오버라이딩 불가
class Parent {
    final void greet() { System.out.println("안녕"); }
}

class Child extends Parent {
    // @Override
    // void greet() { ... }   // ❌ 컴파일 에러
}

// 3. final 변수 → 값 변경 불가 (상수)
class Constants {
    static final int MAX_AGE = 150;

    void test() {
        // MAX_AGE = 200;   // ❌ 컴파일 에러
        final int x = 10;
        // x = 20;          // ❌ 컴파일 에러
    }
}

// 4. final 참조 변수 → 재할당 불가 (단, 내용은 변경 가능)
public class Main {
    public static void main(String[] args) {
        final StringBuilder sb = new StringBuilder("Hello");

        sb.append(", Java!");           // ✅ 내용 변경 OK
        System.out.println(sb);         // Hello, Java!

        // sb = new StringBuilder();    // ❌ 재할당은 불가
    }
}
```

**출력 결과**

```
Hello, Java!
```



## 출처
- 자바의 신 (13장. 인터페이스와추상클래스, enum), 클로드 
