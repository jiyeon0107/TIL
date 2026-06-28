# TIL - JAVA 책: Java의 신

- **날짜:** 2026-06-28
- **분야:** `개발` 

## 배운 것
자바의 신 책 이론 점검

## 왜 중요한가?
그 동안 습득한 내용 복습

## 복습한 정보
1. static import 용도
static 멤버를 클래스 이름 없이 쓰게 해주는 import

```java
//일반 import

import java.lang.Math;   // (사실 java.lang은 자동 import이지만 예시로)

public class Test {
    public static void main(String[] args) {
        double result = Math.sqrt(16);    // 클래스 이름 Math가 필요
        double pi = Math.PI;              // 클래스 이름 Math가 필요
    }
}

//static import

import static java.lang.Math.sqrt;
import static java.lang.Math.PI;

public class Test {
    public static void main(String[] args) {
        double result = sqrt(16);    // Math. 없이 바로 호출!
        double pi = PI;              // Math. 없이 바로 사용!
    }
}
```
C++에서 using과 비슷하다.

2. static 변수 static 메소드
- static은 클래스에 하나다. 객체마다 있는 게 아니다.

```java
class Counter {
    int instanceCount = 0;          // 일반 변수 (인스턴스 변수)
    static int staticCount = 0;     // static 변수 (클래스 변수)
    
    void increase() {
        instanceCount++;
        staticCount++;
    }
}

public class Main {
    public static void main(String[] args) {
        Counter c1 = new Counter();
        c1.increase();
        c1.increase();
        c1.increase();
        
        Counter c2 = new Counter();
        c2.increase();
        
        System.out.println(c1.instanceCount);   // 3 (c1 자신의 카운터)
        System.out.println(c2.instanceCount);   // 1 (c2 자신의 카운터)
        
        System.out.println(Counter.staticCount); // 4 (모두가 공유)
    }
}
```
객체 없이도 접근 가능

```java
// 일반 변수 — 객체가 있어야 접근
Counter c = new Counter();
c.instanceCount;       // ✅
// Counter.instanceCount;   // ❌ 컴파일 에러

// static 변수 — 클래스 이름으로 바로 접근
Counter.staticCount;   // ✅ 객체 없이도 OK

```

- static 메서드 안에선 인스턴스 변수 못쓴다.

```java
class Test {
    int x = 10;                    // 인스턴스 변수
    static int y = 20;             // static 변수
    
    static void method() {
        // System.out.println(x);   ❌ 컴파일 에러! 어느 객체의 x?
        System.out.println(y);      // ✅ static끼리는 OK
    }
}

public class Main {
    int x = 10;
    
    public static void main(String[] args) {
        System.out.println(x);   // ❌ 에러!
    }
}
```


3. 인터페이스, abstract 클래스, 클래스, Enum 클래스의 요약

일반 클래스 — 기본
abstract 클래스 — 공통 코드 공유 + 강제 구현
interface — 능력 약속, 여러 개 받기 가능
enum — 정해진 값들

```java
// interface — 능력
interface Walkable {
    void walk();
}

// abstract 클래스 — 정체성 + 공통 코드
abstract class Animal implements Walkable {
    String name;
    
    Animal(String name) { this.name = name; }
    
    void sleep() {                          // 공통 메서드
        System.out.println(name + " 잠");
    }
    
    abstract void cry();                    // 자식이 구현 강제
}

// enum — 정해진 값
enum AnimalMood {
    HAPPY, ANGRY, SAD;
}

// 일반 클래스 — 실제 사용 가능한 객체
class Dog extends Animal {
    AnimalMood mood = AnimalMood.HAPPY;
    
    Dog(String name) { super(name); }
    
    @Override
    void cry() {
        System.out.println(name + " 멍멍");
    }
    
    @Override
    public void walk() {
        System.out.println(name + " 산책");
    }
}

// 사용
public class Main {
    public static void main(String[] args) {
        Dog d = new Dog("뽀삐");
        d.sleep();              // Animal에서 상속
        d.cry();                // Dog에서 구현
        d.walk();               // Walkable 인터페이스 구현
        
        System.out.println(d.mood);   // HAPPY (enum)
    }
}
```


## 출처 (중간 점검)
