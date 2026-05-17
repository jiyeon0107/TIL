# TIL - JAVA 책: Java의 신

- **날짜:** 2026-05-17
- **분야:** `개발` 

## 배운 것
Object 클래스

## 왜 중요한가?
모든 자바 클래스의 부모이기 때문에 꼭 알고 넘어가야 한다.

## 새롭게 알게 된 정보
1. object 클래스에서 가장 많이 쓰이는 toString() 메소드 호출의 경우
 - System.out.println() 메소드에 매개 변수로 들어가는 경우
 - 객체에 대하여 더하기 연산을 하는 경우

2. DTO(Data Transfer Object)를 사용할 때에는 toSting() 메소드를 Overriding해 놓는 것이 좋다.

3. 직접 equals() 메소드나 hashcode() 메소드를 작성하는 것은 권장하지 않는다. 요즘 각종 툴에서는 이 두개의 메소드를 자동으로 생성해주는 기능을 제공하고 있으므로, 그 기능을 사용할 것을 권장한다.

## 예시 
1번 내용 예시

```
// Java
package c.inheritance;

public class ToString {
    public static void main(String[] args) {
        ToString thisObject = new ToString();
        thisObject.toStringMethod(thisObject);   // 이름 통일
    }
    
    public void toStringMethod(Object obj) {     // 클래스 안으로
        System.out.println(obj);
        System.out.println(obj.toString());
        System.out.println("plus " + obj);
    }
}

```
**출력 결과**

c.inheritance.ToString@1540e19d
c.inheritance.ToString@1540e19d
plus c.inheritance.ToString@1540e19d
```

2번 내용 예시

```
public class MemberDTO{
    public String name;
    public String phone;
    public String email;
}
```

```
//toString 메소드가 Overriding되어 있지 않다면, MemberDTO에 선언된 값들을 확인하는 방법

public class Test {
    public static void main(String[] args) {
        MemberDTO member = new MemberDTO();
        member.name = "지연";
        member.phone = "010-1234-5678";
        member.email = "jiyeon@example.com";

        // ❌ 이렇게 하면 객체 정보가 안 보임
        System.out.println(member);
        // 출력: MemberDTO@1540e19d  ← 의미 없는 해시코드

        // ✅ 필드를 직접 출력
        System.out.println("name: " + member.name);
        System.out.println("phone: " + member.phone);
        System.out.println("email: " + member.email);
    }
}
```

```
//toString 메소드가 Overriding 방법
public class MemberDTO {
    public String name;
    public String phone;
    public String email;
    
    @Override
    public String toString() {
        return "name: " + name + ", phone: " + phone + ", email: " + email;
    }
}

```

## 출처
- 자바의 신 (12장. 모든 클래스의 부모 클래스는 Object예요.)
