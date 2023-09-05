# 3주차

### 4.3 함수 반환하기

```js
var setup = function () {
  console.log(1)
  return function () {
      console.log(2)
  }
}

var my = setup()
my()
```

- https://hewonjeong.github.io/deep-dive-how-do-react-hooks-really-work-ko/


setup()은 반환된 함수를 감싸고 있어서 closure (11.22)를 생성한다. 클로저는 반환되는 함수에서는 접근할 수 있지만 코드 외부에서는 접근할 수 없어서 비공개 데이터 저장을 위해 사용할 수 있다.

Q. 반환되는 함수라는 뜻은 함수 정의부에서 내부 함수를 말하는지? 
-> 말 그대로 return
Q. 외부는 호출되는 위치를 말하는지!? 


Q. useState을 클로저 관점으로 생각해보면 아래와 같은 코드가 맞는 코드인가? 
```js
const useState = (initValue) => {
	let value = initValue;
	const setValue = (newValue) => {
	    value = newValue
	}
	return [value, setValue]
}
```
useState 함수 내부에 setValue 함수는 클로저를 생성한다. 여기서 반환되는 함수여야만 클로저를 생성하는 것은 아니다. 

- signal
    - [preact](https://taegon.kim/archives/10540)
    - [preact](vhttps://kyechan99.github.io/lib/2021/12/17/React-Preact.html)
- jQuery -> React -> 그 다음?


### 4.4 자기 자신을 정의하는 함수

> 이 패턴은 게으른 함수 선언(lazy function definition)이라고도 불리는데 ... -p82

- 이런 패턴이.. 클로저를 쓰는 게 훨씬 나은 듯.


### 4.5 즉시 실행 함수

```ts
// useEffect에서 즉시 실행 함수를 사용하는 예

useEffect(() => {
  (async () => {
    // ...      
  })()  
}, [])
```

Q. 그럼 지금 시점에서는 즉시 실행 함수를 사용하지 않는 이유와 더 좋은 방법이 무엇이 있는지 궁금했습니다. 
- UMD, CJS, AMD
- ESModule이 나와서?..

### 4.6 즉시 객체 초기화

- init 함수를 만드는 식으로 많이 구현하는 듯.
- 전역 스코프 오염 방지 위해 사용

### 4.7 초기화 시점의 분기

### 4.8 함수 프로퍼티 - 메모이제이션 패턴

Q. JSON.parse와 JSON.stringify 했을때 단점은?
- 성능이 느리다.
- JSON이 아닌 값은 파싱할 수 없다.
    - string, number, array, boolean, null, object

### 4.9 설정 객체 패턴

> 많은 수의 매개변수를 전달하기는 불편하다. 모든 매개변수를 하나의 객체로 만들어 대신 전달하는 방법이 더 낫다. -p94

- 객체를 생성할 때 [빌더 패턴](https://refactoring.guru/ko/design-patterns/builder)도 적용해볼 수 있다.

```ts
const api1 = builder.setHeader().setInterceptor().setBaseUrl().build()

const api2 = builder.setHeader().setInterceptor().setBaseUrl().build()


api1.get();
api2.post();
```

### 4.10 커리(Curry)

하스켈 커리

Q. 그럼 유사배열이라는 것은 정확히 뭐라고 생각하는지 궁금합니다. 

배열같은데 배열이 아닌 친구들
키가 숫자고 length값을 가지는 객체

```ts
{
    0: 'foo',
    1: 'bar',    
    length: 3,
}

// 여기에 넘겨주는 { length: 3 } 객체도 유사배열!
Array.from({ length: 3 }) // [empty, empty, empty]
```

react-hook-form의 에러 객체

### 4.11 요약

## 5장. 객체 생성 패턴

### 5.1 네임스페이스 패턴

```ts
// toast ui 라이브러리는 ToastUI라는 네임스페이스를 정의한다.
const editor = new ToastUI.Editor();
```

### 5.2 의존 관계 선언

### 5.3 비공개 프로퍼티와 메서드

### 5.4 모듈 패턴

- [즉시 실행 함수를 이용한 모듈 import, export](http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html)

```ts
// import
(function (dependency) {
    // dependency ...
})(window)

// export
const mod = (function () {
    // ...
    
    return {} // exported
})()
```

- 함수의 이름이란 무엇인가?

```ts
(() => {}).name // name is '';

const a = () => {};
a.name // name is 'a'

export default () => {} // display-name error
```

- React의 ErrorBoundary

```ts

```

[](https://github.com/CodyMan0/aligoligo/blob/main/src/components/common/Meta.tsx)