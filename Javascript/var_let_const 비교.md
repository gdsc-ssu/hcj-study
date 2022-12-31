# `var`

중복 선언이 가능하다

오로지 **함수의 코드 블록만을 지역 스코프로 인정**해서 함수 외부에서 `var` 키워드로 선언한 변수는 코드 블록 내에서 선언해도 모두 전역 변수가 된다

```tsx
var x = 1;
if(true) {
	var x = 10;
}
console.log(x);    // 10
```

전역변수를 남발할 가능성이 높아서 전역 변수가 중복 선언되는 경우가 발생 할 수 있다


<br>


### 함수 스코프

`var` 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정하는 함수 스코프를 따른다.

즉, 함수 내에서 선언된 변수(지역변수)는 함수 내에서만 유효하며, 함수 외부(전역변수)에서는 참조할 수 없다.

```jsx
// 전역 변수로 선언
var x = 5;
var y = 10;

// 전역 함수로 func() 선언
function func() {
    console.log("전역변수 x: ", x);         // 5
    console.log("전역변수 y: ", y);         // 10
    return x - y;       // 전역변수 x y 에 접근
}
console.log(func());    // -5

// 전역 함수로 parfunc() 선언
function parfunc() {
    console.log("x: ", x);         // undefined
    console.log("y: ", y);         // undefined
    var x = 12;
    var y = 17;
    function add() {
        console.log("지역변수 x: ", x);     // 12
        console.log("지역변수 y: ", y)      // 17
        return x + y;
    }
    console.log("add:", add())          // 29
}
parfunc()
console.log(x);     // 5
console.log(y)      // 10
```


<br>


# `let`

`var`의 중복 선언이 가능한 단점을 보완하기 위해 ES6에서 새로 도입했다

### 중복 선언시 문법 에러 발생


![image](https://user-images.githubusercontent.com/58413633/198831922-9df26a06-4cd8-4a02-9c30-8a6f0df85401.png)



<br>


### 블록 스코프

: 모든 코드 블록 내에서 선언된 변수(지역변수)는 코드 블록 내에서만 유효하며 코드 블록 외부(전역변수)에서는 참조할 수 없다. 

`let`으로 선언한 변수는 모든 코드 블록(함수, if, for, while, try/catch)을 지역 스코프로 인정한다

```jsx
let j = 1;  // 전역변수
{
    let j = 2;      // 지역변수
    let bar = 3;    // 지역변수
}
console.log(j);     // 1
console.log(bar);   // ReferenceError: bar is not defined
```
![image](https://user-images.githubusercontent.com/58413633/198831971-bc28536d-2d58-4ece-bc0d-706d55a61ce8.png)



<br>


## `var` vs `let`

function scope를 가지는 var

```jsx
var foo = "This is String"
if(typeof foo === "string"){
    var result = true;
}
else var result = false;
console.log(result)        // true
```

block scope를 가지는 `let`

```jsx
var foo = "This is String"
if(typeof foo === "string"){
    let result = true;
}
else let result = false;     // error: 'let' 선언은 블록 내부에서만 선언될 수 있습니다.
console.log(result)    // ReferenceError: result is not defined
```

<br>

## `const`

상수를 선언하기 위해 사용하며, 선언한 변수는 **반드시 선언과 동시에 초기화**해야한다

```jsx
const foo;   // error: 'const' 선언은 초기화해야 합니다.
```

`let` 과 똑같이 **블록 레벨 스코프**를 가진다

<br>

`var`과 `let`은 재할당이 자유롭지만 `const`로 선언한 변수는 **재할당이 금지**된다

```jsx
const foo = 1;
foo = 2;        // TypeError: Assignment to constant variable.
```

<br>

### 상수

재할당이 금지된 변수.

상수는 상태 유지와, 가독성, 유지보수의 편의를 위해 사용해야 한다.

```jsx
// 세전 가격
let preTaxPrice = 100;

// 세후 가격
let afterTaxPrice = preTaxPrice + (preTaxPrice * 0.1);
            // 여기서 0.1의 의미를 명확히 알기 어렵다 -> 가독성이 좋지 않다
```

여기서 0.1은 쉽게 바뀌지 않는 값이므로 `const` 키워드를 사용하는 것이 좋다.

```jsx
const TAX_RATE = 0.1;    // 대문자를 사용하여 상수임을 나타내기
// 세전 가격
let preTaxPrice = 100;

// 세후 가격
let afterTaxPrice = preTaxPrice + (preTaxPrice * TAX_RATE);
```

<br>

### 객체

`const` 키워드로 선언한 변수는 값을 변경할 수 없지만, 그 변수에 **객체**를 할당한 경우 변경 가능

```jsx
const person = {
    name: "lee"
}
console.log(person);    // { name: 'lee' }
person.name = "kim"
console.log(person);    // { name: 'kim' }
```

<br>

<br>

---

<br>

# 정리

- 변수 선언에는 기본적으로 `const`를 사용하자
- `let`은 재할당이 필요한 경우에 한정하여 사용하는 것이 좋다 (변수의 스코프는 최대한 좁게)
- `const` 키워드를 사용하면 의도하지 않은 재할당을 방지하기 때문에 안전하다

변수 선언시 우선 `const`를 사용하고 재할당이 필요하면, 그때 `const`를 `let`으로 변경해도 늦지않다!!!
