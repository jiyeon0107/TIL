# TIL - git 구조

- **날짜:** 2026-02-18
- **분야:** `개발` 

## 배운 것
git 구조에 따라 push 방법이 달라진다.

## 왜 중요한가?
로컬 브랜치 → master
원격 저장소 → origin
원격 브랜치 → origin/master

그런데 처음 push 할 때는
로컬 master가 어느 원격 브랜치를 따라가야 하는지 모르는 상태일 수 있다.

## 예시 (선택)
[git push --set-upstream origin master]

master를 origin/master에 push
앞으로 master는 origin/master를 따라가라고 설정

## 출처
- 본 문서는 ChatGPT(OpenAI)를 참고하여 작성하였으며, 내용은 Git 공식 문서를 기반으로 재확인하였다.
