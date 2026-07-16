# TIL - JAVA 책: Java의 신

- **날짜:** 2026-07-15
- **분야:** `개발` 

## 배운 것
Java의 java.lang

## 왜 중요한가?
가장 많이 쓰이기 때문에 중요하다.

## 새롭게 알게 된 내용
1. java.lang 패키지에 있는 클래스들은 import를 안해도 사용 가능
2. 각종 정보를 확인하기 위한 System 클래스
 - 생성자가 없다.
 - GC 수행과 JVM 종료 관련 메소드는 사용 금지


1. java.lang 패키지는 import가 필요 없다

String, Object, Math, System 등 java.lang 패키지에 속한 클래스는 모든 자바 프로그램에 기본으로 import되어 있다. 그래서 import java.lang.System; 같은 코드를 따로 작성하지 않아도 바로 사용할 수 있다.
반면 java.util.Scanner, java.util.ArrayList 같은 다른 패키지의 클래스는 명시적으로 import를 해줘야 한다.

2. System 클래스

시스템(운영체제, JVM, 하드웨어 등)과 관련된 정보를 다루는 클래스. 표준 입출력(System.in, System.out, System.err), 현재 시간(System.currentTimeMillis()), 환경변수(System.getenv()) 등을 제공한다.

- 생성자가 없다
    System 클래스의 생성자는 private으로 선언되어 있어서 외부에서 new System()으로 인스턴스를 만들 수 없다.
    모든 멤버가 static이라 애초에 인스턴스가 필요 없는 구조.
    시스템 정보/기능은 프로그램에 딱 하나만 있으면 되고 굳이 여러 개의 System 객체를 만들 이유가 없으니까, 아예 인스턴스화를 막아버리고(private 생성자) 모든 기능을 static으로만 제공한 것이다.

- GC 수행 / JVM 종료 관련 메소드는 웬만하면 쓰지 말 것
    System.gc(): GC 실행을 "요청"만 할 뿐 실제 실행을 보장하지 않는다. 오히려 불필요한 시점에 GC가 도는 성능 저하를 유발할 수 있어서, GC 타이밍은 JVM에게 맡기는 게 낫다.
    System.exit(): 프로그램을 강제 종료한다. finally 블록이나 자원 해제 같은 정상적인 종료 절차를 건너뛸 수 있어서 예기치 않은 부작용을 일으킬 수 있다.

## 출처 (자바의신2 2장. 가장 많이 쓰는 패키지는 자바랭)
