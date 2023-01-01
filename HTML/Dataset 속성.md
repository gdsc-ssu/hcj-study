# Dataset 속성

### Dataset 이란

HTML태그들의 속성명은 전부 지정되어 있다. 하지만 사용하다보면 개발자들이 속성을 만들고 싶을때가 있는데 그때 사용하는 것이 dataset 속성이다.

HTML5 에서 새로 확장된 속성으로 사용자가 해당 요소에 커스텀 속성을 추가한 객체이다.

"data-*" 어트리뷰트로 표기하며, HTML5 표준 속성처럼 접근할 수 있다.

HTML에 추가의 속성이나 데이터를 표기하는 표준이 없어 비표준적인 방법으로 데이터를 표기하던 라이브러리들이 표준적인 방법을 사용할 수 있도록 개선되었으며, 자바스크립트 또한 표준화된 DOM 메서드로 데이터셋 속성에 접근할 수 있다.

### Da**taset 사용법**

```html
<태그명 data-*="값"></태그명>
```

- data-뒤에 붙는 이름은 대문자를 포함할 수 없다.
1. HTML 태그에 접두어(data-)가 붙은 속성을 추가하고, 거기에 사용하고자 하는 값을 지정해놓는다.
2. 자바스크립트에서 요소를 선택하고, dataset 객체에서 커스텀속성을 읽어들인다.
3. 추가적으로 css에서도 속성 선택자로 선택이 가능하다.

=> dataset 속성의 값은 개수 제한이 특별히 없다.

### 사용예시

- html 사용예시

```html
<img src="image/1.jpg" id="images">
<ul data-name="내 목록">
	<li class="list" data-image="image/1.jpg">1번 사진</li>
	<li class="list" data-image="image/2.jpg">2번 사진</li>
	<li class="list" data-image="image/3.jpg">3번 사진</li>
</ul>
```

- js 사용예시

```jsx
const list = document.querySelector("ul")
console.log(list.getAttribute('data-name')). //여기서 사용되는 dataset은 커스텀 속성을 모아놓은 객체이다.
// 출력 : 내 목록
```

```jsx
let items = document.querySelectorAll(".list")
// items는 배열이 된다.
for(let i=0; i<items.length; i++){
	items[i].onclick=function(){
		let image = this.getAttribute('data-image')
		doucument.querySelector("images").src = img
}

// 출력 : 1번사진, 2번 사진, 3번사진 list를 클릭하면 거기에 맞는 사진으로 변경된다.
```

- css 사용예시

```css
li[data-image="image/1.jpg"]{width:100px;}
li[data-image="image/2.jpg"]{width:200px;}
li[data-image="image/3.jpg"]{width:300px;}
```

### dataset의 속성 (중요)

자바스크립트는 dataset속성을 통해 사용자정의 속성값에 쉽게 다가갈 수 있다.

하지만 이 방법은 ie11이상에서만 사용 가능하므로, 크로스브라우징시 주의 해야한다.

```jsx
//문법
문서객체선택.dataset.속성명
문서객체선택.dataset[속성명]
```

### 코드예시

```jsx
const list = document.querySelector("ul")
console.log(list.dataset.name)

let items = document.querySelectorAll(".list")
// items는 배열이 된다.
for(let i=0; i<items.length; i++){
	items[i].onclick=function(){
		let image = this.dataset.image
		doucument.querySelector("images").src = img
}
```