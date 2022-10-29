<h1>정규표현식 : Regular Expression</h1>
<p>깃에서 마크다운이 어색해서 가독성이 좋지 않아요, 관련 부분은 후에 수정하겠습니다!</p>
 
<h2>1. 정규표현식 개요</h2>

<h3>개념</h3>
-"특정 패턴의 문자열"을 찾기 위한 표현 방식으로 문자열에서 특정 내용을 찾거나 대체 또는 발췌하는데 사용한다.<br />
-반복문과 조건문을 사용해야 할 것 같은 복잡한 코드도 정규표현식을 이용하면 매우 간단하게 표현 할 수 있다.<br />
-형식 언어, formal languange라 부르기도 한다. <br />

<h3>정규표현식이 유용한 상황</h3>
1. 각각 다른 포맷으로 저장된 엄청나게 많은 전화번호 데이터를 추출해야 할 때<br />
2. 사용자가 입력한 이메일, 휴대폰 번호, IP 주소 등이 올바른지 검증하고 싶을 때<br />
 -> 입력칸에 전화번호나 이메일을 입력하라고 했을때 옳지 않은 값을 입력하면(ex. @와 .문자가 들어가지 않았을 때) 경고창이 뜰 것이다.<br />
    이것이 정규표현식에 의해 필터링되어 걸러져 경고창을 띄우게 되는 것이다.  <br />
3. 코드에서 특정 변수의 이름을 치환하고 싶지만, 해당 변수의 이름을 포함하고 있는 함수는 제외하고 싶을 때<br />
4. 특정 조건과 위치에 따라서 문자열에 포함된 공백이나 특수문자를 제거하고 싶을 때<br />
<hr />

<h2>2. 정규표현식의 사용</h2>

<h3>정규표현식의 형식</h3>

```
/패턴/플래그
```
 
<h3>정규표현식 플래그</h3>
정규식 플래그는 정규식을 생성할 때 고급 검색을 위한 전역 옵션을 설정할 수 있도록 지원하는 기능이다.
<img src='https://github.com/gdsc-ssu/hcj-study/blob/javascript/Regular-Expression-Regex/flag.jpg' width='60%'>

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
<img src='https://github.com/gdsc-ssu/hcj-study/blob/javascript/Regular-Expression-Regex/matching-pattern.jpg' width='60%'>

<h3>정규표현식 검색 패턴</h3>
아래 패턴들을 이용하면, AND, OR, StartWith, EndWith 등의 다양한 조합을 만들 수 있다.
<img src='https://github.com/gdsc-ssu/hcj-study/blob/javascript/Regular-Expression-Regex/search-pattern.jpg' width='60%'>


<h3>정규표현식 갯수(수량) 패턴</h3>
특정 패턴이 몇번 반복되는지도 필터링 가능하다.
<img src='https://github.com/gdsc-ssu/hcj-study/blob/javascript/Regular-Expression-Regex/num-pattern.jpg' width='60%'>

<h3>정규표현식 주요 메서드</h3>
정규표현식을 가지고 이메일이나 전화번호 매칭 필터링을 하기위해선 자바스크립트 정규식 메서드를 이용하여 패턴을 검사하고, 매칭되는 문자열을 추출, 변환한다.
<img src='https://github.com/gdsc-ssu/hcj-study/blob/javascript/Regular-Expression-Regex/method.jpg' width='60%'>

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


