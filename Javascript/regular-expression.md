<h1>정규표현식 : Regular Expression</h1>
<p>깃에서 마크다운이 어색해서 가독성이 좋지 않아요, 관련 부분은 후에 수정하겠습니다!</p>
 
<hr />

<h2>1. 정규표현식 개요</h2>

<h3>개념</h3>
-"특정 패턴의 문자열"을 찾기 위한 표현 방식으로 문자열에서 특정 내용을 찾거나 대체 또는 발췌하는데 사용한다.<br />
-반복문과 조건문을 사용해야 할 것 같은 복잡한 코드도 정규표현식을 이용하면 매우 간단하게 표현 할 수 있다.<br />
-형식 언어, formal languange라 부르기도 한다. <br />

<h3>정규표현식이 유용한 상황</h3>
1. 각각 다른 포맷으로 저장된 엄청나게 많은 전화번호 데이터를 추출해야 할 때<br />
2. 사용자가 입력한 이메일, 휴대폰 번호, IP 주소 등이 올바른지 검증하고 싶을 때<br />
 -> 입력칸에 전화번호나 이메일을 입력하라고 했을때 옳지 않은 값을 입력하면 경고창이 뜰 것이다.<br />
    이것이 정규표현식에 의해 필터링되어 걸러져 경고창을 띄우게 되는 것이다.  <br />
 
 ```js
 // 회원가입 할때 휴대폰번호 양식 검사
// 예를 들어 010-1111-2222 라는 전호번호는
// "숫자3개", "-", "숫자4개", "-", "숫자4개" 로 이루어져 있는데,
 
const regex = /\d{3}-\d{4}-\d{4}/; 
// (\d는 숫자를 의미하고, {} 안의 숫자는 갯수를 의미한다.) 
 
regex.test('010-1111-2222') // true; 
regex.test('01-11-22') // false;
```

3. 코드에서 특정 변수의 이름을 치환하고 싶지만, 해당 변수의 이름을 포함하고 있는 함수는 제외하고 싶을 때<br />
4. 특정 조건과 위치에 따라서 문자열에 포함된 공백이나 특수문자를 제거하고 싶을 때<br />
<hr />

<h2>2. 정규표현식의 생성</h2>
<h3>리터럴(Literal) 방식</h3>
정규 표현식은 /로 감사진 패턴을 리터럴로 사용한다.

```
리터럴(Literal)이란? 리터럴은 데이터 그 자체를 뜻하며, 변수에 넣는 변하지 않는 데이터를 의미한다. 리터럴은 변수의 값이 변하지 않는 데이터를 의미한다. (메모리 위치안에 값)
주의! 상수와는 다른 의미이다. 상수는 변하지 않는 변수를 의미한다. (메모리 위치)
```

```js
// 정규 표현식의 리터럴 표현 방법
const regexp1 = /^abc/;  // --> /패턴/
const regexp2 = /^abc/gi; // --> /패턴/플래그
```

<h3>RegExp 생성자 함수 방식</h3>
RegExg 생성자 함수를 호출하여 RegExp 객체를 생성할 수도 있다.

```js
const regexp1 = new RegExp(/^abc/i); // ES6
const regexp2 = new RegExp(/^abc/, 'i');
const regexp3 = new RegExp('^abc', 'i');
```

<h3>재할당 방식(Re-compile)</h3>
사용중인 정규 표현식을 재할당할 수도 있다. 단, 상수가 아닌 변수로 선언해야한다.

```js
let regexp1 = /ipsum/g;
regexp1 = /lorem/i;
console.log(regexp1); // --> /lorem/i
const regexp2 = /ipsum/g;
regexp2 = /lorem/i;  // --> TypeError
```

<hr />

<h2>3. 정규표현식의 사용</h2>
 
<h3>정규표현식 플래그</h3>
정규식 플래그는 정규식을 생성할 때 고급 검색을 위한 전역 옵션을 설정할 수 있도록 지원하는 기능이다.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/104986866/200372416-18faa888-1165-46f2-b443-cc9ff7403dec.jpg" style="zoom:200%;" >

