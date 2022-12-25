## 구조 분해 할당이란?

- 구조 분해 할당 구문은 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript 표현식을 의미함.

## 구조 분해 할당의 장점

- 배열 분해를 통해 배열 접근을 하지 않아도 변수로 이름과 성에 접근하면서 코드의 양을 줄일 수 있음.
    
    ```jsx
    //배열 요소를 직접 변수에 할당할 때배열 요소를 구조 분해 할당 방식을 사용할 때
    
    var arr = ["Soyeon", "Hong"];
    
    var [firstName, lastName] = arr;
    
    console.log(firstName); // "Soyeon"
    console.log(lastName); // "Hong"
    ```
    
    ```jsx
    //배열 요소를 직접 변수에 할당할 때
    
    var arr = ["Soyeon", "Hong"];
    
    var firstName = arr[0];
    var lastName = arr[1];
    
    console.log(firstName); // "Soyeon"
    console.log(lastName); // "Hong"
    ```
    

## 배열에서의 구조 분해 할당

- 기본 변수 할당
    
    ```jsx
    var arr = [1, 2, 3];
    
    var [a, b, c] = arr;
    
    console.log(a); // 1
    console.log(b); // 2
    console.log(c); // 3
    ```
    
- 변수 선언이 된 후 할당
    
    선언이 분리되어 있어도 값 할당이 가능
    
    ```jsx
    var a, b, c;
    
    [a, b, c] = [1, 2, 3];
    
    console.log(a); // 1
    console.log(b); // 2
    console.log(c); // 3
    ```
    
- 기본값
    
    변수에 값을 할당하게 되면 기존에 있던 값보다 할당되는 값을 우선으로 한다.
    
    ```jsx
    var a, b;
    
    [a=5, b=7] = [1];
    
    console.log(a); // 1 (5였던 a값이 1로 바뀜)
    console.log(b); // 7
    ```
    
- 함수가 반환한 배열
    
    함수에서 반환되는 배열도 구조 분해 할당이 가능
    
    ```jsx
    function arr() {
      return [1, 2, 3];
    }
    
    var a, b, c;
    
    [a, b, c] = arr();
    
    console.log(a); // 1
    console.log(b); // 2
    console.log(c); // 3
    ```
    
- 변수 값 교환
    
    변수에 저장되어 있는 값을 교환할 때, 임시 변수가 없어도 가능하다는 장점을 갖고 있음.
    
    ```jsx
    var a = 1;
    var b = 2;
    var c = 3;
    
    [a, b, c] = [b, a, c]
    
    console.log(a); // 2
    console.log(b); // 1
    console.log(c); // 3
    ```
    
- 변수에 배열의 나머지 할당
    
    ‘…’을 사용하여 나머지 부분을 할당할 수 있음. ‘…’뒤에는 더이상 변수를 넣으면 안됨.
    
    ```jsx
    var [a, ...b] = [1, 2, 3];
    console.log(a); // 1
    console.log(b); // [2, 3]
    ```
    
- for of 반복문을 이용한 구조 분해
    
    for of 명령문은 배열의 요소를 분해할당 할 수 있음. 
    
    ```jsx
    var home = [
    	{
    		name: "Hong Soyeon",
    		family: {
    			mom: "Lee mother",
    			dad: "Hong Gildong",
    			sister: "Hong Siyeon"
    		},
    		age: 23
    	},
    	{
    		name: "Kim mina",
    		family: {
    			mom: "Kim mother",
    			dad: "Kim Gildong",
    			sister: "Kim Siyeon"
    		},
    		age: 25
    	}
    ];
    
    for ( var { name: n, family: { dad: d } }  of home){
    	console.log("name: " + n + ", dad: " + d);
    }
    ```
    

## 객체에서의 구조 분해 할당의 경우 할당의 기준은 순서가 의미 없으며, 선언된 변수 이름과 프로퍼티 키가 일치하면 할당됨.

- 기본할당
    
    ```jsx
    var object = {a: 1, b: 2};
    var {a, b} = object;
    
    console.log(a); // 1
    console.log(b); // 2
    ```
    
- 변수 선언이 된 후 할당
    
    변수 선언과 할당을 분리해서 가능
    
    ```jsx
    var a, b, c;
    
    ({a, b, c} = {a: 1, b: 2, c:3});
    
    console.log(a); // 1
    console.log(b); // 2
    console.log(c); // 3
    ```
    
- 새로운 변수로 할당
    
    객체로부터 속성을 해체하여 원래 속성명과 다른 이름의 변수에 할당 가능
    
    ```jsx
    var object = {a: 1, b: 2, c: 3};
    var {a: one, b: two, c: three} = object;
    
    console.log(one); // 1
    console.log(two); // 2
    console.log(three); // 3
    ```
    

## 추가 예외 예시

- String을 분할 한다면?
    
    구조 분해 할당은 배열뿐만 아니라 모든 이터러블(반복 가능한 객체)에 적용 가능
    
    ```jsx
    var [a, b, c] = "123"; // ["1", "2", "3"]
    
    console.log(a); // "1"
    console.log(b); // "2"
    console.log(c); // "3"
    ```
    
- 일부 반환 값을 무시하고 싶다면?
    
    필요하지 않은 반환값은 공백으로 두어 값을 무시할 수 있음
    
    ```jsx
    var a, b;
    
    [a, , b] = [1, 2, 3];
    
    console.log(a); // 1
    console.log(b); // 3
    ```
    
- 변수의 갯수가 배열 요소의 갯수보다 작다면?
    
    첫번째 인덱스부터 차례대로 변수에 할당됨.
    
    ```jsx
    var a, b;
    
    [a, b] = [1, 2, 3];
    
    console.log(a); // 1
    console.log(b); // 2
    ```
    
- 변수의 갯수가 배열 요소의 갯수보다 크다면?
    
    에러가 발생되지는 않지만 할당되지 못한 변수는 ‘undefined’로 표시됨. 
    
    ```jsx
    var a, b, c, d;
    
    [a, b, c, d] = [1, 2, 3];
    
    console.log(a); // 1
    console.log(b); // 2
    console.log(c); // 3
    console.log(d); // undefined
    ```
    

## 참고자료

- [https://ko.javascript.info/destructuring-assignment](https://ko.javascript.info/destructuring-assignment)
- [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [https://www.youtube.com/watch?v=-3QmIXIEWkk](https://www.youtube.com/watch?v=-3QmIXIEWkk)
- [https://intrepidgeeks.com/tutorial/instruction-javascript-nested-repeated-statements-for-in-for-of-arrays-array-methods-functions](https://intrepidgeeks.com/tutorial/instruction-javascript-nested-repeated-statements-for-in-for-of-arrays-array-methods-functions)