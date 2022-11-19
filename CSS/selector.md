## 선택자( selector )란?

- 말 그대로 선택을 해주는 요소
- 특정 요소들을 선택하여 스타일 적용이 가능

## selector의 rule set

- rule set 즉 규칙은 HTML페이지 안의 특정 요소를 어떻게 렌더링 할 것인지 알려주는 기본 문장으로 스타일 규칙이라고 함.
    
    ```css
    p {               /* p가 선택자 */
    	color: red;     /* 속성: 속성값 */
    	padding: 5px;   /* 라인 하나가 선언 */
    }
    ```
    
    ![https://user-images.githubusercontent.com/66131167/202841704-19830824-1179-4660-91b2-74163f1b9d34.png](https://user-images.githubusercontent.com/66131167/202841704-19830824-1179-4660-91b2-74163f1b9d34.png)
    

## selector의 종류

- 전체 선택자
    - HTML 내부의 모든 요소(태그)에 같은 CSS속성을 적용함
    - 문서 안의 모든 요소를 읽기에 페이지 로딩 속도가 느려져 자주 사용하지 않는 것을 선호
    
    ```css
    * {
    	margin: 0;
    	text-decoration: none;
    }
    ```
    
- 태그 선택자
    - 태그명을 직접 선택함.
    
    ```css
    /* HTML*/
    <p> hello </p>
    <div> my name is </div>
    
    /* CSS */
    div {
    	background: yellow;
    	color: darkgreen;
    }
    
    /*div 태그는 위의 CSS가 적용됨.*/
    ```
    
    ![https://user-images.githubusercontent.com/66131167/202846106-72d28d89-ca13-40c0-aef1-c49bd91aa38d.png](https://user-images.githubusercontent.com/66131167/202846106-72d28d89-ca13-40c0-aef1-c49bd91aa38d.png)
    
- 클래스 선택자
    - 클래스의 속성값과 일치하는 요소를 선택함.
    - 클래스 선택자를 사용할때는 속성값 앞에 마침표 (.)를 찍어 class값임을 알려줌.
    
    ```css
    /*HTML*/
    <div class="first"> 선택자1 </div>
    <div class="second"> 선택자2 </div>
    <p class="first"> 선택자3 </div>
    
    /* CSS */
    .second{
    	background: yellow;
    	color: darkgreen;
    }
    
    div.first{
    	background: darkgreen;
    	color: yellow;
    }
    
    /* 위의 경우 div 안의 first클래스를
    선택했기에 선택자 3은 스타일이 적용되지 않음 */
    ```
    
    ![https://user-images.githubusercontent.com/66131167/202846119-8e2963d3-90a9-4f66-9c96-8620cdde509e.png](https://user-images.githubusercontent.com/66131167/202846119-8e2963d3-90a9-4f66-9c96-8620cdde509e.png)
    
- id 선택자
    - id 선택자를 사용할때는 속성값 앞에 ‘#’을 사용하여 id 선택자임을 알려줌.
    
    ```css
    /* HTML */
    <div id="id1"> 선택자1 </div>
    <div id="id2"> 선택자2 </div>
    <div id="id3"> 선택자3 </div>
    <p id="id4"> 선택자4 </div>
    
    /* CSS */
    #id1 {
      font-size: 30px;
      background: darkgreen;
      color: yellow;
    }
    
    div#id2 {
      font-size: 50px;
      background: yellow;
      color: darkgreen;
    }
    ```
    
    ![https://user-images.githubusercontent.com/66131167/202846086-02a832f9-ea72-4b2f-99b9-a5135481ca20.png](https://user-images.githubusercontent.com/66131167/202846086-02a832f9-ea72-4b2f-99b9-a5135481ca20.png)
    
- 복합 선택자
    - 두 개 이상의 선택자 요소가 모인 선택자로 하위 선택자 / 자식 선택자 / 인접 형제 선택자 / 일반 형제 선택자가 대표적임.
    
    - 하위 선택자: A요소의 자손인 B요소를 선택함. 요소를 나열하여 작성.
        
        ```css
        section ul {
          font-size: 30px;
          background: darkgreen;
        }
        ```
        
    - 자식 선택자: A요소의 자식인 B요소를 선택함. 요소 사이에 ‘>’를 써서 작성.
        
        ```css
        section > ul {
          font-size: 30px;
          background: yellow;
        }
        ```
        
    - 인접 형제 선택자: A요소를 따르는 B요소를 선택함. 요소 사이에 ‘+’를 써서 작성.
        
        ```css
        p + li {
          font-size: 30px;
          background: darkgreen;
        }
        ```
        
    - 일반 형제 선택자: A요소가 앞에 존재하면 B요소를 선택함. 요소 사이에 ‘~’을 써서 작성.
        
        ```css
        p ~ li {
          font-size: 30px;
          background: yellow;
        }
        ```
        

## 클래스 선택자를 사용해야하나 id선택자를 이용해야하나?

- 한 페이지 안에서 여러번 반복되는 스타일이 있을 때는 클래스 사용자를 사용하고, 단 한번만 유일하게 적용하는 스타일이면 id 선택자를 사용한다.
    - class 속성: 분류 안에 포함되는 요소의 특성을 정의하는 데 사용하기에 한 페이지 안에 중복되어 사용됨.
    - id 속성: 요소의 유일한 특성을 정의하기에 한 페이지 안에서 특정 id 속성 값을 오직 하나만 사용하기를 권장함.
- class 속성은 속성값을 두 개 이상 가질 수 있다. 그래서 클래스 선택자를 사용하면 여러 종류의 스타일 규칙을 적용할 수 있다.
- id 선택자가 클래스 선택자보다 우선순위가 높다. 우선적으로 적용할 스타일은 id 선택자를 사용하는 것이 좋다.

## 하위 선택자와 자식 선택자의 차이

- 포함하는 요소를 부모요소 포함되는 요소를 자식요소라고 한다.
    
    ```css
    /* HTML */
    
    <div>
      <p>hello</p>      /* 하위선택자, 자식선택자 */
      <ul>
        <li>my</li>
        <li>
          name
          <ul>
            <p>is</p>      /* 하위선택자 */
            <li>hong</li>
            <li>So yeon</li>
          </ul>
        </li>
      </ul>
    </div>
    
    /* CSS */
    
    /* 하위 선택자 */
    div p {
      font-size: 30px;
      background: darkgreen;
    }
    
    /* 자식 선택자 */
    div > p {
      font-size: 30px;
      background: yellow;
    }
    ```
    
- 하위 선택자는 부모요소에 포함된 모든 하위요소에 스타일을 적용한다.
    
    ![https://user-images.githubusercontent.com/66131167/202845954-772eae36-ab22-4d24-a6c6-c363de1d369d.png](https://user-images.githubusercontent.com/66131167/202845954-772eae36-ab22-4d24-a6c6-c363de1d369d.png)
    
- 자식 선택자는 부모요소에 포함된 바로 아래 자식 요소에만 스타일을 적용한다.
    
    ![https://user-images.githubusercontent.com/66131167/202845946-296666c3-cfae-4d71-b545-b80ee3ac4117.png](https://user-images.githubusercontent.com/66131167/202845946-296666c3-cfae-4d71-b545-b80ee3ac4117.png)
    

## 인접 형제 선택자와 일반 형제 선택자

- 같은 부모 요소를 가지는 요소들을 형제 관계라고 한다. 먼저 나온 요소를 ‘형 요소’, 나중에 나온 요소를 ‘동생 요소’라고 한다.
    
    ```css
    /* HTML */
     
    <div>
      <p>hello</p>
      <ul>
        <li>my</li>
        <li>name</li>
        <p>hello</p>
        <li>is</li>   /* 인접 형제 선택자, 일반 형제 선택자 */
        <li>So yeon</li>  /* 일반 형제 선택자 */
      </ul>
    </div>
    
    /* CSS */
    
    /* 인접 형제 선택자 */
    p + li {
      font-size: 30px;
      background: darkgreen;
    }
    
    /* 일반 형제 선택자 */
    p ~ li {
      font-size: 30px;
      background: yellow;
    }
    ```
    
- 인접 형제 선택자는 형 요소 다음으로 나오는 첫번째 동생 요소에만 스타일을 적용한다.
    
    ![https://user-images.githubusercontent.com/66131167/202845873-35a7c4d6-84f1-495c-9e4b-ec493475e0dd.png](https://user-images.githubusercontent.com/66131167/202845873-35a7c4d6-84f1-495c-9e4b-ec493475e0dd.png)
    
- 일반 형제 선택자는 형 요소 다음으로 나오는 모든 동생 요소에 스타일을 적용한다.
    
    ![https://user-images.githubusercontent.com/66131167/202845850-bc60cef2-6d59-4052-b2f1-61fb3880de63.png](https://user-images.githubusercontent.com/66131167/202845850-bc60cef2-6d59-4052-b2f1-61fb3880de63.png)
    

## 출처

- [https://heinafantasy.com/155](https://heinafantasy.com/155)
- [https://kkangsg.tistory.com/10](https://kkangsg.tistory.com/10)
- [https://www.nextree.co.kr/p8468/](https://www.nextree.co.kr/p8468/)