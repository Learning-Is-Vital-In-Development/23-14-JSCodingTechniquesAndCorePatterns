# 2주차

## 3장. 리터럴과 생성자

### 3.1 객체 리터럴

> 자바스크립트에 빈 객체란 없다는 사실을 알아두어야 한다. -51p

- 아니다. `Object.create(null)`로 빈 객체를 만들 수 있다.

### 3.2 사용자 정의 생성자 함수

- `Number`, `Object`, `Boolean`
- `new Number()` => `Number{123}`
- `Number("123")` => `123`

#### this란? 
지역 변수를 할당할 수 있는 것.
키워드. 함수마다 this를 가지고 있음.
    - 그냥 호출 -> window / global / globalThis
    - a.b() -> a


화살표 함수의 this binding

- 화살표 함수의 평가
```
1. If name is not present, set name to "".
2. Let scope be the LexicalEnvironment of the running execution context.
3. Let privateScope be the running execution context's PrivateEnvironment.
4. Let sourceText be the source text matched by ArrowFunction.
5. Let closure be OrdinaryFunctionCreate(%Function.prototype%, sourceText, ArrowParameters, ConciseBody, lexical-this, scope, privateScope).
6. Perform SetFunctionName(closure, name).
7. Return closure.
```
- 5번의 `OrdinaryFunctionCreate()` 진행과정
```
    1. Let internalSlotsList be the internal slots listed in Table 34.
    2. Let F be ! OrdinaryObjectCreate(functionPrototype, internalSlotsList).
    3. Set F.[[Call]] to the definition specified in 10.2.1.
    4. Set F.[[SourceText]] to sourceText.
    5. Set F.[[FormalParameters]] to ParameterList.
    6. Set F.[[ECMAScriptCode]] to Body.
    7. If the source text matching Body is strict mode code, let Strict be true; else let Strict be false.
    8. Set F.[[Strict]] to Strict.
    9. If thisMode is lexical-this, set F.[[ThisMode]] to lexical.
    10. Else if Strict is true, set F.[[ThisMode]] to strict.
    11. Else, set F.[[ThisMode]] to global.
    12. Set F.[[IsClassConstructor]] to false.
    13. Set F.[[Environment]] to Scope.
    14. Set F.[[PrivateEnvironment]] to PrivateScope.
    15. Set F.[[ScriptOrModule]] to GetActiveScriptOrModule().
    16. Set F.[[Realm]] to the current Realm Record.
    17. Set F.[[HomeObject]] to undefined.
    18. Set F.[[Fields]] to a new empty List.
    19. Set F.[[PrivateMethods]] to a new empty List.
    20. Set F.[[ClassFieldInitializerName]] to empty.
    21. Let len be the ExpectedArgumentCount of ParameterList.
    22. Perform ! SetFunctionLength(F, len).
    23. Return F.
```

