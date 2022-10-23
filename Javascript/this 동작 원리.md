# `this`

## `this`가 필요한 이유
생성자 함수로 인스턴스를 생성하려면 먼저 생성자 함수가 존재해야 한다.

생성자 함수를 정의하는 시점에는 아직 인스턴스를 생성하기 이전이므로 생성자 함수가 생성할 인스턴스를 가리키는 식별자를 알 수 없으므로 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 `this` 식별자가 필요하다

> **`this`는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수(self-referencing variable)다. `this`를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.**

`this`는 JS엔진에 의해 암묵적으로 생성!

```jsx
// this는 어디서든지 참조 가능
// 전역에서의 this는 전역 객체 window
console.log(this);   // window

function square(number) {
  // 일반 함수 내부에서 this는 전역 객체 window를 가리킴
  console.log(this);   // window
  return number * number;
}
square(2);

const person = {
    name: 'LEE',
    getName() {
        // 메서드 내부에서 this는 메서드를 호출한 객체
        console.log(this);   // {name: "LEE", getName: f}
        return this.name;
    }
};
console.log(person.getName());  // LEE

function Person(name) {
    this.name = name;
    // 생성자 함수 내부에서 this는 생성자 함수가 생성할 인스턴스를 가리킴
    console.log(this);  // Person {name: "Lee"}
}

const me = new Person("LEE");
```

<br>


## 함수 호출 방식

this 바인딩(this에 바인딩될 값)은 함수 호출 방식, 즉 <U>함수가 어떻게 호출되었는지</U>에 따라 동적으로 결정된다.

### 1. 일반 함수 호출

기본적으로 this에는 **전역 객체(global object)** 가 바인딩된다.

```jsx
function foo() {
	console.log("foo's this: ", this);    // window
	function bar() {
		console.log("bar's this:", this);   // window
	}
	bar();
}
foo();
```

중첩 함수를 **일반 함수로 호출하면 함수 내부의 this에는 전역 객체가 바인딩** 된다

하지만 객체를 생성하지 않는 일반 함수에서 this는 의미X

<br>



strict mode가 적용되면 this에는 `undefined`가 바인딩 ⬇️

```jsx
function foo() {
	'use strict';
	
	console.log("foo's this: ", this);   // undefined
	
```

<br>

메서드 내에서 정의한 중첩 함수도 **일반 함수** 로 호출되면 

중첩 함수 내부의 this에는 **전역객체** 가 바인딩 ⬇️

```jsx
// var 키워드로 선언한 전역변수 value는 전역 객체의 프로퍼티
var value = 1;
// const 키워드로 선언한 전역 변수 value는 전역 객체의 프로퍼티X

const obj = {
	value: 100,
	foo() {
		console.log("foo's this: ", this);   // {value: 100, foo: f}
		console.log("foo's this.value: ", this);  // 100

		// 메서드 내에서 정의한 중첩 함수
		function bar() {
			console.log("bar's this: ", this);  // window
			console.log("bar's this.value: ", this.value); // 1
		}

		// 메서드 내에서 정의한 중첩 함수도 일반 함수로 호출되면 
		// 중첩 함수 내부의 this에는 전역객체가 바인딩
		bar();
	}
};

obj.foo();
```

<br>


콜백 함수가 일반함수로 호출되면 콜백 함수 내부의 this에도 전역객체가 바인딩

어떠한 함수라도 일반 함수로 호출되면 this에 전역 객체 바인딩 ⬇️

```jsx
var value = 1;

const obj = {
	value: 100,
	foo() {
		console.log("foo's this: ", this);   // {value: 100, foo: f}
			// 콜백 함수 내부의 this에는 전역 객체가 바인딩 됨
		setTimeout(function () {
			console.log("callback's this: ", this);  // window
			console.log("callback's this.value: ", this.value);  // 1
		}, 100);
	}
};

obj.foo();
```

→ 일반 함수로 호출된 모든 함수(중첩 함수, 콜백 함수 포함) 내부의 this에는 전역 객체 바인딩

메서드 내부에서 `setTimeout` 함수에 전달된 콜백 함수의 this에는 전역객체 바인딩

따라서 `this.value`는 obj 객체의 value 프로퍼티가 아닌 전역 객체의 value(= `window.value` )

`var` 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 되므로

<br>


메서드 내부의 중첩 함수나 콜백 함수의 this 바인딩을 메서드의 this 바인딩과 일치시키기 위한 방법 ⬇️

```jsx
var value = 1;

const obj = {
	value: 100,
	foo() {
			// this 바인딩(obj)을 변수 that에 할당
		const that = this;

			// 콜백 함수 내부에서 this 대신 that을 참조
		setTimeout(function () {
			console.log(that.value);  // 100
		}, 100);
	}
};

obj.foo();
```

<br>

`this` 를 명시적으로 바인딩할 수 있는 `apply` `call` `bind` 메서드 제공

```jsx
var value = 1;

const obj = {
	value: 100,
	foo() {
			// 콜백 함수에 명시적으로 this를 바인딩
		setTimeout(function () {
			console.log(this.value);  // 100
		}.bind(this), 100);
	}
};

obj.foo();
```

