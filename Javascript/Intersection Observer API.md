# Intersection Observer API

타겟 요소와 viewport 사이의 intersection 내의 변화를 비동기적으로 관찰하는 방법

<br>

## intersection 정보가 필요한 이유

- 웹, 앱 최적화를 위한 지연 로딩
- 페이지 이동의 UX 개선을 위한 infinite-scroll
- 광고 노출 통계 파악
- 타겟 요소의 노출에 따른 애니메이션 수행

<br>

## 이전 방법

이전에는 `Element.getBoundingClientRect()` 와 같은 메소드를 이벤트 핸들러와 함께 사용해 위의 작업을 수행했다. 하지만 이 방법은 모든 코드가 main thread에서 실행되어, 성능 문제를 발생시킨다.

비동기 처리를 지원하는 Intersection Observer API는 타겟 요소가 viewport와 발생하는 모든 상황(viewport에 들어오거나, 나가거나, 원하는 부분만큼 intersection이 변경될 때) 마다 실행될 콜백 함수를 등록할 수 있다.

<br>

## 기본 개념

Intersection Observer API는 다음과 같은 상황에 콜백 함수를 실행시킬 수 있다.

- target이 기기의 viewport 나 특정 요소(root) 와 교차될 때
- observer가 최초로 타겟을 관측하도록 요청받을 때

<br>

## Intersection observer 생성하기

`IntersectionObserver` 생성자는 `callback`과 `options` 두 개를 파라미터로 받는다.

```tsx
let observer = new IntersectionObserver(callback, options)
```

<br>

### callback

콜백 함수가 받는 파라미터는 두 개가 있는데, `entries`와 `observer` 이다.

- `entries`: IntersectionObserver의 threshold를 구체적으로 설정할 수 있다. 
  ([IntersectionObserverEntry]() 리스트를 포함하고 있으며 골라서 사용할 수 있다.)

- `observer`: 생성자로 만든 객체의 observer를 컨트롤 할 수 있다.

  ```js
  // 예제 
  observer.observe(target)	// 타겟 요소 관측 시작
  observer.unobserve(target)	// 타겟 요소 관측 종료
  observer.disconnect()		// 모든 요소 관측 종료
  ```


### options

- `root`: viewport 요소 설정(기본값: 브라우저 뷰포트)
- `rootMargin`: root의 여백, css의 margin 속성과 유사하게 설정할 수 있다. (기본값: 0)
- `threshold`: 콜백이 실행될 타겟 요소의 노출 비율 지정 (0 ~ 1), 배열로 설정 시 노출 정도에 따라 계속 바뀐다. `[0, 0.25, 0.5, 0.75, 1]`

```js
const options = {
	root: document.querySelector('#scrollArea'),
	rootMargin: '0px',
	threshold: 1.0
}
```



<br>

### 타겟 요소 설정하기

```js
const target = document.querySelector('.target');
observer.observe(target);	// 타겟 관찰 시작
```

<br>

## 예시

- id명이 `target`인 타겟 요소가 화면에 100% 노출되었을 시(최초 1번), 노출된 타겟 요소의 배경색, 글씨색 변경하기

  (타겟 요소 노출 시, class명에 `intersection`을 추가해줌으로써 타겟 요소에 변화 주는 방식)

  ```js
  // css
  .intersection {
      background-color: black;
      color: white;
  }
  
  //js
  const targetDOM = document.querySelector('.target');
  
  const callback = (entries, observer) => {
      targetDOM.classList.add('intersection');	// class명 추가
  	observer.disconnect()	// or observer.unobserve(entries[0].target)    
  }
  
  const option = {
      threshold: 1.0
  }
  
  const myObserver = new IntersectionObserver(callback, option);
  
  myObserver.observe(targetDOM);	// 관찰 시작
  ```

<br>

## 참고자료

- https://developer.mozilla.org/ko/docs/Web/API/Intersection_Observer_API