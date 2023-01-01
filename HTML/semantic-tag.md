## semantic tag란?

- 말 그대로 의미가 담겨있는 태그 요소
- HTML 에서 block의 영역을 칭하는 div와 inline 영역을 칭하는 span태그와 달리 태그 그 자체에 의미가 담겨 있는 태그를 말한다.
- 종류 : header, main, footer, section, article 등
- 전체적인 구조
    
    ![https://user-images.githubusercontent.com/66131167/200269676-30c77230-ac45-4a3a-8328-cc915667bd98.png](https://user-images.githubusercontent.com/66131167/200269676-30c77230-ac45-4a3a-8328-cc915667bd98.png)
    

## 왜 사용하는가?

div 태그를 사용해도 물론 가능은 하지만 우리는 여러 이점이 있기에 semantic tag를 사용한다.

1. 검색엔진 최적화 (SEO: Search Engine Optimization)
    - 웹사이트를 크롤링 할 때  구조를 정확하게 분석하도록 도움
2. 웹 접근성에 효율적
    - 스크린리더 ( 시각장애인을 위한 웹 서핑 프로그램)과 같은 환경에서 웹 접근성과 사용성 향상
3. 유지보수의 용이성
    - 해당 태그 영역의 특성에 맞는 작업을 구분하여 가독성이 높아지며 유지보수가 쉬움

## sementic tag 종류

- header
    - 일반적으로 제목(h1~h6 요소)을 포함함.
        
        ![https://user-images.githubusercontent.com/66131167/200261649-745fbe1e-4118-4790-8716-3b375371b098.png](https://user-images.githubusercontent.com/66131167/200261649-745fbe1e-4118-4790-8716-3b375371b098.png)
        
- nav
    - 다른 테이지나 같은 페이지 안에 다른 부분으로 이어주는 네비게이션 링크로 구성된 섹션
    - 주로 네비게이션 블럭을 구성하는 섹션
        
        ![https://user-images.githubusercontent.com/66131167/200261719-380cc806-20e8-47d6-9171-5a17b8e32a5a.png](https://user-images.githubusercontent.com/66131167/200261719-380cc806-20e8-47d6-9171-5a17b8e32a5a.png)
        
- footer
    - 주로 저작권 정보나 서비스 제공자 정보 등을 나타냄.
    - 사이트 하단에 위치함.
        
        ![https://user-images.githubusercontent.com/66131167/200261775-3eac5ff6-cf37-4175-8fb0-0eb8f785affe.png](https://user-images.githubusercontent.com/66131167/200261775-3eac5ff6-cf37-4175-8fb0-0eb8f785affe.png)
        
- section
    - 문서나 응용프로그램의 일반적인 섹션
    - 같은 테마를 가진 여러 컨텐트를 의미적으로 그룹핑하기위해 사용
        
        ![https://user-images.githubusercontent.com/66131167/200263119-6844821a-b00d-4570-8927-2e335ab6d491.png](https://user-images.githubusercontent.com/66131167/200263119-6844821a-b00d-4570-8927-2e335ab6d491.png)
        
- main
    - 문서에서 가장 중심이 되는 컨텐츠를 정의
        
        ![https://user-images.githubusercontent.com/66131167/200261575-cc45897d-7106-452d-b9ba-0377c8a70782.png](https://user-images.githubusercontent.com/66131167/200261575-cc45897d-7106-452d-b9ba-0377c8a70782.png)
        
- article
    - 문서 내에서 독립적인 컨텐츠를 나타냄.
        
        ![https://user-images.githubusercontent.com/66131167/200265059-b70a9df3-7c46-4ffb-8894-7a85cb9dfb94.png](https://user-images.githubusercontent.com/66131167/200265059-b70a9df3-7c46-4ffb-8894-7a85cb9dfb94.png)
        
- aside
    - 페이지 전체 내용과는 어느정도 관련성이 있지만, 주요 내용과는 직접적인 연관성은 없는 분리된 내용을 담음.
    - 주로 사이드바의 형태로 보여짐
        
        ![https://user-images.githubusercontent.com/66131167/200265880-393919b3-1404-47b5-ac29-a8b0d17dace8.png](https://user-images.githubusercontent.com/66131167/200265880-393919b3-1404-47b5-ac29-a8b0d17dace8.png)
        
- details
    - 추가적인 정보를 나타내거나 사용자가 요청하는 정보를 나타냄
    - summary태그와 함께 사용하며, open 속성을 이용해서 details 요소가 나타내는 내용들을 노출시킬 수 있음.
- figure
    - 일러스트, 사진, 코드 등에 주석을 다는 용도로 사용
    - 이 요소가 제거 되더라도 문서의 주된 흐름에는 큰 영향을 미치지 않음
- mark
    - 하나의 문서 내에서 다른 문맥과의 관련성을 나타내고자 마킹이나 하이라이트된 텍스트를 표현
    - 검색어와 매칭되는 부분을 하이라이팅하기 위해 사용함.
- time
    - 현대의 날짜와 시간을 기계가 읽을 수 있는 방식으로 인코드해서 제공할 목적으로 사용
    

## article 태그와 section 태그의 차이점

- article은 내용이 독립적이고 section은 주제별로 구분한 그룹이다.
- article 태그는 section 태그와 달리 독립적으로 존재할 수 있으며 재사용이 가능하고 section 태그는 논리적으로 관계있는 요소나 문서를 분리할 때 사용한다.
- 사용예시
    
    ```html
    <section>
      <h1>World</h1>
      <section>
         <p>Asia</p>
         <article>Korea</article>
         <article>Japan</article>
         <article>China</article>
      </section>
      <section>
        <p>Europe</p>
        <article>France</article>
        <article>Nederland</article>
        <article>Monaco</article>
      </section>
    </section>
    ```
    

## 참고자료
 
- [https://opentutorials.org/module/1892/10954](https://opentutorials.org/module/1892/10954)
- [https://server-talk.tistory.com/106](https://server-talk.tistory.com/106)
- [https://www.youtube.com/watch?v=uDmNhHYecL4&t=146s](https://www.youtube.com/watch?v=uDmNhHYecL4&t=146s)