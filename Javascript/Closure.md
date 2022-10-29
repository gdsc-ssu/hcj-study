# Closure (클로저)

> MDN 정의)
>
> "A closure is the combination of a function and the lexical environment within which that function was declared." 

클로저는 **함수와 그 함수가 선언될 당시의 `LexicalEnvironment`(그 중 `Outer Lexical Environment Reference`)의 상호관계에 따른 현상**이다. 즉, 자바스크립트가 **Lexical Scope**를 따르는 프로그래밍 언어이기 때문에 발생하는 현상이다.

(단어가 헷갈릴 수 있는데 조심하자!)



## 1. Lexical Scope

Lexical Scope를 간단하게 설명하면, "자바스크립트 엔진이 함수를 어디서 호출했는지가 아닌, **어디에 정의했는지에 따라 상위 스코프를 결정하는 것**"을 말한다.

```js
const x = 1;

const test1 = () => {
    console.log(x);
}

const test2 = () => {
    const x = 10;
    test1();
}

test1();	// 1
test2();	// 1 (10이 아님!!)
```

만약 자바스크립트가 상위 스코프를 결정할 때 함수가 정의된 곳이 아닌 호출된 곳에서 결정되었다면 `test2()` 함수의 실행 결과는 10이 되었을 것이다.



### 1.1 함수가 호출될 때 정의된 환경 알아내는 방법

여기서 궁금한 점이 하나 생긴다. 함수는 호출될 때마다 매번 실행 컨텍스트가 생성되고, 함수가 정의된 환경을  `Lexical Environment`의 `Outer Lexical Environment Reference` 에 저장하여 상위 스코프를 참조할 수 있다. 그렇다면 매번 해당 함수가 정의된 환경을 어떻게 알고 매번 `Outer Lexical Environment Reference`에 저장하는 것일까?

그 방법은 바로 **함수 객체의 내부 슬롯 `[[Environment]]`를 이용**하는 것이다. 

함수 정의가 평가되어 함수 객체를 생성할 때, 자신이 정의된 환경에 의해 결정된 **상위 스코프의 참조를 함수 객체 자신의 내부 슬롯 `[[Environment]]`에 저장**한다. 그리고 함수가 호출될 때, 생성될 실행 컨텍스트의  `Lexical Environment`의 `Outer Lexical Environment Reference` (외부 렉시컬 환경에 대한 참조)에 저장될 참조값으로 사용한다.



## 2. Closure와 Lexical Environment

함수의 실행이 종료되면, 실행 컨텍스트 스택에서 종료된 함수의 실행 컨텍스트는 제거된다. **하지만 함수의 내부에 정의된 중첩 함수는 이미 생명 주기가 종료된 외부 함수의 변수를 참조할 수 있다**. 이러한 중첩 함수를 **Closure**(클로저)라고 부른다.

```js
const x = 1;

// 외부 함수
function outer() {
	const x = 10;

  // 중첩 함수(내부 함수)
  const inner = function () {
        console.log(x);
	}
	
  return inner;
}

const myFun = outer();
myFun();	// 10
```

위 코드를 분석해보자. `outer` 함수를 호출하면 `inner` 함수를 반환하고 `outer`함수의 생명 주기(life cycle)는 마감된다. 즉, `outer` 함수의 실행 컨텍스트가 실행 컨텍스트 스택에서 제거되는 것인데, 어떻게 `myFun` 함수는 `outer` 함수 안에서 선언된 `x`에 계속 접근할 수 있을까?

그 이유는 **`outer` 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 제거되지만, `outer` 함수의 `Lexical Environment` 까지 제거되는 것은 아니기 때문**이다.

만약 `inner` 함수가 `outer` 함수 내부에 존재하지 않았다면, `outer` 함수의 실행 컨텍스트가 제거되고 `Lexical Environment`은 garbage collector에 의해 제거된다. 하지만, **`inner` 함수의 `[[Environment]]`에서 `outer` 함수의 `Lexical Environment` 를 참조**하고 있어, garbage collector에 의해 제거되지 않는 것이다. (garbage collector는 어떤 값을 참조하는 변수가 하나라도 있다면 그 값은 수집 대상에 포함시키지 않음)

여기서 메모리가 걱정이 될 수 있는데, 모던 자바스크립트 엔진은 최적화가 잘 되어 있어서 closure가 참조하고 있는 식별자 외에는 기억하지 않으니 `Lexical Environment` 내부의 모든 값들이 저장될 걱정은 하지 않아도 된다!



## 3. 클로저의 활용

### 3.1 콜백 함수 내부에서 외부 데이터를 사용

대표적인 콜백 함수 중 하나인 `addEventListener()`  예제

```js
const fruits = ['apple', 'banana', 'peach'];
...
fruits.forEach((fruit) => {  
	...
	$li.addEventListener('click', () => {
		alert('your choice is' + fruit)   // fruit: 외부 데이터
	});
	...
});
```



### 3.2 접근 권한 제어 (정보 은닉)

**클로저는 상태(state)를 안전하게 변경하고 유지하기 위해 사용될 수 있다.** 즉, 상태가 의도치 않게 변경되지 않도록 **상태를 안전하게 은닉**하고 **특정 함수에게만 상태 변경을 허용**하기 위해 사용한다.

```js
// 💩

let num = 0;	// 상태

const increase = function() {	// 상태 변경 함수
    return ++num;
};

const decrease = function() {	// 상태 변경 함수
    return --num;
};

console.log(increase());	// 1

// 문제점
num = 'test';
console.log(increase());	// NaN
```

위 코드에서 `num` 변수가 전역 변수를 통해 관리되고 있어 누구나 접근 및 변경할 수 있다. 즉, 의도치 않게 상태가 변경될 수 있고 이로 인한 오류가 발생할 수 있다.

따라서 `num` 변수, 즉 상태를 안전하게 변경하고 유지하기 위해 `increase()`, `decrease()` 함수만이 `num` 변수를 참조하고 변경할 수 있게 만들어야 한다.

```js
const counter = (function() {	// 즉시 실행 함수
	let num = 0;
    
	return function() {
		return {
			increase() {
				return ++num;
			},
			decrease() {
				return --num;
			}
		}
	};
}());

const test = new counter();

console.log(test.num);	// undefined, 접근 불가!
console.log(test.increase());	// 1
console.log(test.increase());	// 2
console.log(test.decrease());	// 1
```

위 코드를 실행하면 즉시 실행 함수가 호출되고, 즉시 실행 함수가 반환한 함수가 `counter` 변수에 할당된다. `counter` 변수에 할당된 함수는 자신이 정의된 위치에 의해 결정된 상위 스코프인 즉시 실행 함수의 렉시컬 환경을 기억하는 클로저이다.

이제 `num` 변수는 외부에서 직접 접근할 수 없는 은닉된 private 변수이므로 의도치 않은 변경을 막을 수 있어 안정적인 프로그래밍이 가능해졌다.



> <u>캡슐화</u>(encapsulation)는 객체의 상태를 나타내는 프로퍼티와 프로퍼티를 참조하고 조작할 수 있는 동작인 메서드를 하나로 묶는 것을 말한다. 캡슐화는 객체의 특정 프로퍼티나 메서드를 감출 목적으로 사용하기도 하는데 이를 <u>정보 은닉</u>(information hiding)이라고 한다.
>
> 객체의 상태가 변경되는 것을 방지해 **정보를 보호**하고, 객체 간의 상호 의존성, 즉 **결합도를 낮추는 효과**가 있다.





## 참고자료

- [모던 자바스크립트 Deep Dive (도서)](http://www.yes24.com/Product/Goods/92742567)

