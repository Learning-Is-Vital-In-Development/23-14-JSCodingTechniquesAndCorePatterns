# 4주차

### 5.5 샌드박스

- RequireJS와 매우 유사한 형태
    - https://d2.naver.com/helloworld/591319

### 5.6 스태틱 멤버

### 5.7 객체 상수

### 5.8 체이닝 패턴

- this 반환
- `foo().bar().baz();`

### 5.9 mehtod() 메서드

JS에서 프로토타입이란?!
- 객체

자바스크립트는 프로토타입 체인
- 프로퍼티 찾아가는 체인
- 스코프 체인이랑 차이점?
- 객체의 프로토타입을 확인하면서 체인을 거슬러 올라감 => 프로퍼티를 찾는 과정

프로토 타입 체인 : 프로퍼티가 무엇인지 찾아가는 액션
스코프 체인 : 식별자(변수)가 무엇인지 찾아가는 액션

용도
1. 객체 상속을 위해 사용한다. 
2. 객체 메소드 재사용을 위해 사용한다. 

### 5.10 요약

## 6장. 코드 재사용 패턴

> '클래스 상속보다 객체 합성을 우선시하라' -p.137

- 책 '오브젝트'에서,
    - 상속은 인터페이스를 재사용하는 것이다.
    - 합성은 로직을 재사용하는 것이다.
    - 상속은 합성보다 훨씬 더 결합도를 높인다. ⇒ 변경하기 힘들게 한다
    - 그러므로 로직을 재사용하기 위해서는 합성을 활용해야 한다.
    - 상속은 다형성을 활용할 때 좋다.

```ts
class Number {
    toString() {
        return String.toString()
    }
}
```

유지보수가 용이하다는 것은 변경시 범위가 좁다는 의미이다.

### 6.1 클래스 방식 vs 새로운 방식의 상속 패턴

### 6.2 클래스 방식의 상속을 사용할 경우 예상되는 산출물

### 6.3 클래스 방식의 상속 패턴 #1 - 기본 패턴

```ts
Child.prototype = new Parent();
```

### 6.4 클래스 방식의 상속 패턴 #2 - 생성자 빌려쓰기

```ts
function Child() {
    Parent.apply(this, arguments);
}
```

### 6.5 클래스 방식의 상속 패턴 #3 - 생성자 빌려쓰고 프로토타입 지정해주기

```ts
function Child() {
    Parent.apply(this, arguments); // super();
    // this.Parent(arguments); 요런 느낌
    
    // call을 작성하면 
    Parent.call(this, ...arguments); // ?
    
    // .apply(this [a, b, c, d])
    // .call(this, a, b, c, d)
}
Child.prototype = new Parent();
```
- super() 상위 클래스의 constructor를 호출하는 메소드



### 6.6 클래스 방식의 상속 패턴 #4 - 프로토타입 공유

```ts
Child.prototype = Parent.prototype;
```
Class 기능이 없을때 extends 기능을 구현할 수 있는 방법인데...
constructor 호출이 안됨

- new Parent()와 Parent.prototype을 할당할 경우 차이점은?!

정리해보기! 


### 6.7 클래스 방식의 상속 패턴 #5 - 임시 생성자

```ts
var F = function () {};
F.prototype = Parent.prototype;
Child.prototype = new F();
```

