# Web Storage

일시적인 정보를 서버에 저장하는 것은 비효율적이므로, 클라이언트 단에서 저장할 수 있는 Web Storage를 활용한다.

- 과거: **Cookie**
- HTML5 이후: **Web Storage**



## 분류

Web Storage는 Local Storage와 Session Storage로 구분된다.

- **Local Storage**: 직접 데이터를 삭제하지 않는 한 계속 유지된다.
- **Session Storage**: 페이지 세션이 유지되는 동안 데이터가 유지된다.



## 개념

Web Storage 객체 `localStorage`와 `sessionStorage`는 브라우저 내의 **key-value 저장소**다.

- key와 value는 항상 **문자열**로 저장된다. (만약 다른 자료형을 사용할 경우 자동으로 문자열로 변경)
- `JSON`을 사용하여 객체 사용 가능하다.



## Cookie와의 차이점

1. **Web Storage는 네트워크 요청 시 서버로 전송되지 않는다.**

   → 쿠키보다 더 많은 자료 보관 가능 (약 2MB 이상)

2. **Web Storage는 HTTP 헤더를 통해 조작되지 않고, 자바스크립트 내에서 조작된다.**

3. **Web Storage 객체는 도메인, 프로토콜, 포트로 정의되는 origin에 묶여있어 프로토콜과 서브 도메인이 다르면 데이터에 접근 불가능하다.**



## 메소드

- `setItem(key, value)`: key-value 쌍을 저장
- `getItem(key)`: key에 해당하는 value를 불러옴
- `removeItem(key)`: 해당하는 key-value 삭제
- `clear()`: 모든 것을 삭제
- `key(index)`: 인덱스에 해당하는 key를 불러옴
- `length`: 저장된 항목의 개수



## 예시

Session Storage의 value로 객체를 저장하기 위해 `JSON`을 사용하는 방식을 하나의 함수로 묶어서 사용할 수 있다.

(Local Storage로 변경하고 싶으면 코드의 `sessionStorage`를 `localStorage`로 변경하면 된다.)

```js
export const callSessionData = (key) => {
  const savedData = sessionStorage.getItem(key);
  return JSON.parse(savedData);
};

export const saveSessionData = (key, value) => {
  const toJson = JSON.stringify(value);
  sessionStorage.setItem(key, toJson);
};
```





## 참고자료

- https://ko.javascript.info/localstorage