```javascript
// flags 에 플래그 문자열이 들어간다.
cosnt flags = 'i';
const regex = new RegExp('abapplec', flags);
 
// 리터럴로 슬래쉬 문자뒤에 바로 표현이 가능
const regex1 = /apple/i;
const regex2 = /apple/gm;
```

<h3>정규표현식 매칭 패턴</h3>
정규식 특정 문자 숫자 매칭 패턴으로 아래 매칭 패턴을 사용하면, 훨씬 쉽게 문자/숫자/기호를 표현할 수 있다.
<p>특징</p>
+패턴은 /로 열고 닫으며, 문자열의 따옴표는 생략한다.<br />
+따옴표를 포함하면 따옴표까지도 패턴에 포함되어 검색된다.<br />
+패턴은 특별한 의미를 가지는 메타문자 또는 기호로 표현 가능하다.<br />
+어떤 문자열 내에 패턴과 일치하는 문자열이 존재할 때, ‘정규 표현식과 매치한다’고 표현한다.<br />
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/104986866/200372420-1364e9bd-cdac-4a80-9e4e-bbd4fe1b8d7a.jpg" style="zoom:200%;" >

<h3>정규표현식 검색 패턴</h3>
아래 패턴들을 이용하면, AND, OR, StartWith, EndWith 등의 다양한 조합을 만들 수 있다.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/104986866/200372426-be6936e8-874f-446f-a268-6eea3e30649e.jpg" style="zoom:200%;" >


<h3>정규표현식 갯수(수량) 패턴</h3>
특정 패턴이 몇번 반복되는지도 필터링 가능하다.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/104986866/200372425-20778dc5-7f4f-4196-8dd3-dc5514a6ac00.jpg" style="zoom:200%;" >

<h3>정규표현식 주요 메서드</h3>
정규표현식을 가지고 이메일이나 전화번호 매칭 필터링을 하기위해선 자바스크립트 정규식 메서드를 이용하여 패턴을 검사하고, 매칭되는 문자열을 추출, 변환한다.

주의! exec 메서드는 문자열 내의 모든 패턴을 검색하는 g 플래그를 지정해도 첫 번째 매칭 결과만 반환해준다.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/104986866/200372424-f4249940-5fd2-4e6e-a319-2876ec78febb.jpg" style="zoom:200%;" >

```javascript
// 정규표현식을 담은 변수
const regex = /apple/; // apple 이라는 단어가 있는지 필터링
 
// "문자열"이 "정규표현식"과 매칭되면 true, 아니면 false반환
regex.test("banana and apple"); // true
 
// "문자열"에서 "정규표현식"에 매칭되는 항목들을 배열로 반환
const txt = "banana and apple is fruit";
txt.match(regex); // ['apple']
 
// "정규표현식"에 매칭되는 항목을 "대체문자열"로 변환
txt.replace(regex, "watermelon"); // 'banana and watermelo'
```

<hr />
<h2>4. 정규표현식 예제</h2>

```js
const form = document.querySelector('#form')
const input = document.querySelector('#phone')
const output = document.querySelector('#output')

const re = /^(?:\d{3}|\(\d{3}\))([-\/\.])\d{4}\1\d{4}$/

function testInfo(phoneInput) {
  const ok = re.exec(phoneInput.value)

  if (!ok) {
    output.textContent = `형식에 맞지 않는 전화번호입니다. (${phoneInput.value})`
  } else {
    output.textContent = `감사합니다. 전화번호는 ${ok[0]} 입니다.`
  }
}

form.addEventListener('submit', (event) => {
  event.preventDefault()
  testInfo(input)
})
```

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/104986866/200372408-66f920cb-4654-47fb-8ffb-c05f827ef149.jpg" style="zoom:200%;" >
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/104986866/200372415-b2f7b5ba-58e4-4671-9770-2ef103329568.jpg" style="zoom:200%;" >


<p>참조</p>
https://hanamon.kr/javascript-%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%EA%B0%9C%EB%85%90%ED%8E%B8/
https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Regular_Expressions
https://curryyou.tistory.com/234
https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%A0%95%EA%B7%9C%EC%8B%9D-RegExp-%EB%88%84%EA%B5%AC%EB%82%98-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-%EC%89%BD%EA%B2%8C-%EC%A0%95%EB%A6%AC
