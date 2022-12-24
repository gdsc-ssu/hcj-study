# sort

자바스크립트의 배열의 요소를 정렬하는 메소드 `sort()`

<br>

## 1. 사용 방법

재밌는 점은 전달받은 배열도 정렬되고, 반환된 배열도 정렬되어 있다는 점이다. 이는 아래 코드를 통해 확인할 수 있다.

```jsx
const array1 = [4, 3, 2, 1];
const array2 = array1.sort();
console.log(array1);  // Array [1, 2, 3, 4]
console.log(array2);  // Array [1, 2, 3, 4]
```

<br>

만약 기존의 배열을 그대로 유지하고, 반환된 배열만 정렬되도록 만들고 싶다면 구조분해할당(…)을 이용하면 된다.

```jsx
const array1 = [4, 3, 2, 1];
const array2 = [...array1].sort();
console.log(array1);  // Array [4, 3, 2, 1]
console.log(array2);  // Array [1, 2, 3, 4]
```

<br>

하지만 위 `sort()` 메소드를 아무런 인자를 넘겨주지 않고 정렬하게 될 경우 사용자가 의도한대로 정렬이 되지 않을 수 있다. 그 예시가 MDN 문서 예시에도 나와있다. (애초에 `sort()`만 쓴 경우에는 오름차순 밖에 되지 않지만..ㅎ)

```jsx
const array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1); // Array [1, 100000, 21, 30, 4]
```

100000이 21보다 작다는 결과가 나오는 이유는 MDN에 나오는 `sort()` 메소드의 파라미터와 이에 대한 설명을 보면 이해할 수 있다.

```jsx
// context
arr.sort([compareFunction])
```

<br>

`sort()` 메소드는 `compareFunction` 이 제공되지 않으면 배열의 요소를 문자열로 변환하고 유니코드 코드 포인터 순서로 문자열을 비교하여 정렬**된다. 그렇기 때문에 100000이 21보다 작다는 결과가 도출되는 것이다..!

이제 의도한대로 배열을 정렬하기 위해 `sort()` 메소드의 파라미터로 전달되는 콜백함수 `compareFunction` 을 사용하는 방법에 대해 알아보자. `sort()` 메소드는 `**compareFunction`이 제공되면 배열 요소는 해당 함수의 반환 값에 따라 정렬**된다. 반환되는 값의 부호에 따라 다르게 정렬이 이뤄지는데, 동작 방식은 다음과 같다.

- `compareFunction(a, b) < 0` 인 경우, a를 b보다 낮은 색인으로 정렬
- `compareFunction(a, b) > 0` 인 경우, a를 b보다 높은 색인으로 정렬
- `compareFunction(a, b) === 0` 인 경우, 변경 X

<br>

### 응용

자바스크립트 Array 자료구조의 요소에는 어떤 타입이든 올 수 있다. 예시를 통해 다양한 방법으로 `sort()` 메소드를 응용하는 방법에 대해 알아보자

우선 기본적으로 위 예제에서 사용했던 요소가 Number인 배열을 오름차순으로 정렬하는 방법이다.

```jsx
const array1 = [1, 30, 4, 21, 100000];

function compareNumbers(a, b) {
  return a - b;
}

array1.sort(compareNumbers); // or array1.sort((a, b) => a - b);
console.log(array1); // Array [1, 4, 21, 30, 100000]
```

콜백함수 `compareNumbers`를 외부에서 정의해서 사용할 수 있으며, `sort()` 메소드 내에 로직을 작성해도 된다. 만약 내림차순을 원한다면 반환값을 `b - a` 로 변경하면 된다.

조금 더 응용해서 요소가 객체 구조인 경우, 객체의 특정 프로퍼티 값을 기준으로 정렬하는 방법이다.

```jsx
const items = [
  { name: 'Edward', value: 21 },
  { name: 'Sharpe', value: 37 },
  { name: 'And', value: 45 },
  { name: 'The', value: -12 },
  { name: 'Magnetic', value: 13 },
  { name: 'Zeros', value: 37 }
];

// sort by value
items.sort((a, b) => a.value - b.value);

// sort by name
items.sort((a, b) => {
  const nameA = a.name.toUpperCase(); // ignore upper and lowercase
  const nameB = b.name.toUpperCase(); // ignore upper and lowercase
  if (nameA < nameB) {
    return -1;
  }
  if (nameA > nameB) {
    return 1;
  }

  return 0;
});
```

한번은 `value` 로, 다른 한번은 `name` 으로 객체 요소들이 정렬되도록 구현한 예제이다.

<br>

## 2. 내부 동작 원리

위에서 `sort()` 메소드의 사용 방법을 알아봤다면, 이젠 `sort()` 메소드가 어떤 알고리즘을 기반으로 동작하는 지 간단하게 알아보자. (왜냐? 궁금하니까!)

이를 공부하며 알게된 재밌는 점은 브라우저 환경에 따라 다양한 자바스크립트 엔진을 사용한다는 자바스크립트 특성 상, 엔진의 종류에 따라 `sort()` 메소드의 구현 방식이 다를 수 있다는 것이다..!! ([관련 링크](https://stackoverflow.com/questions/234683/javascript-array-sort-implementation))

그렇다면 대표적인 자바스크립트 엔진인 v8에서의 구현 방식에 대해서 간단하게 알아보자.

<br>

### v8

v8에서의 `sort()` 메소드에 대한 구현 코드는 [v8 github](https://github.com/v8/v8/blob/main/third_party/v8/builtins/array-sort.tq)에서 볼 수 있으며, [Tim Sort](https://d2.naver.com/helloworld/0315536)를 사용하는 것을 확인할 수 있다. (Tim Sort 알고리즘은 Java와 Python에서도 사용된다고 한다)

<br>

## 참고자료

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort
- https://stackoverflow.com/questions/234683/javascript-array-sort-implementation
- https://github.com/v8/v8/blob/main/third_party/v8/builtins/array-sort.tq

