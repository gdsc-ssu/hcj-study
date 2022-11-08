## Event

### 자주 사용되는 DOM 이벤트 모음

다양한 DOM 이벤트들이 존재하지만, 주로 사용되는 이벤트들을 살펴보자.

- 마우스 이벤트
  - `click` : 요소 위에서 마우스 왼쪽 버튼 클릭
  - `contextmenu` : 요소 위에서 마우스 오른쪽 버튼 클릭
  - `mouseover` : 마우스 커서 요소 위로 이동
  - `mouseout` : 마우스 커서 요소 밖으로 이동
  - `mousedown` : 요소 위에서 마우스 왼쪽 버튼 누르고 있을때
  - `mouseup` : 요소 위에서 마우스 버튼 뗄 때
  - `mousemove` : 마우스 움직일때
- 폼 이벤트

  - `submit` : 사용자가 <form> 을 제출할때.
  - `focus` : 사용자가 <input> 같은 요소에 포커스 할때
  - `blur` : 요소에서 포커스가 해제될때
  - `input` : <input> 이나 <textarea> 요소 값이 변경되었을 때
  - `change` : select-box, check-box, radio-button 등의 값이 변경되었을 때

- 키보드 이벤트

  - `keydown` , `keypress` : 사용자가 키보드 버튼 누를때

  - `keyup` : 사용자가 키보드 버튼 뗄 때

    > keydown 와 keypress 의 차이
    >
    > - keydown 는 모든 키보드 버튼을 인식한다. 버튼을 누르고 있으면 계속 실행된다.
    > - keypress 는 enter, shift 등을 제외한 텍스트를 입력할 수 있는 버튼을 인식한다. 버튼을 누르고 있으면 한번만 실행된다. 이 이벤트는 deprecated 되었으므로 사용을 권장하지 않는다.
    >
    > - keydown -> keypress -> keyup 순으로 발생한다.

- 문서 및 UI 이벤트

  - `DOMContentLoaded` : HTML이 전부 로드되어 DOM 트리 생성이 완료되었을 때

  - `load` : DOM 트리 생성되고, 외부 리소스(이미지, 외부 script 등) 도 모두 로드되었을 때

    > DomContentLoaded 가 load 보다 항상 먼저 발생된다.

  - `unload` : 페이지에서 이탈할 때 (새로운 페이지로 이동)
  - `resize` : 브라우저 창의 크기를 조절할때
  - `scroll` : 사용자가 페이지를 위 아래로 스크롤할때

- CSS 이벤트

  - `transitioned` : CSS 에니메이션이 종료되었을 때

- Clipboard 이벤트
  - `copy` : 컨텐츠를 복사할때
  - `paste` : 컨텐츠를 붙여넣기할때

더 많은 DOM 이벤트들은 [이 링크](https://www.w3schools.com/jsref/dom_obj_event.asp) 에서 확인할 수 있다.

### 이벤트 핸들러

HTML 요소에 이벤트를 할당하는 방법에는 여러 가지가 있다.

1. HTML `on<event>` 속성 이용하기

   ```html
   <input onclick="console.log('클릭')" type="button" />
   ```

 onclick 속성값 내에 큰따옴표가 들어가지 않도록 주의하자.

2. DOM 프로퍼티 사용하기

   ```html
   <input id="btn" type="button" />
   <script>
     btn = document.getElementById('btn');
     btn.onclick = function () {
       console.log('클릭');
     };
   </script>
   ```

 만약 중간에 이벤트를 제거하고 싶다면 btn.onClick = null 같이 null을 할당하면 된다.

3. **addEventListener** 사용하기

 HTML 속성과 DOM 프로퍼티를 이용한 이벤트 핸들러 할당 방식에는 복수의 핸들러를 할당할 수 없다는 단점이 있다. 따라서 여러 개의 이벤트를 할당하고 싶다면 `addEventListener` 라는 특별한 메서드를 이용하면 된다.

```javascript
element.addEventListener(event, handler, [options]);
```

- event : 이벤트 이름 (click, mouseoever 등)
- handler : 핸들러 함수
- options
  - `once` : true이면 이벤트가 트리거될때 리스너가 자동으로 삭제.
  - `capture` : 어느 단계에서 이벤트를 다뤄야하는지 알려주는 프로퍼티
  - `passive` : true면 리스너에서 지정한 함수가 `preventDefault()` 를 호출하지 않음

### 이벤트 객체

이벤트가 발생하면 브라우저는 event object 을 생성한다. 이 객체에는 이벤트에 관한 상세한 정보가 담겨지고, 이를 핸들러에 인수 형태로 전달한다.

```js
element.addEventListener('click', function (event) {
  console.log(event.type); // event 대신 e를 사용해도 된다.
});
```

<img width="529" alt="스크린샷 2022-11-07 15 27 45" src="https://user-images.githubusercontent.com/67703882/200240272-abbd9749-81b3-4e5e-a1bb-25fb27fde49b.png" style="zoom:70%;" >

event 객체를 console에 찍어보면 객체 내에 다양한 정보가 담겨있음을 알 수 있다.

다음은 자주 사용되는 이벤트 객체의 프로퍼티들이다.

- `event.target` : 이벤트를 발생시킨 요소

- `event.currentTarget` : 이벤트에 바인딩된 DOM 요소

  > div 요소에 클릭 이벤트를 걸어놨는데, div 내에 button 요소가 있다고 하자. button 영역과 div 영역 모두 동일한 클릭 이벤트가 발생할 것이다.
  >
  > 그러나 만약 button을 클릭하여 이벤트가 발생했을 때, event.currentTarget 을 찍어보면 div 가 나오고, event.target을 찍으면 button이 나온다. 이벤트를 발생시킨건 button 요소이지만, 이벤트가 바인딩되어 있는건 div 요소이기 때문이다.

- `event.type` : 이벤트 종류를 문자열로 나타냄

- `event.clientX` , `event.clientY` : 클라이언트 영역 내 이벤트가 발생한 커서 위치. 스크롤은 고려되지 않고, 해당 페이지의 상단을 0으로 두고 시작한다.

- `event.offsetX` , `event.offsetY` : 이벤트 대상 기준 이벤트 발생 커서 위치 (만약 박스 내부에서 클릭 이벤트가 발생했을 경우, 해당 박스의 왼쪽 모서리 좌표가 0이 된다.)

- `event.pageX` , `event.pageY` : 뷰포트 기준 이벤트 발생 커서 위치. 스크롤 포함한다. (IE8 이전 지원X)

- `event.screenX` , `event.screenY` : 모니터 화면 기준 커서 위치

  ![image](https://user-images.githubusercontent.com/67703882/200263701-b3e7b7c0-b78f-4a4e-afc1-58053e1d3af8.png)

- `key` : 키보드 이벤트를 사용했을 경우, 어떤 키보드 버튼을 눌렀는지. 아래 링크에서 키 정보를 자세히 알 수 있다.

   https://www.toptal.com/developers/keycode
