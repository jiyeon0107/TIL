# TIL - JAVA 책: Java의 신

- **날짜:** 2026-05-04
- **분야:** `개발` 

## 배운 것
자바의 API

## 왜 중요한가?
자바를 코딩하기 위해서 API 문서보는 방법과 내용을 알아야 하기 때문이다.

## 새롭게 알게 된 정보
1. java.lang.String 같은 표준 라이브러리도 "API"라고 부르는데, 이는 클래스·인터페이스·메서드를 다 포괄하면서 "이렇게 호출하면 이렇게 동작한다"는 약속을 강조하는 표현이다. C++에서는 표준 라이브러리라고 불린다.

2. import는 항상 같은 키워드지만, 뒤에 클래스 이름이 오면 "하나만", *이 오면 "패키지 전체"를 가져오는 거다.

3. Java는 Oracle이 단독으로 관리하기 때문에 docs.oracle.com처럼 공식 표준 API 문서가 한 곳에 깔끔하게 정리되어 있다. 반면 C++은 ISO 표준으로 관리되고, 컴파일러 벤더(GCC, Clang, MSVC)도 여러 개라서 "공식 한 곳"이 없습니다. 표준 문서 자체는 ISO에서 유료로 판매한다.

## 예시 

```
// Java
import java.util.ArrayList;   // C++ <vector>에 해당
// String, System은 import 불필요 (java.lang은 자동)

public class Test {
    public static void main(String[] args) {
        String s = "Hello";
        ArrayList<Integer> v = new ArrayList<>();
        System.out.println(s);
    }
}

```


## 출처
- 자바의 신 (11장. 매번 만들기 귀찮은데 누가 만들어 놓은 거 쓸 수 없나요?)
