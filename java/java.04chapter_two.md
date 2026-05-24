# TIL - Java의 신

- **날짜:** 2026-03-24
- **분야:** `개발` 

## 배운 것
인스턴스 변수, 클래스 변수

## 왜 중요한가?
- 인스턴스 변수: 
1) 객체가 생성될 때 생명이 시작되고, 그 객체를 참조하고 있다는 다른 객체가 없으면 소멸된다.
2) 객체마다 따로 가지는 변수

- 클래스 변수: 
1) 클래스가 처음 호출될 때 생명이 시작되고, 자바 프로그램이 끝날 때 소멸된다.
2) 모든 객체가 공유하는 변수

## 예시 (선택)
public class Person {
    String name;  // 인스턴스 변수
    int age;      // 인스턴스 변수
    static int personCnt; // 클래스 변수
}

Person p1 = new Person();
p1.name = "지니";

Person p2 = new Person();
p2.name = "민수";

Person.personCnt++;  // 객체 없이도 접근 가능

Person p1 = new Person();
p1.personCnt++;

Person p2 = new Person();
p2.personCnt++;

==> p1.name = "지니"
    p2.name = "민수"
// 각 객체당 name 이름을 가지고 있다.

==> personCnt = 2 //개별이 아닌 클래스 한 개만 가지고 있는 값

## 출처
- 자바의 신 (4장. 정보를 어디에 넣고 싶은데 80p)
