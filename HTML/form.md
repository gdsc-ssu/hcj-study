# form 태그

html <form>태그는 웹페이지에서의 입력양식을 의미

ex) 로그인 창, 회원가입폼 (텍스트 필드에 글자를 입력하거나, 체크박스나 라디오 버튼을 클릭하고 제출 버튼을 누르면 벡엔드 서버에 양식이 전달되어 정보를 처리하게 된다.)

### <form> 태그의 속성

- 속성

**action** - 전송한 데이터를 보낼 웹페이지의 url
**autocomplete** - 사용자가 전에 적었던 내용을 자동완성 할 것인지 구분 (기본적으로 on)
**name** - 고유한 양식의 이름
**target** - 새로운 브라우저에 띄울지, 기존 페이지에 띄울지 (_blank, _self)
**method** - 서버로 전송할 http방식 (GET과 POST가 존재)
**novalidate** - 서버로 전송시 양식 데이터의 유효성을 검사하지 않도록 지정 ( 지정한 방식을 검사하지 않는다.)

### <input> 태그

<form>태그는 전체 양식을 의미하며, 화면에 보이지 않는 추상적인 태그이다. 실질적으로 사용자가 양식을 입력하기 위한 태그는 <input>태그 등이 사용된다.

- 속성

**autofocus** - 자동으로 입력되는 부분이 포커스됨 (한 번밖에 사용불가능)
**form** - form 속성은 input태그가 form 태그 밖에 있을 경우, form태그의 id값을 input태그의 form속성에 작성해주면 안에 form태그 안에 있는 역할을 하게 된다.
**maxlength** - 최대 글자수
**placeholder** - 사용자에게 데이터입력의 힌트를 주는 속성
**checked** - 체크가 되어져 있음
**multiple** - 여러개의 파일을 집어넣을 수 있음.
**name** - 데이터의 이름을 입력 (필수)
**type** - 입력받을 데이터의 종류

type 속성에 입력할 수 있는 값
— button - <button>태그와 같음.
— checkbox - 체크가 가능함. (동의, 비동의)
— email
— file
— password
— submit - 제출 버튼
— text
— image ( 이미지를 삽입해 이미지 제출도 가능함. src 속성과 alt 속성도 작성해줘야함.)
— radio (checkbox와 유사하지만 조금 다름. 여러개 중 하나를 선택할 때 사용가능한 값) - 고유해야 하므로 name을 하나로 통일해서 같은 데이터임을 표시해줘야함.
— reset 초기화 버튼

### 예시

```jsx
<form>
	<p>
		<strong>아이디</strong>
		<input type="text" name="name" value="아이디 입력">
	</p>
	<p>
		<strong>비밀번호</strong>
		<input type="password" name="password" value="비밀번호 입력">
	</p>
	<p>
		<strong>성별</strong>
		<input type="radio" name="gender" value="M">남자
		<input type="radio" name="gender" value="F">여자
	</p>
	<p>
		<strong>응시분야</strong>
		<input type="checkbox" name="part" value="eng">영어
		<input type="checkbox" name="part" value="math">수학
	</p>
	<p>
		<input type="submit" value="제출">
	</p>
</form>
```

### <button> 태그

선택가능한 버튼을 생성

- 속성

**autofocus** - 자동으로 포커스가 지정되며 문서내에 고유해야함.
**form** - form태그안에 있지않을 경우, 해당 form태그의 id값을 작성
**type** - 버튼의 역할 종류

— button(일반적인 버튼, 기본적으로 javascript로 기능을 추가한다 대부분)

— reset(초기화를 위한 버튼)

— submit(다른 페이지로 데이터를 보내는 버튼)

input도 버튼기능을 나타낼 수 있지만 차이점은 코드내용에 차이점이 있다. (둘 다 같은 버튼 기능을 한다.)
ex) <input type: “reset”  value:”초기화" >
<button type:”reset” > 초기화 </button>

### 예시

```jsx
<button type="submit" value="Submit">Submit</button>
    <button type="reset" value="Reset">Reset</button>
    <button type="button" value="Button">click</button>
```

### <select>,<option>태그

<select> 및 <option>은 드롭다운 리스트를 만드는 태그이다.

<select>태그는 <option>태그를 항상 감싸고 있어야 한다.

### 예시

```jsx
<select>
	<option value="ktx">KTX</option>
	<option value="itx">ITX 새마을</option>
	<option value="mugung">무궁화호</option>
</select>
```