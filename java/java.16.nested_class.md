# TIL - JAVA 책: Java의 신

- **날짜:** 2026-06-18
- **분야:** `개발` 

## 배운 것
내부 클래스는 코드를 간단히 하기 위해 사용한다.

## 왜 중요한가?
자바 기반의 UI 처리를 할 때 사용자의 입력이나, 외부의 이벤트에 대한 처리를 하는 곳에서 많이 사용할 수 있다.

# 새롭게 알게 된 정보
1. 겉으로 보이에는 유사하지만, 내부적으로 구현이 달라야 할 때 static nested 클래스를 사용한다.
2. Inner 클래스를 생성하기 전에는 먼저 Inner 클래스를 감싸고 있는 외부 클래스를 객체를 만들어야 한다.
3. 버튼이 눌렀을 때 작동하는 방식으로 익명 클래스를 활용한다.

## 예제 
1. static nested 클래스
학교를 관리하는 School 클래스, 대학을 관리하는 University 클래스가 있을 때 Student 클래스 만들 경우 School의 학생인지 University의 학생인지가 불분명할 때 School과 University 클래스 내부에 각각의 Student 내부 클래스를 만들어 사용한다.

2. Inner 클래스 생성 - 외부 객체가 먼저 필요

```java
class Outer {
    private String name = "외부 클래스";
    
    class Inner {                    // static 없음 — 인스턴스 내부 클래스
        void show() {
            System.out.println("외부의 이름: " + name);   // 외부 필드 접근
        }
    }
}

public class Main {
    public static void main(String[] args) {
        // ❌ 이렇게는 안 됨 — 컴파일 에러
        // Outer.Inner inner = new Outer.Inner();
        
        // ✅ 외부 인스턴스를 먼저 만들어야 함
        Outer outer = new Outer();                    // 1단계: 외부 객체 생성
        Outer.Inner inner = outer.new Inner();        // 2단계: 외부 객체를 통해 내부 객체 생성
        
        inner.show();
    }
}
```
3. 익명 클래스 

```java
interface ClickListener {
    void onClick();
}

class Button {
    private String name;
    private ClickListener listener;
    
    public Button(String name) {
        this.name = name;
    }
    
    public void setClickListener(ClickListener listener) {
        this.listener = listener;
    }
    
    public void click() {                            // 버튼이 눌리면
        System.out.println("[" + name + " 버튼 눌림]");
        if (listener != null) listener.onClick();    // 등록된 동작 실행
    }
}

public class Main {
    public static void main(String[] args) {
        Button saveBtn = new Button("저장");
        
        // 익명 클래스 — 이름 없이 인터페이스 구현하면서 객체 생성
        saveBtn.setClickListener(new ClickListener() {
            @Override
            public void onClick() {
                System.out.println("→ 파일을 저장합니다");
            }
        });
        
        Button deleteBtn = new Button("삭제");
        saveBtn.setClickListener(new ClickListener() {
            @Override
            public void onClick() {
                System.out.println("→ 파일을 삭제합니다");
            }
        });
        
        saveBtn.click();
        deleteBtn.click();
    }
}
```

## 출처 (16장 클래스 안에 클래스가 들어갈 수도 있구나)
