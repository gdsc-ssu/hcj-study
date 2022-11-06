# 배열 (array)

### 배열 [ ]

js에서 배열은 이름과 인덱스로 참조되는 정렬된 값의 집합으로 정의

배열을 구성하는 각각의 값을 배열요소(element)라고 하며, 배열에서의 위치를 가리키는 숫자를 인덱스라고 한다.

- 배열의 특징
1. 배열 요소의 타입이 고정되어 있지 않으므로, 같은 배열에 있는 배열 요소끼리의 타입이 서로 다를 수 있다.
2. 배열 요소의 인댁스가 연속적이지 않아도 되며, 따라서 특정 배열 요소가 비어 있을 수 있다.
3. js에서 배열은 array 객체로 다룬다.

### 배열의 생성

```jsx
1. var arr = [배열요소1, 배열요소2,...];          // 배열 리터럴을 이용하는 방법

2. var arr = Array(배열요소1, 배열요소2,...);     // Array 객체의 생성자를 이용하는 방법

3. var arr = new Array(배열요소1, 배열요소2,...); // new 연산자를 이용한 Array 객체 생성 방법
```

### 배열의 참조

- 자바스크립트에서 배열의 각 요소를 참조하고 싶을 때는 [ ] 연산자를 사용한다.

```jsx
var arr = ["JavaScript"]; // 요소가 하나뿐인 배열을 생성함.

var element = arr[0];     // 배열의 첫 번째 요소를 읽어서 대입함.

 

arr[1] = 10;      // 배열의 두 번째 요소에 숫자 10을 대입함. 배열의 길이는 1에서 2로 늘어남.

arr[2] = element; // 배열의 세 번째 요소에 변수 element의 값을 대입함. 배열의 길이는 2에서 3으로 늘어남.
```

- 배열 요소의 개수를 배열의 길이 → length를 이용
- 인덱스는 언제나 0부터 시작

### 배열의 기본 연산 (삽입,삭제)

- 삽입

.push(element) 메소드를 사용해 배열 삽입을 구현

```jsx
let array1=[1,2,3,4]

array1.push(5) //array1=[1,2,3,4,5]
```

- 삭제

.pop() 메소드를 사용해 배열 삭제를 구현

```jsx
let array1=[1,2,3,4]

array1.pop() // 4를 반환
```

### 배열 내장 함수

- 배열을 다룰 때 유요한 내장 함수

### forEach

- 배열의 모든 요소(각 원소)에 대해 주어진 함수를 실행 (for문을 대신해서 사용)

```jsx
const heros =[’a’, ‘b’ ,’c’];

heros.forEach(hero=>{
	console.log(hero);
}); // a b c
```

forEach 함수의 파라미터로는, 각 원소에 대하여 처리하고 싶은 코드를 함수로 넣어준다. 이 함수의 파라미터 hero는 각 원소를 가르킨다.

이렇게 함수형태의 파라미터를 전달하는 것을 콜백함수. 함수를 등록해주면, forEach 가 실행을 해준다.

### map

- map 은 배열 안의 각 원소를 변환 할 때 사용 되며, **이 과정에서 새로운 배열이 만들어진다.**→ 그러므로 빈배열에 넣는 것이 안되고 새로운 상수값에 재할당을 해야한다.

```jsx
const array = [1, 2, 3, 4, 5, 6, 7, 8]

const squared = array.map(n => n * n);
console.log(squared);
// 찍히는 값 = [1, 4, 9, 16, 25, 36, 49, 64]
```

- map 내장함수를 안쓴다면

```jsx
const array=[1, 2, 3, 4, 5, 6, 7, 8];

const squared=[];

array.forEach(n=>{squared.push(n*n);});

console.log(squared);
```

### indexOf

- indexOf는 원하는 항목이 배열의 몇번째 원소인지 찾아주는 함수이다.

```jsx
const superHeroes2 = ['아이언맨', '캡틴 아메리카', '토르', '닥터 스터레인지'];
const index = superHeroes2.indexOf('토르');
console.log(index);
// 찍히는 값 = 2
```

### findIndex

- 객체들로 이루어진 배열 안에서 객체의 정보를 가지고 몇번째인지 알아내려고 할때는 indexOf를 쓰지 못하므로 findIndex 함수 사용한다.

```jsx
const todos = [
  {
    id: 1,
    text: '자바스크립트 입문',
    done: true,
  },
  {
    id: 2,
    text: '함수 배우기',
    done: true,
  },
  {
    id: 3,
    text: '객체와 배열 배우기',
    done: true,
  },
  {
    id: 4,
    text: '배열 내장함수 배우기',
    done: false
  }
]

const index2 = todos.findIndex(todo => todo.id === 3);
console.log(index2);
// 찍히는 값 = 2
```

