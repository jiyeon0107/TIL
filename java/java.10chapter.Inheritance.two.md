# TIL - java Java의 신

- **날짜:** 2026-04-30
- **분야:** `개발` 

## 배운 것
자바의 상속 중 참조 자료형의 형 변환

## 왜 중요한가?
참조 자료형의 형태를 알아야 오류 없이 접근 가능한 클래스의 메소드와 변수 정보를 이용할 수 있기 때문에 필요 시 형변환을 통해 구현한다.

## 새롭게 알게 된 정보
부모 타입의 객체를 자식 타입으로 형 변환할 때에는 명시적으로 타입을 지정해 주어야 한다.
 이 때, 부모 타입의 실제 객체는 자식 타입이여야만 한다.

## 예시 

```
 업캐스팅 vs 다운캐스팅

class Parent { void parentMethod() {} }
class Child extends Parent { void childMethod() {} }

// 업캐스팅: 자식 → 부모 (자동, 안전)
Parent p = new Child();

// 다운캐스팅: 부모 → 자식 (명시적, 검증 필요)
Child c = (Child) p;

 안전한 다운캐스팅

if (p instanceof Child c) {  // Java 16+
    c.childMethod();
}

```

| 구분 | 코드 예시 | 결과 |
|------|-----------|------|
| 업캐스팅 | `Parent p = new Child();` | ✅ 자동, 항상 안전 |
| 다운캐스팅 (실제 자식) | `Parent p = new Child(); Child c = (Child) p;` | ✅ 정상 동작 |
| 다운캐스팅 (실제 부모) | `Parent p = new Parent(); Child c = (Child) p;` | ❌ `ClassCastException` |
| 안전한 다운캐스팅 | `if (p instanceof Child c) { ... }` | ✅ 권장 패턴 |


## 출처
- 자바의 신 (10장. 자바는 상속이라는 것이있어요)
