# 🐙 Git 협업 및 충돌 해결 워크플로우

1. 작업 브랜치 Push
   작업한 이슈 브랜치(예: feat/login)를 원격 저장소(Remote)에 올립니다.
   `git push origin feat/login`

2. PR(Pull Request) 생성
   GitHub 페이지로 이동하여 main 브랜치로 합쳐달라는 PR을 생성합니다.

3. 💥 충돌(Conflict) 발생 시 로컬 동기화
   GitHub에서 충돌 알림이 뜨면, 로컬(내 컴퓨터)에서 원격의 최신 내용을 가져와 합칩니다.
   1. 내 작업 브랜치로 이동 (확인용)
      `git checkout feat/login`
   2. 원격 저장소의 최신 정보를 가져옴 (업데이트 확인)
      ` git fetch origin`
   3. 가져온 원격의 최신 main 내용을 내 브랜치에 병합 시도
      `git merge origin/main`

4. 충돌 해결 및 커밋
   VS Code에서 충돌난 파일들을 수정합니다. 수정이 완료되면 다시 스테이징하고 커밋합니다.
   충돌 수정 후 저장

   ````git add .
   git commit -m "Fix: 충돌 해결 및 코드 병합"```

   ````

5. 재전송 (Push)
   수정한 내용을 다시 원격 브랜치로 보냅니다. 이렇게 하면 열려있는 PR에 자동으로 수정 사항이 반영됩니다. (PR을 새로 만들 필요가 없습니다!)
   bashgit push origin feat/login

6. 최종 병합 (Merge)
   GitHub PR 페이지에서 충돌이 해결된 것을 확인하고, 승인 후 [Merge pull request] 버튼을 클릭하여 main 브랜치에 병합합니다.

# CSS 방법론-Bem 방식

## 1.Bem 이란?

CSS 제작 방법론으로 일종의 ‘네이밍 컨벤션’이다.

Block(블록),Element(요소),Modifier(수정자)의 약자로, 목적에 따라 네이밍 하는 것이 특징.

### 1-2 Bem의 규칙

- 명시도를 균일하게 유지하기 위해 class 선택자만 사용한다.
- 목적에 따라 네이밍한다.
- Html 요소들을 각각 Block\_\_Element--Modifer 세가지로 분류한다.

## 2. Block, Element, Modifier

### 2-1. Block

블럭은 기능적으로 독립적인 페이지 구성 요소로써, 재사용이 가능한 부분.

![블록 예시](https://velog.velcdn.com/images/kjwboa/post/525d2a21-65cd-4f8c-b22e-e71a52e1a5ff/image.png)

예를 들어 이미지처럼 logo 블록, search 블록, menu 블록 등의 블록들은 여기저기 재사용될 수 있는 요소들이다.

- Block은 중첩되는 것을 허용한다.
- Block의 이름은 상태가 아닌 용도를 나타내야 한다.
- 모든 Block이 Element를 가지는 것은 아니다.

```
<!-- O 올바른 사용 : 용도(error)를 나타냄 -->
<div class="error"><div>

<!-- X 잘못된 사용 : 상태(red)를 나타냄 -->
<div class="red-box"><div>
```

### 2-2. Element

블록을 구성하는 단위. block은 독립적이지만, element는 의존적인 형태다. 자기 자신이 속한 block 내에서만 사용 될 수 있다.

![element 예시](https://velog.velcdn.com/images/kjwboa/post/8aded662-58f5-4eb8-85fc-c6c8f0aa88ad/image.png)
이미지 처럼 탭메뉴 전체를 감싸는 부분이 블록이고, 탭메뉴 하나하나가 엘리먼트이다.

```
<ul class="tab">
  <li class="tab__item">탭 01</li>
  <li class="tab__item">탭 02</li>
  <li class="tab__item">탭 03</li>
</ul>
```

이미지와 코드의 예시를 보면, tab은 block이고, tab_item은 element이다.

- Element는 Block의 부품으로 Block과 별도로 사용할 수 없다.
- Element 역시 Block처럼 상태가 아닌 용도를 나타내야 한다.
  예)
  이것이 무엇인가? (O) : item, text, button...
  이것이 어떻게 생겼는가? (X) : red, big...
- element는 서로 중첩이 가능하다. 다만, Element는 Block의 하위 요소이기때문에 다른 Element에 포함되지 않는다.

```
<form class="search-form">
	<div class="search-form__inner>
    	<!-- X 권장: search-from__input | search-from__content-input -->
    	<input class="serach-form__inner__input /">
        <!-- X 권장: search-form__button | search-from__content-button -->
        <button class="search-form__content__button"></button>
    </div>
</form>
```

### 2-3. Modifier

Modifier은 Block이나 Element의 속성으로, 상태 또는 동작을 정의한다.

```
<ul class="tab">
  <li class="tab__item tab__item--active">탭 01</li>
  <li class="tab__item">탭 02</li>
  <li class="tab__item">탭 03</li>
</ul>
```

tab\_\_item--active의 --active가 modifier이다.

- Modifier는 모양(appearance), 상태(state), 동작(behavior)을 나타낸다.
  - 특정 사이즈 또는 테마 : size_s / theme_blak
  - 특정 상태 : disabled / focused / active
  - 특정 동작 : dirctions_left-top
- Modifier는 Block, Element의 모양/상태/동작을 변경하는 것이기 때문에 Block, Element에 추가하여 사용한다. (block\_\_element—modifier)