- [MDN의 객체 상속](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf#pseudoclassical_inheritance_using_object.setprototypeof)

```ts
function Human(name, level) {
  this.name = name;
  this.level = level;
}

function SuperHero(name, level) {
  Human.call(this, name, level);
}

Object.setPrototypeOf(SuperHero.prototype, Human.prototype);

// Set the `[[Prototype]]` of `SuperHero.prototype`
// to `Human.prototype`
// To set the prototypal inheritance chain

Human.prototype.speak = function () {
  return `${this.name} says hello.`;
};

SuperHero.prototype.fly = function () {
  return `${this.name} is flying.`;
};

const superMan = new SuperHero("Clark Kent", 1);

console.log(superMan.fly());
console.log(superMan.speak());
```


### 6.8 Klass

### 6.9 프로토타입을 활용한 상속

> child 객체는 object()라는 함수를 통해 생성했다. 이 함수는 자바스크립트에는 존재하지 않는다. -p.156

- 이제 Object.create()를 사용하면 된다.

```ts
const parent = {};
const child = Object.create(parent);

const a = {}; --> (Object { }) --> null
```



### 6.10 프로퍼티 복사를 통한 상속

- 다음 문장들의 차이는?
    - `parent.hasOwnProperty(i)`
    - `Object.hasOwn(parent, i)`

```ts
const parent = {
    hasOwnProperty() {
        return true;
    }
}

parent.hasOwnProperty('bbbb') // true
// -> `Object.hasOwn(parent, i)`가 나옴
// property shadowing (가려지다, 덮여씌워지다.)

Object.hasOwnProperty.call(parent, 'bbb')

Object.hasOwn(parent, 'bbb');
```




### 6.11 믹스-인

```ts
const foo = {
    a: 1,
    b: 2,
}

const bar = {
    b: 3,
    c: 4,
}

const mixinResult = {
    ...foo,
    ...bar,
} // { a: 1, b: 3, c: 4 }
```

### 6.12 메서드 빌려쓰기

```ts
const datadogLogger: Logger = {
  info: datadog.info.bind(datadog),
  warn: datadog.warn.bind(datadog),
  error: datadog.error.bind(datadog),
}
// datadog에서 this를 쓸 수도 있어서

const consoleLogger: Logger = {
  info: console.info.bind(console),
  warn: console.warn.bind(console),
  error: console.error.bind(console),  
}

interface Logger {
    info: () => void
    warn: () => void
    error: () => void
}

const isLocal = process.env.ENV === 'LOCAL';

const logger: Logger = isLocal ? consoleLogger : datadogLogger;

logger.error('에러!');
```

```ts
// HTTPClient.ts

// eslint-disable-next-line @typescript-eslint/no-explicit-any
export type AnyRecord = Record<string, any>

export interface HTTPClientConfig<P> {
  params?: P
  headers?: Record<string, string> // { [key: string]: string }
}

export interface HTTPClientConfigWithBody<P, B> extends HTTPClientConfig<P> {
  body?: B
}

export interface HTTPClient {
  get<R = never, P = AnyRecord>(url: string, config?: HTTPClientConfig<P>): Promise<R>
  post<R = never, B = AnyRecord, P = AnyRecord>(
    url: string,
    config?: HTTPClientConfigWithBody<P, B>,
  ): Promise<R>
  patch<R = never, B = AnyRecord, P = AnyRecord>(
    url: string,
    config?: HTTPClientConfigWithBody<P, B>,
  ): Promise<R>
  put<R = never, B = AnyRecord, P = AnyRecord>(
    url: string,
    config?: HTTPClientConfigWithBody<P, B>,
  ): Promise<R>
  delete<R = never, P = AnyRecord>(url: string, config?: HTTPClientConfig<P>): Promise<R>
}

export type RequestInterceptor = (setHeader: (key: string, value: string) => void) => void

export type ResponseInterceptor = (response: unknown) => void

export interface HTTPClientBuilder {
  setBaseUrl(baseUrl: string): HTTPClientBuilder
  setRequestInterceptor(interceptor: RequestInterceptor): HTTPClientBuilder
  setResponseInterceptor(interceptor: ResponseInterceptor): HTTPClientBuilder
  build(): HTTPClient
}
```

```ts
import axios, { AxiosInstance, AxiosResponse } from 'axios'
import {
  HTTPClient,
  HTTPClientBuilder,
  RequestInterceptor,
  ResponseInterceptor,
  HTTPClientConfig,
  HTTPClientConfigWithBody,
  AnyRecord,
} from '@/src/lib/httpClient/HTTPClient'

export class AxiosClient implements HTTPClient {
  private readonly axiosInstance: AxiosInstance

  constructor() {
    this.axiosInstance = axios.create()
  }

  set baseUrl(baseUrl: string) {
    this.axiosInstance.defaults.baseURL = baseUrl
  }

  set requestInterceptor(interceptor: RequestInterceptor) {
    this.axiosInstance.interceptors.request.use((request) => {
      const setHeader = (key: string, value: string) => {
        if (!request.headers) return
        request.headers[key] = value
      }
      interceptor(setHeader)
      return request
    })
  }

  set responseInterceptor(interceptor: ResponseInterceptor) {
    this.axiosInstance.interceptors.response.use((response) => {
      interceptor(response)
    })
  }

  get<R = never, P = AnyRecord>(url: string, config?: HTTPClientConfig<P>) {
    return this.axiosInstance.get<R>(url, config).then(({ data }) => data)
  }

  post<R = never, B = AnyRecord, P = AnyRecord>(url: string, config: HTTPClientConfigWithBody<P, B> = {}) {
    const { body, ...restConfig } = config
    return this.axiosInstance.post<B, AxiosResponse<R>>(url, body, restConfig).then(({ data }) => data)
  }

  put<R = never, B = AnyRecord, P = AnyRecord>(url: string, config: HTTPClientConfigWithBody<P, B> = {}) {
    const { body, ...restConfig } = config
    return this.axiosInstance.put<B, AxiosResponse<R>>(url, body, restConfig).then(({ data }) => data)
  }

  patch<R = never, B = AnyRecord, P = AnyRecord>(url: string, config: HTTPClientConfigWithBody<P, B> = {}) {
    const { body, ...restConfig } = config
    return this.axiosInstance.patch<B, AxiosResponse<R>>(url, body, restConfig).then(({ data }) => data)
  }

  delete<R = never, P = AnyRecord>(url: string, config?: HTTPClientConfig<P>) {
    return this.axiosInstance.delete<R>(url, config).then(({ data }) => data)
  }
}

export class AxiosClientBuilder implements HTTPClientBuilder {
    // private  캡슐화 build 메소드로만 리턴
    // readonly constructor에서만 설정하고 빌드 과정에서 재설정
  private readonly instance: AxiosClient

  constructor() {
    this.instance = new AxiosClient()
  }

  setBaseUrl(baseUrl: string): HTTPClientBuilder {
    this.instance.baseUrl = baseUrl
    return this
  }

  setRequestInterceptor(interceptor: RequestInterceptor) {
    this.instance.requestInterceptor = interceptor
    return this
  }

  setResponseInterceptor(interceptor: ResponseInterceptor) {
    this.instance.responseInterceptor = interceptor
    return this
  }

  build(): HTTPClient {
    return this.instance
  }
}
```

```ts
// index.ts
export const createHTTPClientBuilder = () => new AxiosClientBuilder();
```

```ts
// factory.ts
import { createHTTPClientBuilder } from '@/src/lib/httpClient'
import { AUTH_TOKEN_KEY, AuthToken } from '@/src/components/AuthRoute'

const BASE_URL = 'https://app.com'

export const httpClient = createHTTPClientBuilder()
  .setBaseUrl(BASE_URL)
  .setRequestInterceptor((setHeader) => {
    const auth = localStorage.getItem(AUTH_TOKEN_KEY)
    if (!auth) return
    const { accessToken, tokenType } = JSON.parse(auth) as AuthToken
    setHeader('Authorization', `${tokenType} ${accessToken}`)
  })
  .build()

export const httpClient2 = createHTTPClientBuilder()
    .setBaseUrl(BASE_URL_OTHER)
    .build()
```

### 6.13 요약