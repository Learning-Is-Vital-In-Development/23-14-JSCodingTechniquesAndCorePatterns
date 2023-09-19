# 5주차

## 7장. 디자인 패턴

### 7.1 싱글톤

```ts
export const obj = {}
```

```ts
class C {
    
}

export const c = new C();
```

### 7.2 팩터리

- https://refactoring.guru/ko/design-patterns/factory-method
- https://www.patterns.dev/posts/factory-pattern


```ts
const data = [...];
              
data.map(createFoo);

// 많을 때 분리
function createFoo() {
    return {}
}
```

```ts
// 추상 팩토리
interface Car {}

interface CarFactory {
    create: () => Car
}

const truckFactory: CarFactory = {
    create: () => {}
}

const bikeFactory: CarFactory = {
    create: () => {}
}

const factory: CarFactory = isRacing ? bikeFactory : truckFactory;

factory.create();
```

### 7.3 반복자

- [iterable, iterator protocol](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Iteration_protocols)
- [iterator helpers](https://github.com/tc39/proposal-iterator-helpers)
- `[].values().map().reduce().take().drop()`
- `Iterator.from()`

### 7.4 장식자 (decorator)

- 클래스에 적용하는 형태로 구현됨
    - https://github.com/tc39/proposal-decorators

```ts
class App {

    @Cache({ ttl: 30 })
    render() {
        // return html;
    }
}
```
    
- [타입스크립트](https://velog.io/@octo__/TypeScript-%EB%8D%B0%EC%BD%94%EB%A0%88%EC%9D%B4%ED%84%B0Decorator)

### 7.5 전략

```ts
// authenticator.auth(googleStrategy)
```

### 7.6 퍼사드

- 주로 같이 자주 사용되는 메서드의 호출들을 묶어 새로운 메소드를 만들어주는 패턴
- 복잡도 낮추기
- 훅도 퍼사드

```tsx
// 복잡한 것이 있을 때, 그것을 감추고 간단한 인터페이스를 노출하는 패턴.

function f() {
    const { handleInput, handleSubmit, .... } = useXXXX()

    return <></>;
}
```

### 7.7 프록시

- [Proxy](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Proxy)
- Vue 내부적으로 proxy로 구현

```ts
const state = new Proxy({ value: 1 }, { value: double });
const double = () => state * 2;

state.value = 3;
double // 6;
```

- [Reflect](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect)
- [메타 프로그래밍](https://meetup.nhncloud.com/posts/302)



### 7.8 중재자
- 컴포넌트가 서로 직접 대화하는 대신 중개자는 요청을 수신하고 이를 전달한다.


```ts

```


### 7.9 감시자

- 이벤트가 발생할 때마다 옵저버블은 모든 옵저버에게 알림을 보낸다,
- 서로 다른 프레임 간의 통신
    - [postMessage](https://developer.mozilla.org/ko/docs/Web/API/Window/postMessage)
- 서로 다른 탭 간의 통신
    - https://developer.mozilla.org/en-US/docs/Web/API/Broadcast_Channel_API

### 7.10 요약

