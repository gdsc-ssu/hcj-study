## Bubbling and Capturing 

### 이벤트 흐름 

<img width="613" alt="스크린샷 2022-11-11 12 26 42" src="https://user-images.githubusercontent.com/67703882/201256551-d37b8f47-820b-457f-968e-7ec599c293de.png" style="zoom: 75%;" >

HTML DOM에서 이벤트가 발생하면 크게 3가지 단계로 이벤트 흐름을 나눌 수 있다.

1. Capturing Phase : 이벤트가 하위 요소로 전파되는 단계
2. Target Phase : 이벤트가 실제 타깃 요소로 전달되는 단계
3. Bubbling Phase : 이벤트가 상위 요소로 전파되는 단계 

위 예시 그림에서 html, body, div 태그에 각각 click 이벤트가 걸려있다고 가정하고, div 요소에 click 이벤트가 발생할 경우의 과정을 보자.  

- 브라우저는 window -> html -> body 순으로 내려가면서 태그들 중에 click 이벤트가 있는지 모두 검색한다. (캡처링 단계)  

- div 태그에 도달하면 div의 click 이벤트가 실행이 되고 (타겟 단계)
- 그 이후에는 다시 div 태그부터 차례대로 위로 올라가면서 body, html 태그의 click 이벤트를 발생시킨다. (버블링 단계)

즉 div 요소를 click 해도, div 부모 요소에 걸려있는 click 이벤트들도 차례대로 실행되는 것이다. (div -> body -> html) 

#### 이벤트 발생 정보

- `event.target` : 실제 이벤트가 발생한 요소. 
- `event.currentTarget` (=`this`) : 현재 실행 중인 이벤트가 할당되어있는 요소. 
- `event.eventPhase` : 현재 이벤트 흐름 단계 (캡처링=1, 타깃=2, 버블링=3)

```html
<form onclick="console.log('form')">
  <div>
    <p></p>
  </div>
</form>
```

- p 태그 클릭 시 : target = p, currentTarget = form 
- div 태그 클릭 시 : target = div, currentTarget = form
- form 태그 클릭 시 : target = currentTarget = form 

#### 버블링 중단하기 

만약 특정 이벤트가 상위 요소로 전파되는 것을 막고 싶다면, 즉 버블링을 중단하기 위해서는 해당요소에 `event.stopPropagation` 을 사용하면 된다.

```html
<form onclick="console.log('form')">
  <div>
    <p onclick="event.stopPropagation()"></p>
  </div>
</form>
```

위 예시 코드에서 p 태그를 클릭하면 form이 console에 찍히지 않는다. 클릭 이벤트가 버블링을 중단시켰으므로 form의 클릭 이벤트가 실행되지 않기 때문이다. 

만약 모든 이벤트의 버블링을 멈추고 싶다면 `event.stopImmediatePropagation()` 를 사용하면 된다. 

> 버블링을 꼭 막아야하는 이유가 분명히 있지 않은 이상 막지 않는 것이 좋다.
>
> 페이지 내에서 사용자의 행동 패턴을 분석하기 위해 클릭 이벤트 전부를 감지하는 시스템을 사용한다고 하자. 이러한 시스템은 stopPropagation으로 버블링을 막아놓은 영역에서 클릭 이벤트를 감지하지 못하게 된다. 이 밖에도 예상치 못한 결과를 추후에 야기할 수 있기 때문에 웬만하면 이벤트 버블링은 막지 않도록 한다. 

#### 캡처링 제어하기

앞서 이야기했듯, 이벤트가 발생한 태그의 부모 요소들은 캡처링 단계에서 이벤트가 감지된 후, 버블링 단계에서 이벤트가 실행된다. 그런데 만약 부모 요소들의 이벤트를 **버블링 단계가 아닌 캡처링 단계에서 실행**시키고 싶다면 어떻게 해야할까?

이를 위해 요소에 이벤트를 등록하는 addEventListener의 구조를 다시 보자. 

```js
element.addEventListener(event, handler, [options])
```

3번째 인자의 options 중 capture 옵션으로 false/true 두가지 값을 가질 수 있다. 

- `false` 이면 이벤트는 버블링 단계에서 동작한다. (default 값)
- `true` 이면 이벤트는 캡처링 단계에서 동작한다. 

이벤트를 캡처링 단계에서 동작하기 위해 `{capture:true}` 로 지정해주면 되지만, options 값 자체를 `true` 로 할당해주어도 동일하다. 

<br />

위 내용을 토대로 간단한 코드를 테스트해보자.

<img width="177" alt="스크린샷 2022-11-11 14 17 32" src="https://user-images.githubusercontent.com/67703882/201268712-c37f43bb-5c6e-4587-b11d-9e9501754c77.png"> 

```javascript
//캡쳐링 이벤트 등록
A.addEventListener("click", function (e) {
  console.log(e.eventPhase,"click A Capture");
}, true);
  
B.addEventListener("click", function (e) {
  console.log(e.eventPhase,"click B Capture");
}, true);
  
C.addEventListener("click", function (e) {
  console.log(e.eventPhase,"click C Capture");
}, true);

//버블링 이벤트 등록
A.addEventListener("click", function (e) {
  console.log(e.eventPhase,"click A Bubble");
});
  
B.addEventListener("click", function (e) {
  e.stopPropagation();
  console.log(e.eventPhase,"click B Bubble");
});
  
C.addEventListener("click", function (e) {
  console.log(e.eventPhase,"click C Bubble");
});
```

만약 C 영역을 클릭했을 경우 아래와 같이 콘솔에 찍힌다. 

<img width="158" alt="스크린샷 2022-11-11 14 25 35" src="https://user-images.githubusercontent.com/67703882/201269632-b37dea59-80e1-4f7c-a3e0-18fdca227e5b.png"> 

B의 버블링 이벤트 등록 단계에서 stopPropagation을 사용했기 때문에 A 까지 버블링이 안되는 것을 볼 수 있다. 

#### 이벤트 위임 (event delegation)

이벤트 위임은 캡처링과 버블링 과정을 이용하는 것으로, 여러 엘리먼트마다 각각의 이벤트 핸들러를 할당하지 않고, 공통되는 부모에 이벤트 핸들러를 할당하여 이벤트를 관리하는 방식이다.

```html
<div id='menu'>
  <button>버튼 1</button>
  <button>버튼 2</button>
  <button>버튼 3</button>
</div>
```

위 코드에서 총 3개의 버튼에 같은 클릭 이벤트를 할당해야한다고 가정해보자. 

모든 버튼에 대해 이벤트 리스너를 등록하면 매우 비효율적일 것이다. (버튼 개수가 많아진다면 더 비효율적이다.. ) 따라서 이벤트 위임 방식을 이용해 `<div id='menu'>` 에 이벤트를 등록하면 이러한 문제를 해결할 수 있다. 

#### 요약

1. 이벤트가 발생하면 브라우저는 DOM 트리를 따라 이벤트가 발생된 요소(= `event.target` ) 까지 내려간다.
2. 이벤트는 트리를 따라 내려가면서 `addEventListener(...,true)` 로 할당한 핸들러를 동작시킨다. (캡처링 단계)
3. 이후 타깃 요소에 설정된 핸들러가 호출되고, `event.target` 부터 시작해서 최상위 노드까지 이벤트가 전달되면서 `addEventListener(...,false)` 로 할당된 핸들러를 동작시킨다. (버블링 단계)



#### 참고

https://www.youtube.com/watch?v=7gKtNC3b_S8

https://ko.javascript.info/bubbling-and-capturing

https://velog.io/@pjeeyoung/event#2-evstoppropagation