# TIL - JAVA 책: Java의 신

- **날짜:** 2026-06-08
- **분야:** `개발` 

## 배운 것
String  클래스

## 왜 중요한가?
자바에서 사용하는 String 클래스는 좀 독특해서 꼭 알아두는 것이 좋다.

# 새롭게 알게 된 정보
[constant pool]
.class 파일 안에 있는 "상수 저장소"이다. 코드에서 쓰는 문자열,숫자,클래스 이름,메서드 이름 같은 걸 한 곳에 모아두고, 바이트코드는 번호로 참조한다. 
<특징>
1. 중복 제거
  같은 문자열을 코드에서 100번 써도, Constant Pool에는 딱 한 번만 저장되도록 되어 있다.
2. 메모리 절약
 문자열, 숫자 같은 걸 매번 따로 저장하지 않고 한 곳에 모아두니까 메모리 효율이 좋다.
3. 빠른 접근
 바이트코드에서 문자열을 직접 쓰는 게 아니라 번호로 참조한다.

<주의>
1. new로 String 객체 만들고 == 비교 시 false가 리턴된다.
2. 변수로 만든 문자열로 == 비교 시 오류가 발생할 수 있으니 .equal()을 권장한다.

## 예제 
<특징>
1. 중복 제거
```java
String a = "Hello";
String b = "Hello";
String c = "Hello";
```
-> Constant Pool에 "Hello"는 한 번만 저장되고, a,b,c는 다 그걸 가리켜요.

2. 빠른 참조

```
책 본문에서: "그 내용은 1장 23절을 참고"
             └─────────┬─────────┘
                  번호로 참조

색인(Constant Pool):
  1장 23절 → 실제 내용
  ...
```

<주의>
1. new로 String 객체 만들고 == 비교 시
```
String a = "Hello";
String b = "Hello";
```

```java
System.out.println(a == b);        // true ⭐ (같은 객체)
System.out.println(a.equals(b));   // true (값도 같음)
```

```java
String a = "Hello";              // String Pool 사용
String b = new String("Hello");  // ⭐ 새 객체 생성, Pool과 별개

System.out.println(a == b);        // false ❌
System.out.println(a.equals(b));   // true ✅
```

2. 변수로 만든 문자열
```java
String a = "Hello";
String b = "Hel" + "lo";          // 리터럴끼리 더하기
String c = "Hel";
String d = c + "lo";              // 변수가 섞이면?

System.out.println(a == b);   // true ⭐
System.out.println(a == d);   // false ❌
```

# String 비교와 String Pool

## 비교표

| 코드 | Pool 사용? | `==` 결과 |
|---|---|---|
| `String a = "Hello"` | ✅ | (Pool에 저장) |
| `String b = "Hello"` | ✅ | `a == b` → **true** |
| `String c = new String("Hello")` | ❌ | `a == c` → **false** |
| `String d = "Hel" + "lo"` | ✅ (컴파일 시 합쳐짐) | `a == d` → **true** |
| `String e = someVar + "lo"` | ❌ (런타임 계산) | `a == e` → **false** |

## 예제 코드

```java
String a = "Hello";
String b = "Hello";
String c = new String("Hello");

System.out.println(a == b);        // true
System.out.println(a == c);        // false
System.out.println(a.equals(c));   // true
```

## 결론

문자열 비교는 항상 `.equals()`를 쓰는 것이 안전하다.
```

## 출처 (15장 String)
