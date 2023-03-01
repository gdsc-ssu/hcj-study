# Flexbox

- Container에 여러 개의 item 배치를 개발자가 쉽게 컨트롤할 수 있도록 도와주는 것
- 각 아이템의 height 를 동일하게 하거나 각 아이템의 간격을 동일하게 하는 작업을 좀 더 편하게 수행할 수 있다.
- 반응형 웹 디자인을 가능하게 해준다.

<br>

## flexbox 구성 요소

> 💡 flex container와 flex item에는 서로 적용할 수 있는 CSS 속성이 다르다.

- **flex container**
  - `flex-direction`
  - `justify-content`
  - `align-items`
  - ...
- **flex item**
  - `flex-basis`
  - `flex-grow`
  - `flex-shrink`
  - ...

<br>

## Main/Cross Axis

> main axis: 주축, cross axis: 교차축

flexbox를 원하는대로 제어하려면, axis의 개념에 대해서 이해해야 한다.

- **main axis**:  [`flex-direction`](https://developer.mozilla.org/ko/docs/Web/CSS/flex-direction) 속성을 사용하여 지정
- **cross axis**: main axis와 **수직**인 축으로 결정

<br>

### Main Axis

: `flex-direction`에 의해 결정되며, 4개의 값을 가질 수 있다.

- `row`
- `row-reverse`
- `column`
- `column-reverse`

<br>

### Cross Axis

: Main Axis에 수직한다.

- **Main Axis**(`flex-direction`): `row` or `row-reverse` 
  → **Cross Axis**: column direction
- **Main Axis**(`flex-direction`): `column` or `column-reverse`
  → **Cross Axis**: row direction

<br>

## justify-content

: flex item을 **main axis를 기준**으로 정렬하는 방식을 결정하는 속성

<br>

- 기본값은 `flex-start`

- 속성값
  - `stretch`
  - `flex-start`
  - `flex-end`
  - `center`
  - `space-around`
  - `space-between`
  - ...

- [모든 속성값](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content#values)

<br>

### Example

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

<br>

## align-items

: flex item을 **cross axis를 기준**으로 정렬하는 방식을 결정하는 속성

<br>

- 기본값은 `stretch`

- 속성값
  - `stretch`
  - `flex-start`
  - `flex-end`
  - `center`
  - ...

- [모든 속성값](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items#values)

<br>

### Example

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

<br>

## flex item

flex item에 지정가능한 속성들

- [`flex-basis`](https://developer.mozilla.org/ko/docs/Web/CSS/flex-basis)
- [`flex-grow`](https://developer.mozilla.org/ko/docs/Web/CSS/flex-grow)
- [`flex-shrink`](https://developer.mozilla.org/ko/docs/Web/CSS/flex-shrink)

<br>

### flex-basis

: 항목의 크기를 결정

- 기본값: `auto`
- 크기가 지정되어 있으면, 그대로 사용
- 크기가 지정되어 있지 않으면, **flex item**의 크기가 flex-basis 값으로 사용

<br>

### flex-grow

: 주축에서 남는 공간을 항목들에게 분배하는 방법을 결정

- 모든 항목의 `flex-grow` 값을 1로 지정하면 사용가능한 공간은 각 항목에게 동일하게 분배된다.
- 첫 항목의 `flex-grow` 값을 2로 지정하고 나머지 두 개의 항목을 1로 지정한다면 각 항목에 지정된 `flex-grow` 값의 비율에 따라 남은 공간이 분배된다.

<br>

### flex-shrink

: `flex-shrink` 속성은 주축의 공간이 부족할때 각 항목의 사이즈를 줄이는 방법을 결정

<br>

## 참고 자료

- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox