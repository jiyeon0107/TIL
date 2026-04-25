# TIL - java Java의 신

- **날짜:** 2026-04-25
- **분야:** `개발` 

## 배운 것
패키지 선언

## 왜 중요한가?
중복된 이름의 자바 파일을 용도에 맞게 사용할 수 있도록 한다.

## 예시 (패키지 선언)
```
User.java  ← 회원 관리용
User.java  ← 관리자용
User.java  ← 외부 라이브러리에도 있음
```

패키지가 없으면 셋 다 같은 User 자바 파일이라서 Java가 어떤 걸 써야할 지 구분하지 못한다.

```
com.myapp.member.User      // 일반 회원
com.myapp.admin.User       // 관리자
com.google.auth.User       // 구글 라이브러리 User
```

```
<패키지가 없으면 파일 구조>
src/
├── User.java
├── Product.java
├── Order.java
├── UserController.java
├── ProductController.java
├── UserService.java
├── ProductService.java
├── UserRepository.java
...  (수백 개 파일이 한 폴더에)

<패키지로 정리하면 파일 구조>
src/
├── controller/
│   ├── UserController.java
│   └── ProductController.java
├── service/
│   ├── UserService.java
│   └── ProductService.java
└── repository/
    ├── UserRepository.java
    └── ProductRepository.java
```

## 출처
- 자바의 신 (9장. 자바를 배우면 패키지와 접근 제어자는 꼭 알아야 해요)
