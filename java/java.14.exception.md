# TIL - JAVA 책: Java의 신

- **날짜:** 2026-06-02
- **분야:** `개발` 

## 배운 것
자바의 예외 사용 방법

## 왜 중요한가?
예외를 생각하지 않고는 안전한 프로그램 개발이 쉽지 않다.

# 새롭게 알게 된 정보
1. 오류가 발생하는 부분에는 System.err를 사용하는 것이 좋다.
2. 먼저 선언한 catch 블록의 예외 클래스가 다음에 선언한 catch 블록의 부모에 속하면, 자식에 속하는 catch 블록은 절대 실행될 일이 없으므로 컴파일되지 않는다.
3. Error는 프로세스에 영향을 주고, Exception은 쓰레드에만 영향을 준다.

## 예제 
1. System.out은 일반 출력, System.err는 에러 출력용 둘다 콘솔에 나오지만 별도의 스트림이라서 구분 처리 가능하다.

```
public class Main{
    public static void main(String[] args){
        int[] arr = {1,2,3}

        try{
            System.out.println("배열 접근 시도"); 
            int value = arr[3];
            System.out.println("값: "+value);
        }catch(ArrayIndexOutOfBoundsException e){
            System.err.println("에러 발생");
        }

        System.out.println("프로그램 계속 진행");
    }
}

-------------------------------------------
//콘솔에서 err은 빨간색 표시
//로그 파일을 분리할 수 있음 (일반 로그와 에러 로그 따로 저장)

배열 접근 시도
에러 발생
프로그램 계속 진행

```



2. 자바의 catch 블록은 위에서 아래로 순서대로 검사한다. 부모 예외를 위에 두면, 자식 예외는 도달 자체가 불가능해서 컴파일러가 막아준다.

```
public class Main {
    public static void main(String[] args) {
        try {
            String s = null;
            s.length();   // NullPointerException 발생
        } catch (Exception e) {                    // ⚠️ 부모를 먼저
            System.err.println("일반 예외: " + e);
        } catch (NullPointerException e) {         // ❌ 자식이 뒤에 — 컴파일 에러!
            System.err.println("Null 예외: " + e);
        }
    }
}

//출력
error: exception NullPointerException has already been caught
```

```
Exception (부모)
   └─ RuntimeException
        └─ NullPointerException (자식)

//Exception이 위에 있으면, NullPointerException도 Exception의 자식이라 첫 번째 catch에서 다 자벼버려요. 두 번째 catch는 영원히 실행될 일이 없어서 이건 dead code라고 막는다.
```

3. Error는 프로세스에 영향, Exception은 쓰레드에 영향

```
Throwable
   ├─ Error          ← 시스템 차원의 심각한 문제 (보통 복구 불가능)
   │    ├─ OutOfMemoryError
   │    ├─ StackOverflowError
   │    └─ ...
   │
   └─ Exception      ← 프로그램 차원의 문제 (보통 복구 가능)
        ├─ IOException
        ├─ NullPointerException
        ├─ ArrayIndexOutOfBoundsException
        └─ ...
```
## 출처 (14장 다 배운 것 같지만, 예외라는 중요한 것이 있어요.)
