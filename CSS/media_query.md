## 미디어 쿼리(media query)란?

- 미디어 쿼리는 단말기의 유형, 화면 해상도, 뷰포트 너비 등에 따라 사이트의 CSS를 다르게 적용할 수 있도록 도와주는 기능

## 미디어 타입(media type)

- 미디어 쿼리는 미디어 별로 적용할 CSS를 따로 작성하는 것이므로 미디어 타입을 알려주어야 한다. 생략 시에는 all 타입으로 적용된다.
1. all - 모든 장치
2. screen - 컴퓨터 화면 장치 또는 스마트 기기의 화면
3. print - 인쇄 장치

## 미디어 특성

- 미디어 특성 표현식을 사용하여 출력 장치, 환경 등 특성의 존재 여부와 값을 판별하여 조건을 정의할 수 있음.
1. width : 스크롤바를 포함한 뷰포트의 너비
    
    ```css
    /*HTML*/
    <body>
        <div id="id1"> 400px 이하면 안 보여요 </div>
        <div id="id2"> 항상 보여요 </div>
        <div id="id3"> 600px 이상이면 안 보여요 </div>
     </body>
    
    /*CSS*/
    @media screen and (max-width: 400px) {
      #id1 {
        display: none;
      }
    }
    
    @media screen and (min-width: 600px) {
      #id3 {
        display: none;
      }
    }
    ```
    
    - 화면 크기에 따라 보이는 태그와 안 보이는 태그 지정
        
        [ 600 이상 일 때 ]
        
        ![https://user-images.githubusercontent.com/66131167/208882927-32addd9e-43f7-4cf8-95c9-3aa8f0d15924.png](https://user-images.githubusercontent.com/66131167/208882927-32addd9e-43f7-4cf8-95c9-3aa8f0d15924.png)
        
        [ 400 초과 600 미만 일 때 ]
        
        ![https://user-images.githubusercontent.com/66131167/208881618-4bfbcd74-187f-4ef1-aaa4-b5d1c8e671fd.png](https://user-images.githubusercontent.com/66131167/208881618-4bfbcd74-187f-4ef1-aaa4-b5d1c8e671fd.png)
        
        [ 400 이하 일 때 ]
        
        ![https://user-images.githubusercontent.com/66131167/208881909-efb844a2-4a63-4db8-adbf-9cc16cf6d263.png](https://user-images.githubusercontent.com/66131167/208881909-efb844a2-4a63-4db8-adbf-9cc16cf6d263.png)
        
2. height : 뷰포트의 높이
3. aspect-ratio : 화면의 비율
    
    ```css
     /* 뷰포트 너비가 5/4 비율 이하면 body를 아쿠아색으로 */
    @media screen and (max-aspect-ratio:5/4) {
      body{
        background-color: aquamarine;
      }
    }
    ```
    
    ![https://user-images.githubusercontent.com/66131167/208885323-f9b2b861-fd43-44e0-9941-27c3a917e51c.png](https://user-images.githubusercontent.com/66131167/208885323-f9b2b861-fd43-44e0-9941-27c3a917e51c.png)
    
4. orientation : 뷰포트의 방향
    
    ```css
    /*뷰포트의 방향이 세로일 때 body를 보라색으로 (1)*/
    @media (orientation: portrait) {
      body {
          background-color: rebeccapurple;
      }
    }
    
    /*뷰포트의 방향이 가로일 때 body를 보라색으로 (2)*/
    @media (orientation: landscape) {
      body {
          background-color: rebeccapurple;
      }
    }
    ```
    
    [ portrait 일 때  - 세로 비율이 더 큼]
    
    ![https://user-images.githubusercontent.com/66131167/208885951-cdaa6fc9-f9b5-4c03-ac43-9ee777ab23d2.png](https://user-images.githubusercontent.com/66131167/208885951-cdaa6fc9-f9b5-4c03-ac43-9ee777ab23d2.png)
    
    [ landscape 일 때 - 가로 비율이 더 큼 ]
    
    ![https://user-images.githubusercontent.com/66131167/208885704-60ffd964-3534-4c23-8d38-c5bdc5818418.png](https://user-images.githubusercontent.com/66131167/208885704-60ffd964-3534-4c23-8d38-c5bdc5818418.png)
    
5. scan - tv의 스캔 방식
6. grid : 그리드와 비트맵 스크린 중 어느 것을 사용하는지
7. color : 기기의 비트 수
8. color-index : 기기의 색상 수 
9. hover : 사용자가 요소 위에 마우스를 올릴 수 있는 환경인지

## 미디어 쿼리 작성 방법

- 가장 기본적인 미디어 쿼리 구문 작성 방법은 다음과 같다.
    
    ```css
    @media 미디어 타입 and ( 조건문 ) { 
    	/* 실행문 */
    }
    ```
    

## 미디어 쿼리 적용 방법

1. HTML의 link태그의 media속성에 값을 설정하는 방법
    
    ```html
    <link href="css/sso.css" rel="stylesheet" type=text/css" media="screen and (min-width:0px) and (max-width:480px)">
    ```
    
2. CSS파일 내에 직접 media를 설정해 주는 방법
    
    ```css
    @media
    all and (min-width: 480px){
    	div{
    		display: block;
      }
    }
    ```
    
3. media query를 설정한 파일을 CSS파일 내에서 import해서 적용하는 방법
    
    ```css
    import url("soyeon.css") all and (min-width: 320px);
    ```
    

## 주의사항

1. 띄어쓰기
    - 논리 연산자 중 하나인 and 구문을 사용할 때 구문 뒤에는 항상 공백을 한 칸 띄어줘야함.
2. min/max 작성 순서
    - min을 사용할 때는 반드시 크기가 작은 순서대로, max를 사용할 때는 반드시 크기가 큰 순서대로 작성해야함.