[this](https://github.com/johnyejin/tech-interview-for-frontend/blob/main/Notes/JavaScript/this.md)
 

### 3.3 new를 강제하는 패턴

### 3.4 배열 리터럴

> new Array(3)은 길이가 3이고 실제 원소값은 가지지 않는 배열을 생성한다. -59p

- 1~100의 원소를 가지는 배열을 만드는 법?
    > empty 는 map 으로 안돌아가짐
    - `Array(100).fill(null).map((_, idx) => idx + 1)`
    - `Array.from({ length: 100 }, (_, idx) => idx + 1)`
    - const a = Array.from({ length: 100 }).map((_, idx) => idx + 1);
- undefined, empty

> Object.prototype.toString() 메서드를 호출하여 판별할 수 있다. 배열에 toString을 호출하면 "[object Array]"라는 문자열을 반환하게 되어 있다. -60p

- 모든 toString()은 같은 Object.prototype에서 상속받은 함수인 줄 알았는데 아니였음..
- "foooo".toString()
- [Object.prototype.toString](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)
- `Object.prototype.toString({})` // `[object Object]`
    - ({}).toString()
- `String.prototype.toString({})` // `''` 
    - "foo".toString()![](https://hackmd.io/_uploads/r12TZ8jT2.png)


### 3.5 JSON

[`JSON.parse() vs eval()`](`https://github.com/Learning-Is-Vital-In-Development/23-14-JSCodingTechniquesAndCorePatterns/issues/3`)



### 3.6 정규 표현식 

> 그러나 매칭시킬 패턴을 미리 알 수 없고 런타임에 문자열로 만들어지는 경우에는 new Regex()를 사용해야 한다. -64p

- 기본적으로는 리터럴을 쓰는 게 더 낫다.

### 3.7 원시 데이터 타입 래퍼

> 자바스크립트에는 숫자, 문자열, 불린, null, undefined의 다섯 가지 원시 데이터 타입이 있다. -p64

- 현재는 BigInt, Symbol 두 개가 더해져 일곱 가지가 되었다.

> 메서드를 호출하는 순간 내부적으로는 원시 데이터 타입 값이 객체로 임시 변환되어 객체처럼 동작한다. -p65

Symbol 사용 방법?!
-> 중복되지 않는 key를 만들고 싶을 때?

### 3.8 에러 객체

> 이 생성자들을 통해 생성된 에러 객체들은 다음과 같은 프로퍼티를 가진다. name, message -p66

- Error 객체에 [cause](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Error/cause) 프로퍼티도 추가되었다.

```ts
// 달아주는 앱 전역 에러 핸들러
// 처리되지 않은 모든 에러를 모두 로그 찍겠다!
app.config.errorHandler = (err) => {
    console.error(err);
    sentry.captureException(err);
};
```

### 3.9 요약

> ... Error() 등 내장 생성자들은 사용을 자제하라

- 에러를 상속받아 사용하는 패턴
```ts!
try {
    throw MyError('oops!')    
} catch(err) {
     if (err instanceof MyError) {
         // ...
     }   
}
```

## 4장. 함수

### 4.1 배경 지식

> name 프로퍼티는 파이어버그나 다른 디버거에서 코드를 디버깅할 때 유용하다. 함수 내에서 발생한 에러를 보여주어야 할 때, 디버거가 name 프로퍼티 값을 확인하여 이름표로 쓸 수 있기 때문이다. -73p
 
- 리액트에도 비슷하게 컴포넌트의 이름을 붙이는 것이 좋다. (관련 규칙 : [display-name](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/display-name.md))

```tsx
function Comp() {
    return <></>
}

Comp.Item = function Item () {
    return <></>
}
```

특징은 두가지 

일급 시민, 일급 함수?
- 일급 = 다른 요소와 차이가 없다. 다른 값처럼 쓸 수 있다.
1. 일급 객체라는 것
	- 런타임, 즉 프로그램 실행 중에 동적으로 생성
	- 변수에 할당할 수 있고 다른 변수에 참조를 복사할 수 있고 확장 가능하고 삭제가능
	- 다른 함수의 인자로 전달할 수 있고 return값이 될 수 있다. 
	- 자기 자신의 프로퍼니와 메서드를 가질 수 있다. 
2. 유효 범위를 제공한다는 것
    - 모듈을 만들기 위한 목적으로도 사용

### 4.2 콜백 패턴

```js
const myapp = {};
myapp.color = 'green'
myapp.paint = function (node) {
  node.style.color = this.color;
}

const findNodes = function (callback){
  if(typeof callback === 'function'){
    callback(found)
  }
}

findNodes(myapp.paint)
```
callback()의 인자를 찾을 수 없다. this가 예상과 다르게 동작. this가 전역 객체를 참조한다. 콜백 내부의 this는 예상과 달리 dom을 참조한다.
```js
const myapp = {};
myapp.color = 'green'
myapp.paint = function (node) {
  node.style.color = this.color;
}

const findNodes = function (callback, callback_obj){
    // found ...
  if(typeof callback === 'function'){
    callback.call(callback_obj,found)
  }
}

findNodes(myapp,myapp.paint)
// myapp.paint.bind(myapp) 이런 식으로 바인딩해서 전달 가능
```



## 다음 스터디 주제

- 디자인패턴
- 소스코드 파헤치기
- zustand deep dive
- react deep dive
- git
- storybook
- TDD? E2E Test? (Playwright?)



## 숙제

- global, window, globalThis
- WeakMap, WeakSet
- 주영님 블로그 작성후 링크올려주세요
- 주영님 jotai 블로그 작성후 올려주세요
- 주영님 에러처리 디프만 코드 보여주세요
- callback this
