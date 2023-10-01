# 6주차

## 8장. DOM과 브라우저 패턴

### 8.1 관심사의 분리

### 8.2 DOM 스크립팅

> 원칙적으로 DOM 업데이트를 최소화하는 게 좋다. 이를 위해서는 변경 사항들을 일괄 처리하거나, 실제 문서 트리 외부에서 변경 작업을 수행해야 한다. -p.217

- innerHTML로 한 번에 변경하기

### 8.3 이벤트

### 8.4 장시간 수행되는 스크립트

> 또한 과도한 스크립트 연산을 실행하면, 브라우저 UI는 응답불가능한 상태가 되어 사용자가 아무 것도 클릭할 수 없게 된다. 이런 상태는 사용자 경험에 해가 되므로 반드시 피해야 한다. -p.223

- [Node.js 가이드에도 비슷한 내용이 있음 (이벤트 루프를 막지마세요)](https://nodejs.org/ko/docs/guides/dont-block-the-event-loop#%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84%EB%A5%BC-%EB%A7%89%EC%A7%80%EB%A7%88%EC%84%B8%EC%9A%94)

### 8.5 원격 스크립팅

> ... JSONP를 사용하는 방법이다. XHR과 달리 브라우저의 동일 도메인 정책의 제약을 받지 않는다. 따라서, 서드파티 사이트에서 데이터를 로딩할 수 있으므로 보안 측면에서의 영향을 고려하여 신중하게 사용해야 한다. -p.227

- `JSONP`, `Image Beacons`와 같은 방법들은 모던 브라우저에선 `CORS`로 대체됨

```
/get-user-jsonp?callback=fn


fn({
 user: 1
});
```

// SOP(동일출처원칙)
// XHR 요청하면 SOP에 걸림
// img, css, js file 요청들은 SOP에 안 걸림
// jsonp, image beacon은 이 원리를 활용한 방법


- 쓰기: 일반적으로 허용한다. 일부 HTTP요청은 preflight가 필요하다
(CORS에서 등장하는 preflight)
    - 링크, 리다이렉트, 폼 제출
    - `<a>`
    - `<form>` 으로 다른 origin에 데이터를 쓰는 작업
- 임베딩: 일반적으로 허용한다.
    - `<script src="..."></script>`
    - `<link rel="stylesheet" href="…">`
    - `<img>`, `<video>`, `<audio>`, `<object>`, `<embed>`
    - `@font-face`
    - `<iframe>`
- 읽기: 일반적으로 허용하지 않는다.
    - 보통 js 코드로 접근하는 행위들이 해당된다.
    - js로 iframe내의 document에 접근
    - js로 canvas내에 다른 origin의 이미지를 불러오는 작업
    - js로 다른 리소스를 fetch하는 작업


// CORS
// access-control-* 헤더를 보고 브라우저가 응답을 허용하는 매커니즘

// GET 요청이 아닌 요청? 리소스를 변경할 수 있는 요청?
// preflight request
// OPTIONS 메서드 사용 -> 요청 전에 먼저 허용되는 지 체크
// option 메서드는 캐싱
//`Access-Control-Max-Age`는 preflight 요청의 결과를 캐시할 기간을 결정하는 헤더 요청입니다.


[단순 요청](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS#%EB%8B%A8%EC%88%9C_%EC%9A%94%EC%B2%ADsimple_requests)


### 8.6 자바스크립트 배포

### 8.7 로딩 전략 
