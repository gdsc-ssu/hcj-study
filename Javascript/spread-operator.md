## spread-operator 전개구문
전개구문은 개인적으로 진짜 손에 안 익혀지는 문법이다. 한 번 더 공부하면서 최종정리 하려 한다 !

### 1. Spread operator 스프레드 연산자
스프레드 연산자는 반복가능한(이터러블)객체에 적용할 수 있는 문법이다.
배열이나 문자열 등을 아래처럼 풀어 요소 하나하나로 전개시킬 수 있다. 
```js
const arr = [1,2,3,4,5];
const str = "string";

console.log(...arr) //1 2 3 4 5
console.log(...str) // s t r i n g
```

### 2. 사용 케이스
스프레드 연산자는 ...만 붙이면 자유롭게 그 객체를 펼칠 수 있어 여러 곳에 유용하게 사용할 수 있다
1) 함수 호출 시 인자로 넘길 때</br>
```js
function mul(x,y,z) {
    return x*y*z;
}
const arr = [1,3,5];

const result1 = mul.apply(null, arr); //원래는 apply()를 사용했어야 하는데
const result2 = mul(...arr); //...을 사용할 수도 있다

console.log(result1);
console.log(result2);
```

2. 배열 리터럴의 전개</br>
배열 리터럴은 []로 생성한 배열을 의미한다.
배열에 추가로 요소를 넣는다던지, 배열을 복사, 배열 이어 붙이기 등 다양한 작업에서 ... 연산자를 사용할 수 있다. 
```js
const arr1 = [0, 1, 2];
const arr2 = [3, 4, 5];

//1. 배열 복사
const arr3 = [...arr1]; //[0, 1, 2]
//2. 배열에 추가 요소로 넣기
const arr4 = [1,2, ...arr2, 9, 10]; // [1, 2, 3, 4,5, 9, 10]
//3. 두 배열 이어 붙이기
const arr5 = [...arr1, ...arr2]; //[0, 1, 2, 3, 4, 5]
```
3. 객체 스프레드 프로퍼티</br>
어떤 한 객체의 프로퍼티를 다른 새로운 객체에 복사할 때도 유용하게 사용된다. 사실 객체 (object)자체는 반복가능한(iterable) 객체가 아니며, 아래와 같이 사용하면 에러가 발생한다
```js
const obj = {name : 'john', age: '20'};
console.log(...obj);
```
하지만 위와 같은 방식이 아니라 ES9에서는 객체의 프로퍼티를 전개할 수 있도록 지원하고 있으며 아래와 같이 객체 내부에 사용할 수 있다.
```js
console.log(obj1);
console.log(clonedObj1);
console.log(obj1 == clonedObj1) //false : 프로퍼티만 복사받은 객체이므로 두 객체의 참조값 자체는 다르다

const mergedObj = {...obj1, ...obj2};
console.log(mergedObj);
```
이러한 스프레드 연산자의 성질은 <b>상태의 불변성 유지</b>에도 유용하다.
### 기존의 메모리에 담겨 있던 값이 다시 변경되지 않으며, 이 불변성을 유지함으로서 상태변화를 빠르게 탐지할 수 있다.
```js
const obj1 = {name : 'John', age : '20', flag : 'true', foo: 'bar'};
const newObj1 = { ...obj1, name: 'Alice'}; //복사받은 값에서 뒤에 적은 name값만 변경(덮어씌우는)효과를 갖게 된다

console.log(newObj1);
console.log(obj1 === newObj1); //false : 서로 다른 객체임
```