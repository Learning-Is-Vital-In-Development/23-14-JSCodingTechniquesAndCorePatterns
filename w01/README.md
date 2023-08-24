# 1주차

## 1장. 개요

### 1.1 패턴
- 모범적인 관행, 쓰임새에 맞게 추상화된 원리, 어떤 범주의 문제를 해결하는 템플릿
- 패턴은 검증된 실행방법을 사용하여 쓸데없이 시간을 낭비하지않고 더 나은 코드를 작성할 수 있게 도와준다.

사용하는 패턴
- [presentational-container-pattern](https://www.patterns.dev/posts/presentational-container-pattern)

코드 순서를 어떻게 배치하는지?
- 기능별로 묶기,
- 코드배치 룰
    - https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/sort-comp.md
    - [채널톡에서 쓰는 예시](https://github.com/channel-io/eslint-config/blob/exp/rules/react.js#L23C4-L23C4)


### 1.2 자바스크립트의 개념
- **number, string vs Number, String**
    - number vs Number
        - number
            - 타입 
            - typeof foo === "number"
        - Number
            - 숫자로 변환하는 함수
            - Number("123")
            - (12).toString()
- 네이티브 객체 : ECMAScript 표준에 정의된 객체
    - 내장객체(Array, Date…) 또는 사용자 정의 객체
    -  Object, String, Number, Function, Array, RegExp, Date, Math 등이 있다.
- 호스트 객체 : 호스트환경(브라우저 환경)에서 정의된 객체
    - window, DOM 객체
        - 브라우저 환경에서만!!! 실행됨
        - window, document, location, XMLHttpRequest, querySelectorAll,,,
    - 호스트 객체는 호스트 환경에 정의된 객체를 말한다. 예를 들어, 브라우저에서 동작하는 환경과 브라우저 외부에서 동작하는 환경의 자바스크립트(node.js)는 다른 호스트 객체를 사용할 수 있다.


만약 브라우저 환경이라면 다음과 같은 것들이 존재한다. 

### 1.3 ECMAScript 5

- https://github.com/tc39/proposals
- stage 0 > stage 1 ,2,3 > final > 내년 ecmascript
- https://github.com/tc39/proposal-pipeline-operator
- 


### 챙겨보는거 공유

- https://github.com/tc39/proposals
    - ECMAScript 스펙 미리보기
- https://news.hada.io/
    - geeknews
- https://chromestatus.com/roadmap
    - 크롬 스펙 미리보기
- https://kofearticle.substack.com/p/korean-fe-article-304?utm_source=substack&utm_medium=email
- 에러 핸들링
    - https://velog.io/@eunddodi/3%EA%B0%9C%EC%9B%94%EC%B0%A8-%EC%A3%BC%EB%8B%88%EC%96%B4%EA%B0%80-%EC%97%90%EB%9F%AC-%ED%95%B8%EB%93%A4%EB%A7%81-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EA%B5%AC%EC%B6%95%ED%95%9C-%ED%9B%84%EA%B8%B0
    - https://jbee.io/react/error-declarative-handling-2/

### 블로그

- https://www.daleseo.com



### 1.4 JSLint

### 1.5 콘솔

## 2장. 기초

### 2.1 유지보수 가능한 코드 작성

- 버그를 고치는사람과 버그를 만드는사람, 버그를 발견한 사람이 모두 다를수있기때문에 코드를 이해하는데 걸리는 시간을 줄이는것이 중요하다.
- 주석을 적는가?
    - 클린코드에서는 주석을 권장하지 않음.
    - 하지만 주석이 필요할 때가 있음.
    - [vscode todo tree 익스텐션](https://velog.io/@young_pallete/%EC%9D%B5%EC%8A%A4%ED%85%90%EC%85%98-Todo-Tree-Extension%EC%9C%BC%EB%A1%9C-%EA%B9%94%EB%81%94%ED%95%98%EA%B2%8C-todo-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0)
    - [토스의 세종대왕 프로젝트](https://tosspayments-dev.oopy.io/chapters/frontend/posts/hangul-coding-convention)
    - [ts-patten](https://velog.io/@hhhminme/ts-pattern%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-%EA%B0%95%EB%A0%A5%ED%95%9C-%EB%94%94%EC%9E%90%EC%9D%B8-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0#ts-pattern-vs-switch-%EB%AC%B4%EC%97%87%EC%9D%B4-%EB%8D%94-%EC%A2%8B%EC%9D%84%EA%B9%8C)
- 얼마나 나눌 것인가?

### 2.2 전역변수 최소화

- 책이 모듈이 나오기 전에 적힌 책이라서 전역변수에 대한 강조가 많은 듯.


```javascript
const a = 1;

function f() {
    console.log(a);
    const a = 2;
    console.log(a);    
}

f();
```

<aside>
❓ empty 처리는 어떻게 하시는지?
    - msw
</aside>

<aside>
❓ 파일내에서 비슷한 역할을 하는 코드들을 모아서 관리하는지
예를들면 useState, useEffect 같은거
</aside>

### 2.3 for 루프

- for문보다 for..of 사용
    - iterator
    - [prefer-for-of](https://typescript-eslint.io/rules/prefer-for-of/)

### 2.4 for-in 

- property descriptor
    - enumerable
        - [propertyIsEnumerable()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/propertyIsEnumerable)
- [hasOwnProperty()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)
    - [hasOwn()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwn)
    - [in operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in)
    - [no-prototype-builtins](https://eslint.org/docs/latest/rules/no-prototype-builtins)
        - `Object.create(null)`
        - property shadowing

### 2.5 내장 생성자 프로토타입 확장하기 / 확장하지 않기

- polyfill
- structuredClone
- 구형 브라우저 지원하기 위함.
- https://caniuse.com/
- https://browsersl.ist/
- 빌드할 때 폴리필 넣으면 폴리필 고정됨.
- 런타임에 브라우저에 따라 폴리필 다르게
    - https://toss.tech/article/smart-polyfills

### 2.6 switch 패턴

- [리액트에서 쓰는 SwitchCase](https://slash.page/ko/libraries/react/react/src/components/switchcase/switchcase.i18n/)

```ts
enum Car {
    A,
    B,
    C,
}

type Car = "A" | "B" | "C";
```

### 2.7 암묵적 타입캐스팅 피하기

- new Function()
    - script 실행할 때 eval() 보다 낫다.

### 2.8 parseInt()를 통한 숫자 변환

### 2.9 코딩 규칙

- 세미콜론 쓰는지?
    - Yes, no..
- if 한줄일 떄라도 중괄호 쓰는지
- A && B
- 여러줄이면 스위치문

### 2.10 명명 규칙
- snake_case
    - axios interceptor..
- SNAKE_CASE 상수
- PascalCase
- [type vs interface](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/consistent-type-definitions.md)
- eslint-typescript/stylistic

### 2.11 주석 작성
- 함수의 매개변수와 반환값에 대해서는 문서화할필요가있다.

<aside>
❓ 함수 생성시 파라미터 작성 방식 : 나열 vs 객체
</aside>

### 2.12 API 문서 작성

- jsdoc

```ts
/**
 * @params
 * @return
 */
function f() {}
```

### 2.13 독자를 위한 문서 작성

[뱅크샐러드 테크스펙](https://blog.banksalad.com/tech/we-work-by-tech-spec/)

### 2.14 동료 리뷰

[multi](https://multi.app?w_id=M7vIqGqSkoyUlzpYhC5o)

### 2.15 출시 단계의 압축

- 개발자는 개발의 효율성을 위한 코드를 작성해야힘 : 공백, 들여쓰기, 주석등을 달고, 파일 압축은 압축도구에 맡긴다.
- 요즘에 잘됨.

### 2.16 JSLint 실행

- eslint + prettier
    - format on save


`
cn
className={cn('')}``


rfc
export const FN = () => {}

rafc
const FN = () => {}
export default FN

## 숙제

- 지훈
    - number vs Number
    - String() vs  .toString()
  ``  - type vs Interface

- eslint-consistent-type
