좋은 커밋을 하기란 어렵다. 항상 호기롭게 시작하지만 중구난방이 되기 일쑤이고, 항상 커밋하고 나면 오타나 실수가 눈에 보인다. 좋은 커밋을 위한 Cheat Sheet을 작성해보고자 한다.

## 커밋 메시지 컨벤션

이런 분야에 포스팅에 항상 인용되는 [글](https://chris.beams.io/posts/git-commit/)이 있어서 읽고 필요한 것만 간단히 정리해보았다.

좋은 커밋 메시지를 작성하기 위해서는 다음의 규칙들을 지켜야한다.

1. 빈 줄로 제목과 본문을 구분해라
1. 제목은 50자 이내로 작성해라
1. 제목 첫 글자는 대문자로 써라
1. 제목 끝에 마침표를 찍지 마라
1. 명령문으로 작성해라
1. 본문을 72자로 제한해라
1. '어떻게'보다 '왜', '무엇'에 집중해라

이중 `1`, `3`, `5`, `7` 번만 좀 더 자세히 설명하자면, 

`1. 빈 줄로 제목과 본문을 구분해라`는 `git shortlog` 등의 명령어를 사용했을 때, 간단하게 확인할 수 있는 제목과 자세한 설명이 있는 본문을 구분해서 작성하라는 의미이다. 

`3. 제목 첫 글자는 대문자로 써라` 그리고 `5. 명령문으로 작성해라`는 서로 같이 쓰이는게 더 좋을 것 같다. 
`git merge` 명령어의 기본 커밋 메시지는 `Merge branch 'branch_name'`이다. 이 메시지를 보면 알 수 있듯, 3번과 5번은
git에 기본으로 탑재된 커밋메시지의 컨벤션이다. 이들은 이런 기본 컨벤션을 지키면서 가독성을 증가시키기 위한 규칙이다.

`7. '어떻게' 보다 '왜', '무엇'에 집중해라`, 뭐 말 그대로다. 하지만 중요한 것 같아서 한번 더 짚는다. '어떻게'는 코드로 말하자.

## 커밋 메시지 스타일 가이드

이제 좀 더 세세한 스타일에 대한 내용을 알아보자. Udacity의 commitmessage style guide를 바탕으로 작성한 글이다.

```
타입: 제목

본문(옵션)

꼬리말(옵션)
```

기존 컨벤션의 제목, 본문의 형태를 가져가며 타입과 꼬리말이 추가되었다.

타입에는 말 그대로 내가 한 작업의 타입을 작성하면 된다. Udacity에서 제안하는 타입들은 다음과 같다.

- feat: 새로운 기능 추가했을 때
- fix: 버그를 수정했을 때
- docs: 문서를 수정했을 때
- style: 포매팅 등의 이슈, 코드 변경은 없을 때
- refactor: 프로덕션 코드를 리팩토링 했을 때
- test: 테스트를 추가하거나 리팩토링 했을때, 프로덕션 코드의 변경은 없을 때
- chore: 패키지 매니져 설정, 빌드 설정 등 변경했을 때, 마찬가지로 프로덕션 코드의 변경은 없을 때

꼬리말에는 issue tracker ID를 추가할 수 있다.

## 참고

- [How to Write a Git Commit Message - Chris Beams](https://chris.beams.io/posts/git-commit/)
- [https://meetup.toast.com/posts/106 - 김은호](https://meetup.toast.com/posts/106)
- [Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/)
- [Git 커밋 메세지 스타일 가이드 - siyoon210](https://siyoon210.tistory.com/56)