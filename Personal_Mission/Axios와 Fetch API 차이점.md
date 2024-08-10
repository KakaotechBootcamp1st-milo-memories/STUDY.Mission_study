`Axios`와 `Fetch API`는 둘 다 자바스크립트에서 HTTP 요청을 보낼 때 사용되는 라이브러리 및 API

## **지원 및 기본 제공**

### **Axios**

- 외부 라이브러리로 설치가 필요하며, Node.js 및 브라우저 환경 모두에서 사용할 수 있음
- `npm` 또는 `yarn`을 통해 설치해야 하며, ES6 Promise를 기본으로 사용

### **Fetch API**

- 브라우저에 내장된 JavaScript API
- ES6에서 처음 도입되었으며, Promise 기반으로 동작

## **기본 사용법**

### **Axios**

```jsx
axios.get('/api/data')
  .then(response => console.log(response.data))
  .catch(error => console.error(error));

```

### **Fetch API**

```jsx
fetch('/api/data')
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Fetch error:', error));

```

## **기본 동작의 차이**

### **Axios**

- 기본적으로 JSON 데이터에 대한 자동 변환을 제공
- 응답을 받으면 자동으로 JSON을 파싱하여 JavaScript 객체로 변환해줌
- 타임아웃 설정, 응답 데이터 구조화 등 추가 기능을 제공
- 요청 인터셉터와 응답 인터셉터 기능을 제공하여, 요청을 보내기 전에 헤더를 수정하거나, 응답을 받기 전에 데이터를 변형 가능

### **Fetch API**

- 응답을 자동으로 JSON으로 변환하지 않음
- `response.json()`을 호출해야 JSON 데이터를 얻을 수 있음
- 네트워크 오류가 발생한 경우에만 `catch` 블록이 실행
- 서버에서 응답 코드가 404나 500인 경우에는 `catch` 블록이 실행되지 않고 `then`에서 `response.ok`를 체크해야 함
- 타임아웃이나 인터셉터 기능은 기본적으로 제공되지 않음

## **타임아웃 설정**

### **Axios**

- 타임아웃 설정을 지원

```jsx
axios.get('/api/data', { timeout: 1000 }) // 1초 타임아웃 설정
  .then(response => console.log(response.data))
  .catch(error => console.error('Timeout exceeded:', error));

```

### **Fetch API**

- 기본적으로 타임아웃 기능을 지원하지 않음
- 타임아웃 기능이 필요하다면 `Promise`를 사용해 직접 구현해야 함

```jsx
const controller = new AbortController();
const timeoutId = setTimeout(() => controller.abort(), 1000);

fetch('/api/data', { signal: controller.signal })
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => {
    if (error.name === 'AbortError') {
      console.error('Fetch timeout:', error);
    } else {
      console.error('Fetch error:', error);
    }
  });

```

## **지원 브라우저**

### **Axios**

- 거의 모든 브라우저에서 사용 가능

### **Fetch API**

- 최신 브라우저에서 기본적으로 지원되지만 IE는 Fetch API를 지원하지 않으므로 폴리필(polyfill) 필요

## **기능 및 유연성**

### **Axios**

- 요청/응답 인터셉터, 취소 토큰, 기본 헤더 설정, 요청 반복 및 재시도와 같은 기능이 내장
- URL 인코딩된 데이터를 자동으로 처리 가능
- 다양한 HTTP 메서드를 지원하고, 요청 본문 데이터로 `Buffer`, `ArrayBuffer`, `Stream` 등을 지원

### **Fetch API**:

- 더 원시적인 API로서, Axios가 제공하는 대부분의 기능은 수동으로 구현해야 함
