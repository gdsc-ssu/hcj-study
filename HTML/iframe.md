## iframe 태그

### 특징
1. iframe = inline frame 태그의 약자
2. 해당 웹 페이지 안에 다른 웹페이지 또는 동영상 등을 삽입해주는 태그
3. inline-block 속성을 가짐.
ex) 내 웹사이트에 원하는 유튜브 영상 가져오는 법

### 사용방법
1. frame과 달리, iframe 태그는 종료 태그가 있음.
```html
<iframe src="/css/intro" style="width:100%; height:300px"> </iframe>
```
2. iframe 태그 형태
```html
<iframe src="">대체 내용</iframe>
```
3. iframe 태그 옵션 (<iframe ~~>안에 쓸 수 있는 옵션들)
+ src: iframe에 삽입될 문서의 주소
+ width: iframe 너비 지정 (px, % 가능)
+ height: iframe 높이 지정 (px, % 가능)
+ frameborder: 테두리를 표시할지 말지 지정 [ 1 : 테두리가 있음, 0 :테두리 지우기]
+ scrolling: 스크롤바 유무를 선택 [yes :스크롤바 표시, no :스크롤바 없음, auto :자동]
+ marginheight :내용의 top, bottom 의 margin
+ marginwidth :내용의 left,right의 margin
+ align :iframe의 정렬 [top, middle, bottom, left, right]
+ name :target이 필요한 프레임의 이름 

4. 동영상 관련 iframe 태그 옵션
+ 특징 : video태그의 경우 가로 세로 길이를 css속성에서만 변경했지만, iframe 태그의 경우 태그 자체에 width , height 옵션이 있으므로, 여기서 값을 수정을 해주며 따로 css에서도 수정이 가능하다
ex)대표적 유튜브 영상의 동영상을 가져올 경우, url이 아닌 영상 우클릭 후 "소스코드복사"를 통해 코드 가져와야한다
 ->해당 소스 코드iframe태그로 구성되어 있기 때문이다.
+ autoplay=1 동영상 자동재생
+ mute=1 음소거 기능
+ loop=1 동영상 반복 재생 
+ playlist-유튜브 코드 (iframe태그 src 끝부분의 영어와 숫자가 혼합되어 있는 코드를 말함)
+  iframe태그에서 loop 기능은 혼자 사용할 수 없으며, playlist 옵션과 같이 사용해줘야함.
```html
<iframe width="704" height="396" src="https://www.youtube.com/embed/wdcPz77Xk88?loop=1&playlist=wdcPz77Xk88" title="[𝙿𝚕𝚊𝚢𝚕𝚒𝚜𝚝] 독기 충전 중 ■■■■■□90% 극복 플리" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```
+ controls 유튜브 동영상에 재생 일시정지 음소거 및 기타 커트롤 버튼 등 기존 인터페이스 없애주는 기능
+ 0: 기본값, 1:인터페이스 제거
+ video 태그는 동영상 자체에 인터페이스가 없으므로 controls을 활용하여 인터페이스를 추가하나, iframe 유튜브 동영상의 경우 동영상 자체에 인터페이스가 있으므로 controls 옵션을 사용하여 인터페이스를 제거해줌
+ 동영상에 다양한 옵션들을 적용하고 싶다면, 동영상 url 뒤에 옵션과 옵션 사이에  아래와 같이 ?옵션&옵션">으로 마무리해야 적용됨.

### 주의할 점
+ iframe 태그를 div 태그 처럼 사용하면 문제가 생길 수 있다.
+ iframe의 다음 특징으로 인해 발생하게 된다.</br>
->1)iframe 태그는 HTML 내부에 다시 HTML을 띄운다.</br>
->2) HTML은 하나의 파일이 하나의 웹 페이지이고, 이 페이지가 호출 될 때 페이지를 띄우는데 필요한 리소스들이(JS 등) 함께 로드된다.</br>

