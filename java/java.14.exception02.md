# TIL - JAVA 책: Java의 신

- **날짜:** 2026-06-03
- **분야:** `개발` 

## 배운 것
자바의 예외 사용 방법 (두 번째)

## 왜 중요한가?
예외를 생각하지 않고는 안전한 프로그램 개발이 쉽지 않다.

# 새롭게 알게 된 정보
1. 모든 예외의 할아버지는 java.lang.Throwable 클래스이다.
2. 예외 발생시키는 throws.
   throw는 try-catch 블록이 있어서 사용한다.
3. 개인이 예외를 만들 수 있다.

## 예제 
1. 모든 예외의 부모는 Throwable

```
java.lang.Throwable                    ← 최상위 부모
   ├─ Error                            ← 시스템 문제 (복구 불가)
   │    ├─ OutOfMemoryError
   │    └─ StackOverflowError
   │
   └─ Exception                        ← 프로그램 문제 (복구 가능)
        ├─ IOException                 ← Checked
        ├─ SQLException                ← Checked
        └─ RuntimeException            ← Unchecked
             ├─ NullPointerException
             ├─ ArrayIndexOutOfBoundsException
             └─ ArithmeticException

```

```
public class Main {
    public static void main(String[] args) {
        try {
            String s = null;
            s.length();
        } catch (Throwable t) {        // 최상위라 뭐든 잡힘
            System.err.println(t.getClass().getSimpleName());
        }
    }
}

------출력------
NullPointerException

```


2. throw vs throws
```
public class Main {
    // throws: 예외를 떠넘긴다고 선언
    static void check(int age) throws Exception {
        if (age < 0) {
            throw new Exception("음수 안 됨");   // throw: 실제로 던짐
        }
    }
    
    public static void main(String[] args) {
        try {
            check(-1);
        } catch (Exception e) {
            System.err.println(e.getMessage());
        }
    }
}

----------------출력------------
음수 안 됨
```


3. 개인이 만든 예외

```
class MyException extends Exception {
    public MyException(String msg) {
        super(msg);
    }
}

public class Main {
    public static void main(String[] args) {
        try {
            throw new MyException("내가 만든 예외");
        } catch (MyException e) {
            System.err.println(e.getMessage());
        }
    }
}

-----------------출력------------
내가 만든 예외

```
## 출처 (14장 다 배운 것 같지만, 예외라는 중요한 것이 있어요.)
