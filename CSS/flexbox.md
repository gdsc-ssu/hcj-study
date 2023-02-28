# Flexbox

- Container 에 여러개의 item 배치를 개발자가 쉽게 컨트롤할수 있도록 도와주는 것
- 각 아이템의 height 를 동일하게 하거나 각 아이템의 간격을 동일하게 하는 작업을 좀 더 편하게 수행할 수 있음
- 반응형 웹 디자인을 가능하게 해줌!

## Flexbox 구성 요소

<aside>
💡 flex container와 flex item에는 서로 적용할 수 있는 CSS 속성이 다름!

</aside>

- 하나의 Flex Container
    - flex-direction
    - justify-content
    - align-items 등

</br>

- 여러개의 Flex Item
    - flex
    - align-self
    - order 등

## Main/Cross Axis

- flexbox를 원하는대로 제어하려면, axis의 개념에 대해서 정확히 이해해야 함
- main/cross axis에 따라 CSS 속성이 좌우 또는 상하로 적용될 수 있기 때문!
    - main axis는 여러 개의 flex item이 **순서대로 배치되는 방향**
    - cross axis는 **main axis와 수직을 이루는 방향**

### main axis

- flex container의 flex-direction 속성에 의해서 결정되며, 기본값은 row 임

<aside>

>💡 따라서, flex-container 내의 flex item은 **왼쪽부터 오른쪽 방향** 으로 배치됨!

</aside>

- 만약 flex-direction 속성을 ‘**column으로 설정’** 한다면, main axis는 위에서 아래로 내려오는 방향이 됨!

### justify-content

- flex item을 main axis를 기준으로 어떻게 정렬할지를 결정하는 속성

</br>

- 기본 값은 `flex-start`
    - flex item을 main axis의 맨 앞으로 정렬해줌
    - 즉, `flex-direction` 속성이 `row`라면 좌측 정렬
    - `flex-direction`속성이 `column`이라면 상단 정렬

</br>

- 속성 값
    - flex-end
    - center
    - space-between
    - space-evenly
    - space-around

</br>

- 속성 예제

```html
<div class="container">
  <div class="item orange">A</div>
  <div class="item green">B</div>
  <div class="item blue">C</div>
</div>
<div class="container" style="justify-content: flex-end;">
  <div class="item orange">A</div>
  <div class="item green">B</div>
  <div class="item blue">C</div>
</div>
<div class="container" style="justify-content: center;">
  <div class="item orange">A</div>
  <div class="item green">B</div>
  <div class="item blue">C</div>
</div>
<div class="container" style="justify-content: space-between;">
  <div class="item orange">A</div>
  <div class="item green">B</div>
  <div class="item blue">C</div>
</div>
<div class="container" style="justify-content: space-evenly;">
  <div class="item orange">A</div>
  <div class="item green">B</div>
  <div class="item blue">C</div>
</div>
```

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
}

.container {
  display: flex;
  flex-direction: row;
  border: 5px solid red;
}

.item {
  color: white;
  font-size: 48px;
  padding: .5em;
  text-align: center;
}

.orange {
  background: orange;
}

.green {
  background: green;
}

.blue {
  background: blue;
}
```
<img width="40%" height="40%" src="https://user-images.githubusercontent.com/109334968/200325424-532cccdb-331c-4ece-9884-f9a0a0c3c7e8.png">


### align-items

- 속성은 flex item을 cross axis를 기준으로 어떻게 정렬할지를 결정
  
</br>

- 기본값은 `stretch`
    - flex item을 flex container의 높이 또는 너비만큼 늘려줌
    - `flex-direction`속성이 `row`라면 높이 만큼 늘어남
    - `flex-direction` 속성이 `column`이라면 너비만큼 늘어남
    
    <aside>
    </br>

    >⚠️ `flex-direction`속성이 `row`일 때는 상하로 공백이 생기도록 `height` 속성을 지정해주지 않으면 아무 효과가 나타나지 않을 수 있음!
    
    </aside>

- 속성 값
    - center
    - flex-start
    - flex-end
    - baseline 등

</br>
- 속성 예제

```html
<div class="container">
  <div class="item orange">A</div>
  <div class="item green">B</div>
  <div class="item blue">C</div>
</div>
<div class="container" style="align-items: center;">
  <div class="item orange">A</div>
  <div class="item green">B</div>
  <div class="item blue">C</div>
</div>
<div class="container" style="align-items: flex-start;">
  <div class="item orange">A</div>
  <div class="item green">B</div>
  <div class="item blue">C</div>
</div>
<div class="container" style="align-items: flex-end;">
  <div class="item orange">A</div>
  <div class="item green">B</div>
  <div class="item blue">C</div>
</div>
```

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
}

.container {
  display: flex;
  flex-direction: row;
  border: 5px solid red;
  height: 25vh;
}

.item {
  color: white;
  font-size: 48px;
  padding: .5em;
  text-align: center;
}

.orange {
  background: orange;
}

.green {
  background: green;
}

.blue {
  background: blue;
}
```
<img width="40%" height="40%" src="https://user-images.githubusercontent.com/109334968/200326204-ea54145b-2268-49f0-b927-3ef3cd991b33.png">




### flex

- main axis 기준으로 ‘**공간 배분을 위해서’** 사용됨
</br>

- flex 속성은 `flex-grow`와 `flex-shrink`, `flex-basis`속성을 한 번에 적용할 수 있도록 해줌
    - **flex-grow**
        - 속성은 해당 flex item이 main axis 상에 공백이 있을 때, 이 공백을 얼마나 점유할지를 지정
    - **flex-shrink**
        - 해당 flex item이 main axis 상에 공간이 부족할 때, 얼마나 공간을 양보할지를 지정
    - **flex-basis**
        - 해당 flex item이 main axis 상에 공백이 있을 때, 최소 얼만큼의 공간을 점유할지를 지정

</br>

- 속성 예제

```html
<div class="container">
  <div class="item orange" style="flex: 1;">A</div>
  <div class="item green">B</div>
  <div class="item blue">C</div>
</div>
<div class="container">
  <div class="item orange" style="flex: 1;">A</div>
  <div class="item green" style="flex: 1;">B</div>
  <div class="item blue" style="flex: 1;">C</div>
</div>
<div class="container">
  <div class="item orange" style="flex: 1;">A</div>
  <div class="item green" style="flex: 2;">B</div>
  <div class="item blue" style="flex: 3;">C</div>
</div>
```

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
}

.container {
  display: flex;
  flex-direction: row;
  border: 5px solid red;
}

.item {
  color: white;
  font-size: 48px;
  padding: .5em;
  text-align: center;
}

.orange {
  background: orange;
}

.green {
  background: green;
}

.blue {
  background: blue;
}
```
<img width="40%" height="40%" src="https://user-images.githubusercontent.com/109334968/200326474-e55502e2-aba1-4aa3-a6d1-d73985bf69ac.png">


