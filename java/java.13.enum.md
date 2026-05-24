# TIL - JAVA 책: Java의 신

- **날짜:** 2026-05-23
- **분야:** `개발` 

## 배운 것
enum 클래스

## 왜 중요한가?
"버그를 사전에 차단하는 안전장치" 

# 새롭게 알게 된 정보
- c++의 enum과 달리 클래스로 사용되어 메소드를 쓸 수 있고 출력시 enum의 이름과 값이 따로 출력 가능하다.
- enum 클래스의 생성자는 아무것도 명시하지 않는 package-private와 private만 접근 제어자로 사용할 수 있다.
- 누가 만들어 놓은 enum을 extends를 이용하여 선언할 수는 없다.


## 예제 

```
public enum Pizza {
    SMALL(8000),
    MEDIUM(12000),
    LARGE(16000);
    
    private final int price;
    
    Pizza(int price) {
        this.price = price;
    }
    
    public int getPrice() {
        return price;
    }
}

public class Main {
    public static void main(String[] args) {
        Pizza p = Pizza.MEDIUM;
        
        // 이름 출력
        System.out.println(p.name());        // MEDIUM
        
        // 값 출력
        System.out.println(p.getPrice());    // 12000
        
        // 같이 출력
        System.out.println(p.name() + ": " + p.getPrice() + "원");
        
        // 전체 메뉴 순회
        for (Pizza pizza : Pizza.values()) {
            System.out.println(pizza.name() + " - " + pizza.getPrice());
        }
    }
}
```

```
출력

MEDIUM
12000
MEDIUM: 12000원
SMALL - 8000
MEDIUM - 12000
LARGE - 16000
```

## 출처
- 자바의 신 (13장. 인터페이스와추상클래스, enum), 클로드 