<br>

화살표 함수 사용해서 `this` 바인딩 일치시키기

```jsx
var value = 1;

const obj = {
	value: 100,
	foo() {
			// 화살표 함수 내부의 this는 상위 스코프의 this를 가리킨다
		setTimeout(() => console.log(this.value), 100);  // 100
	}
};

obj.foo();
```

<br>

### 2. 메서드 호출

메서드 내부의 `this`에는 **메서드를 호출한 객체**, 메서드 이름 앞의 마침표(.) 연산자 앞에 기술한 객체가 바인딩된다.

```jsx
const person = {
	name: 'Lee',
	getName() {
		// 메서드 내부의 this는 메서드를 호출한 객체에 바인딩
		return this.name;
	}
};

// 메서드 getName을 호출한 객체는 person
console.log(person.getName());   // Lee
```

→ `getName()` 메서드는 `person` 객체의 메서드로 정의되었다.

→ `person` 객체의 `getName` 프로퍼티가 가리키는 함수 객체는 `person` 객체에 포함된것이 아니라 독립적으로 존재하는 별도의 객체

<br>

```jsx
const anotherPerson = {
	name: 'Kim'
};

// getName 메서드를 anotherPerson 객체의 메서드로 할당
anotherPerson.getName = person.getName;

// getName 메서드를 호출한 객체는 anotherPerson
console.log(anotherPerson.getName());   // Kim

// getName 메서드를 변수에 할당
const getName = person.getName;

// getName 메서드를 일반 함수로 호출
console.log(getName());  // ''
// 일반 함수로 호출된 getName 함수 내부의 this.name은 브라우저 환경에서 window.name과 같다
// 브라우저 환경에서 window.name은 브라우저 창의 이름을 나타내는 빌트인 프로퍼티이며
// 기본값은 ''
// Node.js 환경에서 this.name은 undefined
```

→ 메서드 내부의 this는 프로퍼티로 메서드를 가리키고 있는 객체와는 관계가 없고 메서드를 호출한 객체에 바인딩된다

<br>

```jsx
function Person(name) {
	this.name = name;
}

Person.prototype.getName = function () {
	return this.name;
};

const me = new Person('Lee');

// getName 메서드를 호출한 객체는 me
console.log(me.getName());  // (1) Lee

Person.prototype.name = 'Kim';

// getName 메서드를 호출한 객체는 Person.prototype 이다
console.log(Person.prototype.getName());  // (2) Kim
```

→ (1)의 경우 `getName` 메서드를 호출한 객체는 `me` . `getName` 메서드 내부의 `this`는 `me`를 가리키며 `this.name` = ‘Lee’

→ (2)의 경우 `getName` 메서드를 호출한 객체는 `Person.protoype`. `Person.protoype` 도 객체이므로 직접 메서드를 호출할 수 있다. 따라서 `getName` 메서드 내부의 `this`는 `Person.protoype`을 가리키며 `this.name` = ‘Kim’

<br>

<br>

### 3. 생성자 함수 호출

생성자 함수 내부의 `this` 에는 생성자 함수가 (미래에) 생성할 인스턴스가 바인딩된다.

```jsx
// 생성자 함수
function Circle(radius) {
	// 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다
	this.radius = radius;
	this.getDiameter = function () {
		return 2 * this.radius;
	};
}

// 반지름이 5인 Circle 객체를 생성
const circle1 = new Circle(5);
// 반지름이 10인 Circle 객체를 생성
const circle2 = new Circle(10);

console.log(circle1.getDiameter());  // 10
console.log(circle2.getDiameter());  // 20
```

<br>

생성자 함수는 이름 그대로 객체를 생성하는 함수.

일반함수와 동일한 방법으로 생성자 함수를 정의하고 new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다. 만약 new 연산자와 함께 생성자 함수를 호출하지 않으면 일반 함수로 동작한다.

```jsx
// new 연산자와 함께 호출하지 않으면 생성자 함수로 동작하지 않는다. => 일반적인 함수 호출
const circle3 = Circle(15);

// 일반 함수로 호출된 Circle에는 반환문이 없으므로 암묵적으로 undefined 반환
console.log(circle3);   // undefined

// 일반 함수로 호출된 Circle 내부의 this는 전역객체를 가리킴
console.log(radius);  // 15
```


<br>

### 4. Function.prototype.apply/call/bind 메서드에 의한 간접호출

`apply`와 `call`은 `this`로 사용할 객체와 인수 리스트를 인수로 전달받아 함수를 호출

<br>

```jsx
function getThisBinding() {
	return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

console.log(getThisBinding());  // window

//getThisBinding 함수를 호출하면서 인수로 전달한 객체를 getThisBinding 함수의 this에 바인딩
console.log(getThisBinding.apply(thisArg));  // {a:1}
console.log(getThisBinding.call(thisArg));   // {a:1}
```

`apply`와 `call` 메서드의 본질적인 기능은 함수를 호출하는 것