### find

- find 함수는 findIndex랑 비슷하며, 찾아낸 값이 몇번째인지 알아내는 것이 아니라, 찾아낸 값 자체를 반환한다.

```jsx
const todo = todos.find(todo => todo.id === 3);
console.log(todo);
// 찍히는 값 = {id: 3, text: "객체와 배열 배우기", done: true
```

### filter

- filter 함수는 배열에서 특정 조건을 만족하는 값들만 따로 추출하여 **새로운 배열을 만든다.**

```jsx
const brr=arr.filter(a⇒a.done===false);

console.log(brr);—> false값을 가진 배열만 나오게 된다.
```

### splice

- 배열에서 특정항목을 제거할 때 사용한다. (기존의 배열을 건드림)

```jsx
const numbers = [10, 20, 30, 40];
const index = numbers.indexOf(30);
numbers.splice(index, 1);
console.log(numbers);
```

→ splice는 인자가 2개이며, index는 제거를 시작할 부분을 말하고,. 1은 몇개를 삭제할지이다.

결론은 30을 삭제하고 10,20,40만 출력된다.

### slice

- slice 는 splice처럼 배열을 잘라낼 때 사용( 중요한 점은 **기존의 배열은 건들이지 않는다)**

```jsx
const numbers = [10, 20, 30, 40];
const sliced = numbers.slice(0, 2);
console.log(sliced);
찍히는 값 = [10, 20]
console.log(numbers);
찍히는 값 = [10, 20, 30, 40]
기존의 배열 변화 없음!
```

### shift, pop

- -배열의 첫번째원소(shift)와 마지막 원소(pop)를 제거하는 함수  (기존의 배열을 건드림)

```jsx
const numbers = [10, 20, 30, 40];

const value = numbers.shift();
console.log(value);
찍히는 값 = [10]
console.log(numbers);
// 찍히는 값 = [20, 30, 40]

const numbers2 = [10, 20, 30, 40];
const values = numbers2.pop();
console.log(values);
찍히는 값 = [40]
console.log(numbers2);
// 찍히는 값 = [10, 20, 30]
```

### unshift, push

- 배열의 첫번째 원소(unshift)를 추가하고, 마지막원소(push)를 추가하는 함수 (기존의 배열을 건드림)

```jsx
const numbers3 = [10, 20, 30, 40];

numbers3.unshift(5);
console.log(numbers3)
// 찍히는 값 = [5, 10, 20, 30, 40]

const numbers4 = [10, 20, 30, 40];

numbers4.push(5);
console.log(numbers4)
// 찍히는 값 = [10, 20, 30, 40, 5]
```

### concat

- 2개의 배열을 하나로 합쳐주는 함수 (기존의 배열을 건드리지 않음.)

```jsx
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6]

const concated = arr1.concat(arr2); // arr1과arr2가 새로운 concated 배열로 선언
console.log(concated);
찍히는 값 = [1, 2, 3, 4, 5, 6];
```

### join

- 배열 안에 있는 원소들을 하나의 문자열로 만들어주는 함수

```jsx
const array = [1, 2, 3, 4, 5];

console.log(array.join());
// 찍히는 값 = 1,2,3,4,5

console.log(array.join(' '));
// 문자열 사이에 공백을 넣어줌
// 찍히는 값 = 1 2 3 4 5

console.log(array.join(', '));
// 문자열 사이에 공백과 콤마를 넣어줌
// 찍히는 값 = 1, 2, 3, 4, 5

```

### reduce

- 배열 연산할 때 사용하는 내장함수로,  reduce 함수에는 2개의 파라미터를 전달, 1번째 파라미터는 accumulator(누적될 값) 와 current 를 파라미터로 가져와서 결과를 반환하는 콜백함수, 2번째 파라미터는 reduce 함수에서 사용 할 초깃값 (누적되기전)이다.

```jsx
const numbers = [1, 2, 3, 4, 5];

const sum2 = numbers.reduce((accumulator, current) => accumulator + current, 0);
console.log(sum2);
// 찍히는 값 = 15
```

- 추가적 설명

reduce 메소드 ( 하나의 값을 반환함.)

4개의 인자를 가질 수 있음.

누산기 ( acc) - 누적되는 값

현재값 (cur)

현재 인덱스 (idx)

원본 배열 (arr) → 별로 의미 없음