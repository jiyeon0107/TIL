# TIL - JAVA 책: Java의 신

- **날짜:** 2026-06-10
- **분야:** `개발` 

## 배운 것
String  클래스 사용 시 주의 사항

## 왜 중요한가?
String 클래스를 잘 사용해야만 메모리를 효율적으로 사용할 수 있고, 적절한 클래스를 선택할 수 있기 때문이다.

# 새롭게 알게 된 정보
1. String의 intern()함수를 사용하지 말자.
2. String 문자열을 더하면 새로운 String 객체가 생성되고, 기존 객체는 버려진다. 
3. StringBuffer와 StringBuilder 클래스는 문자열을 더하더라도 새로운 객체를 생성하지 않는다.
4. StringBuffer와 StringBuilder, CharSequence 타입은 CharSequence 타입으로 받는 것이 좋다. 

## 예제 
1. intern() 사용 하지 않는 이유
 intern() 메소드는 Constrain Pool에 임의의 문자열을 강제로 추가하거나, 이미 있으면 그걸 가져오는 메서드이다.

 ```java
 String a = new String("Hello");   // Heap에 새 객체 생성 (Pool 안 씀)
String b = a.intern();             // Pool에 있는 "Hello"를 가져옴
String c = "Hello";                // Pool 사용

System.out.println(a == b);   // false (a는 Heap, b는 Pool)
System.out.println(b == c);   // true ⭐ (둘 다 Pool의 같은 객체)
 ```

이론적으로는 그럴 싸해보이지만, 실제로는 메모리 문제를 일으킬 소지가 많아서 사용하지 않는 것을 권장한다.

2. String 문자열을 더하면 새로운 String 객체가 생성되고, 기존 객체는 버려진다. 
 String은 불변이라서 한번 만들어지면 절대 안바뀐다.
 
```java
String result = "";
for (int i = 0; i < 1000; i++) {
    result += i;   // ⚠️ 매번 새 객체 생성!
}
```
이 코드는 1000개의 String 객체를 만들고 999개를 버린다.
 <결론>
 짤은 문자열 합치기는 +를 써도 되지만, 반복문이나 많은 문자열 합치기엔 절대 + 쓰지 마세요.

3. StringBuffer와 StringBuilder는 새 객체를 만들지 않는다
  String의 단점을 해결하기 위해 자바는 수정 가능한 문자열 클래스를 제공한다.

4. CharSequence 타입으로 받는 것이 좋다.
CharSequence가 뭐냐면
String, StringBuilder, StringBuffer가 공통으로 구현하는 인터페이스이다.

```java
CharSequence (인터페이스)
   ├─ String
   ├─ StringBuilder
   └─ StringBuffer
```

다형성의 좋은 예시이다.

# 결론
String은 불변이다. ->+ 연산이 비효율적->파생 클래스 생성(StringBuilder)-> CharSequence로 묶여서 유연하게 받는다.

## 출처 (15장 String)