`apply`와 `call` 메서드는 함수를 호출하면서 첫번째 인수로 전달한 객체를 호출한 함수의 `this`에 바인딩

<br>


`apply`와 `call` 메서드는 호출한 함수에 인수를 전달하는 방식만 다를 뿐 동일하게 동작

아래 예제는 `getThisBinding` 함수에 인수를 전달하지 않는다.

```jsx
function getThisBinding() {
	console.log(arguments);
	return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

//getThisBinding 함수를 호출하면서 인수로 전달한 객체를 getThisBinding 함수의 this에 바인딩
// apply 메서드는 호출할 함수의 인수를 배열로 묶어서 전달
console.log(getThisBinding.apply(thisArg, [1,2,3])); 
// Arguments(3) [1,2,3, callee: f, Symbol(Symbol.iterator): f]
// {a:1}

// call 메서드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달
console.log(getThisBinding.call(thisArg,1,2,3));   
// Arguments(3) [1,2,3, callee: f, Symbol(Symbol.iterator): f]
// {a:1}
```

→ `apply` 메서드는 <U>호출할 함수의 인수를 **배열** 로 묶어</U> 전달

→ `call` 메서드는 <U>호출할 함수의 인수를 쉼표로 구분한 **리스트** 형식</U>으로 전달

`apply` 와 `call` 메서드는 호출할 <U>함수에 인수를 전달하는 방식만</U> 다르다.

`this`로 사용할 <U>객체를 전달하면서 함수를 호출</U>하는 것은 동일

<br>

`apply` 와 `call` 메서드를 이용하면 `arguments`객체는  `slice()`를 사용할 수 있다

```jsx
function convertArgsToArray() {
	console.log(arguments);

	// arguments 객체를 배열로 변환
	// Array.protoype.slice를 인수 없이 호출하면 배열의 복사본을 생성
	const arr = Array.prototype.slice.call(arguments);
	// const arr = Array.prottype.slice.apply(arguments);
	console.log(arr);

	return arr;
}

convertArgsToArray(1,2,3);   // [1,2,3]
```

<br>

`Function.prototype.bind` 메서드는 `apply`와 `call` 메서드와 다르게 **함수 호출 X**

첫번째 인수로 전달한 값으로 `this` 바인딩이 교체된 함수를 새롭게 생성하여 반환

```jsx
function getThisBinding() {
	return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

// bind 메서드는 첫번째 인수로 전달한 thisArg로 this 바인딩이 교체된
// getThisBinding 함수를 새롭게 생성해 반환
console.log(getThisBinding.bind(thisArg));   // getThisBinding
// bind 메서드는 함수를 호출하지 않으므로 명시적으로 호출하기
console.log(getThisBinding.bind(thisArg)());  // {a:1}
```

<br>

`bind` 메서드는 메서드의 `this`와 메서드 내부의 중첩함수 또는 콜백함수의 `this`가 불일치하는 문제를 해결하기 위해 유용하게 사용됨

```jsx
const person = {
	name: 'Lee',
	foo(callback) {
		// (1)
		setTimeout(callback, 100);
	}
};

person.foo(function () {
	console.log(`Hi! my name is ${this.name}.`); // (2) Hi! my name is .
	// 일반 함수로 호출된 콜백 함수 내부의 this.name은 브라우저 환경에서 window.name과 같다
	// 브라우저 환경에서 window.name은 브라우저 창의 이름을 나타내는 빌트인 프로퍼티, 기본값은 ''
	// Node.js 환경에서 this.name은 undefined
});
```

`person.foo`의 콜백함수가 호출되기 이전인 

(1)의 시점에서 `this`는 `foo`메서드를 호출한 객체(`person` 객체). 

`person.foo`의 콜백함수가 일반함수로서 호출된 (2)의 시점에서 `this`는 전역객체 `window`를 가리킴

→ `person.foo`의 콜백함수 내부에서 `this.name` = `window.name`

`person.foo`의 콜백함수는 외부 함수 `person.foo`를 돕는 **헬퍼함수** 역할을 하기 때문에 외부함수 `person.foo` 내부의 `this`와 콜백함수의 `this`가 다르면 문제 발생!!!

콜백 함수 내부의 `this`를 외부 함수 내부의 `this`와 일치시키기

→ `bind` 메서드를 사용하여 `this` 일치시키기 가능

```jsx
const person = {
	name: 'Lee',
	foo(callback) {
		// bind 메서드로 callback 함수 내부의 this 바인딩 전달
		setTimeout(callback.bind(this), 100);
	}
};

person.foo(function () {
	console.log(`Hi! my name is &{this.name}.`);  // Hi! my name is Lee.
});
```

<br>


<br>

| 함수 호출 방식 | this 바인딩 |
| --- | --- |
| 일반 함수 호출 | 전역 객체 |
| 메서드 호출 | 메서드를 호출한 객체 |
| 생성자 함수 호출 | 생성자 함수가 (미래에) 생성할 인스턴스 |
| Function.prototype.apply/call/bind 메서드에 의한 간접 호출 | Function.prototype.apply/call/bind 메서드에 첫번째 인수로 전달한 객체 |
