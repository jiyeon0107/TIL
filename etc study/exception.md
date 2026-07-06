# TIL - 예외

- **날짜:** 2026-06-05
- **분야:** `멘토링 기록`

## 배운 것
C, C++, java의 예외 사용 방법

## 왜 중요한가?
각 언어별 특징에 따라 예외 또는 오류 처리 방법이 다른 것을 익힌다.

## 예시 (선택)

``` C++
Exception

void a(int x) {
    if (x == 0) 
    {
        // Error
        throw SomeException(); // a함수에서 d함수로 예외를 바로 보낼 수 있다.
    }

    ...
}

void b(int x) {
    a(x);
}

void c(int x){
    b(x);
}

void d(int x) {
    try {
        c(x);
    catch (SomeException e) { //a함수의 예외를 받는다.
        // Log
    }
}

---

C

호출 구조: a<- b <- c<- d

int a(int x) {
    if (x == 0)
        return 0;
    }

    ...

    return 1;
}

int b(int x) {
    return a(x);
}

int c(int x){
    return b(x);
}

void d(int x) {
    int result = c(x);
    if (result == 0) {
        // Log
    }
}

//d에서 예외 또는 오류를 확인하기 위해서 a,b,c의 리턴 타입이 모두 반환형이 같아야 한다.
```

```Java

Exception <-- SomeException <-- AnotherException

public class SomeException extends Exception {
}

public class AnotherException extends SomeException{
}

void a(int x) throws SomeException {
    if (x == 0){
        // Error
        throw SomeException();
    }

    ...
}

void b(int x) throws SomeException {
    a(x);
}

void c(int x) throws SomeException {
    b(x);
}

void d(int x) {
    try {
        c(x);
    }
    catch (Exception e) {
        // Log
    }
}


//마지막으로 받는 d에서 try-catch문으로 받는다.
//중간에 건너는 예외 처리는 throws를 통해 넘겨야 한다.

```
## 출처
- f-lab 멘토링