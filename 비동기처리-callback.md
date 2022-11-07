# 비동기 처리 - callback

Week: 3주차
name: 나세빈
status: 학습 중
subject: JS

~~오.. 비동기처리에 대해 단계별로 잘 정리 해주신 분이 계신다.. 근데 내용이 자세하지 않아서 ,, 주제를 참고해야겠당~~

[[자바스크립트] 비동기 처리 1부 - Callback](https://www.daleseo.com/js-async-callback/)

차근차근 공부해보기 ,, !

# **콜백 함수**

## 콜백 ,,?

프로그래밍에서 콜백 또는 콜백 함수는 다른 코드의 인수로서 넘겨주는 실행 가능한 코드를 말한다. 콜백을 넘겨받는 코드는 이 콜백을 필요에 따라 즉시 실행할 수도 있고, 아니면 나중에 실행할 수도 있다.

## **콜백함수란**

다른 함수가 실행을 끝낸 뒤 실행되는 함수!

함수 : 입력(파라미터) → 출력(리턴값)

`자바스크립트 : 출력값 X, 대신 콜백 함수를 입력받는 함수들이 있다.`

js에서 함수는 **object**

함수는 다른 함수의 인자로 쓰일 수도 , 어떤 함수에 의해 리턴될 수도 있다.  → ‘고차 함수’

인자로 넘겨지는 함수를 콜백 함수라고 한다.

`함수를 등록하기만 하고 어떤 이벤트가 발생했거나 특정 시점에 도달했을 때 시스템에서 호출하는 함수`

```jsx
functio func(callback) {
	callback();
}
function callback() {
	console.log("callback이다");
}

func(callback);

결과 : callback이다
```

함수 f1 실행 → callback 함수 실행 (제어권은 f1에게)

```jsx
function introduce (lastName, firstName, callback) {
	var fullName = lastName + firstName;
	callback(fullName);
}

introduce("홍", "길동", function(name) {
	console.log(name);
    };

// 결과 -> 홍길동

출처: https://inpa.tistory.com/entry/JS-📚-자바스크립트-콜백-함수 [👨‍💻 Dev Scroll]
```

위 예제를 보면, introduce 함수를 실행하면, callback자리를 새로운 함수 function(name)으로 지정 해주면서 함수 안에서 **callback(fullname)**으로 실행 되는 함수가 된다.

## 필요성

- 가독성이나 코드 재사용 면에서 사용
- 비동기 방식 - 어떤 요청이 오면 완료가 되기 전에 다음 요청을 실행하는 방식(동시 효율적 처리 기능)으로 작성된 함수를 동기 - 하나의 요청이 오면 완료가 된 후 다음 요청을 실행하는 방식 (순차적 로직 흐름)처리하기 위해 필요

예)

```jsx
function findUserAndCallBack(id, cb) {
  setTimeout(function () {
    console.log("waited 0.1 sec.");
    const user = {
      id: id,
      name: "User" + id,
      email: id + "@test.com",
    };
    cb(user);
  }, 100);
}

findUserAndCallBack(1, function (user) {
  console.log("user:", user);
});

결과
waited 0.1 sec.
user: {id: 1, name: "User1", email: "1@test.com"}
```

결과값을 바로 리턴받지 않고, 결과값을 통해 처리할 로직을 콜백 함수로 넘겨서 구현

추가)콜백 지옥이라고 해서 개발자들이 많은 어려움을 겪고 있어 promise나 async/await를 써서 대체 하고 있다고 한다.