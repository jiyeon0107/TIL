# TIL - JAVA 책: Java의 신

- **날짜:** 2026-06-22
- **분야:** `개발` 

## 배운 것
내부 클래스 공부하면서 궁금한 것 추가 공부.
1. 내부 클래스 필요 이유
2. 상속 포함 관계 구별
3. 자바는 함수 포인터를 만들지 않은 이유

## 왜 중요한가?
개발 언어 감각을 익히는 데 중요.

# 새롭게 알게 된 정보 (내가 이해한 내용)
1. 자바의 내부 클래스 필요 이유.
: 자바에서 초반에는 내부 클래스를 만들지 않았다. 하지만 이벤트 핸들러를 다루기 위해서 내부 클래스를 활용하여 만들었다. MFC는 콜백 함수를 통해 이벤트 핸들러의 함수 포인터로 접근하지만 자바는 함수 포인터 개념이 없기에 이벤트 핸들러를 통해 객체를 넘겨 객체의 함수를 통해 이벤트(버튼 클릭 등)을 사용한다.

2. 상속 포함 관계 구별
: 내부 클래스와 외부 클래스의 private에 접근할 수 있기 때문에 그냥 보면 부모 자식 사이라고 오해할 수 있지만 내부 클래스는 외부 클래스의 멤버이다. 상속은 extends를 활용하여 클래스에 선언되어야지만 자식이라고 할 수 있다. 

3. 자바는 함수 포인터를 만들지 않은 이유
: 자바는 객체 지향이라는 가장 큰 맥락으로 사용하기 때문에 C++ 기반에서 사용하는 함수 포인터는 객체 안에서 사용하지 않는 부분이라고 보았기에 처음부터 함수 포인터를 만들지 않았다. 그러나 그와 달리 함수포인터가 필요한 부분들이 생겨서 내부 클래스가 생기고 이후 람다라는 문법이 생성되었다. 결국에는 후에 함수 포인터를 인정하였지만 객체로 감싸서 해결했다.

4. 자바의 익명 클래스와 람다 문법
: 자바의 익명 클래스를 사용하면 new 인터페이스(), @Override, 메서드 시그니처(public void onClick()) 등을 다 표현해야 하지만 람다는 한 줄에 함수 포인터처럼 보이도록 표현할 수 있고 간단해서 JAVA8 이후에 추가된 이후로 익명 클래스보다 람다를 더 많이 사용한다. 하지만 람다가 익명 클래스를 대체"는 아니다. 람다는 함수형 인터페이스(추상 메서드 딱 1개)일 때만 쓸 수 있다.

## 예제 (claude 설명)
1. 내부 클래스가 왜 필요했나 — 이벤트 핸들러

```java
// 버튼이 요구하는 규격(인터페이스)
interface ClickListener {
    void onClick();
}

class Button {
    private ClickListener listener;

    void setListener(ClickListener l) {  // 함수가 아니라 '객체'를 받는다
        this.listener = l;
    }

    void click() {
        if (listener != null) listener.onClick();  // 넘겨받은 객체의 메서드 호출
    }
}

class LoginScreen {
    private int clickCount = 0;  // private!

    void init() {
        Button button = new Button();
        button.setListener(new Handler());  // 내부 클래스 인스턴스를 넘김
    }

    // 내부 클래스: 외부의 private에 자유롭게 접근
    class Handler implements ClickListener {
        @Override
        public void onClick() {
            clickCount++;  // 외부 클래스의 private 멤버 직접 접근
            System.out.println("클릭 횟수: " + clickCount);
        }
    }
}
```
내부 클래스 private int clickCount에 자유롭게 접근할 수 있는 게 핵심

2. 상속 vs 포함 — 같아 보이지만 완전히 다름
```java
// (A) 포함: 내부 클래스. extends 없음. 그냥 멤버.
class Outer {
    private int secret = 42;
    class Inner {
        void show() {
            System.out.println(secret);  // 외부 private 접근 가능
        }
    }
}

// (B) 상속: extends가 있어야만 '자식'
class Parent {
    protected int value = 10;
}
class Child extends Parent {   // ← 이게 있어야 상속
    void show() {
        System.out.println(value);  // 부모 protected 상속받아 사용
    }
}
```

3. 함수 포인터의 빈자리 → 익명 클래스 → 람다 (진화사)
```java
Button button = new Button();

// (1) 익명 클래스 — 이름 없는 일회용 내부 클래스 (Java 1.1)
button.setListener(new ClickListener() {
    @Override
    public void onClick() {
        System.out.println("클릭!");
    }
});

// (2) 람다 — 메서드 하나짜리 인터페이스면 본문만 (Java 8)
button.setListener(() -> System.out.println("클릭!"));
```

4. 익명 클래스 vs 람다 — 같은 일, 다른 문법
```java
// 익명 클래스 — 형식을 다 갖춰야 한다
button.setListener(new ClickListener() {   // new + 인터페이스 이름
    @Override
    public void onClick() {                 // 메서드 시그니처 전부 명시
        System.out.println("클릭!");
    }
});

// 람다 — 본문만 남긴다
button.setListener(() -> System.out.println("클릭!"));
```

```java
// (A) 메서드가 2개 이상 → 람다 불가, 익명 클래스만 가능
interface Worker {
    void start();
    void stop();
}
Worker w = new Worker() {        // 람다로는 못 줄임
    @Override public void start() { System.out.println("시작"); }
    @Override public void stop()  { System.out.println("정지"); }
};

// (B) 상태(필드)를 들고 있어야 함 → 익명 클래스
button.setListener(new ClickListener() {
    private int count = 0;       // 람다는 이런 필드를 못 가짐
    @Override public void onClick() {
        count++;
        System.out.println(count + "번째");
    }
});
```

this의 의미가 익명 클래스, 람다에서 다르다.
```java
class Screen {
    String name = "메인화면";

    void test() {
        // 익명 클래스: this = 익명 클래스 인스턴스 자신
        button.setListener(new ClickListener() {
            @Override public void onClick() {
                // 여기서 this는 이 익명 객체. Screen.this로 써야 외부 접근
                System.out.println(Screen.this.name);
            }
        });

        // 람다: this = 바깥(Screen)을 그대로 가리킴
        button.setListener(() -> System.out.println(this.name));  // 바로 name 접근
    }
}
```


## 출처 (16장 클래스 안에 클래스가 들어갈 수도 있구나), claude와의 대화
