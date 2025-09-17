# 2. HTML - FE
## 1) HTML Tags
### tag의 종류
- 태그는 그 의미에 맞춰서 사용해야 한다.
- 링크
- 이미지
- 목록
- 제목
- HTML reference를 통해 다양한 태그를 확인할 수 있다
  - 빨간색으로 경고된 태그들은 쓰지 않는 것이 바람직하다
  - div, h1, ul, li * 4 로 한번에 리스트 4개 만들기, a href="링크" etc..
```html
ex)
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>boostcourse</title>
</head>
<body>
  
  <div>
    <h1> 반갑습니다. </h1>
여기 여러분들이 좋아하는 과일이 있어요.
    <ul>
      <li><a href="www.apple.com">사과</a></li>
      <li>바나나</li>
      <li>메론</li>
      <li>귤</li>
    </ul>
  </div>
  
</body>
</html>
```
## 2) HTML Layout 태그
### 레이아웃을 위한 태그
- 레이아웃을 구성하는 태그의 의미를 안다
- header : 상단
- section
- nav : 네이버의 뉴스, 연애, 스포츠, 푸드 등 navigation 태그들
- footer : 하단
- aside
- 개발자 도구의 inspector를 통해 구역을 클릭하면 해당 구역의 코드를 알 수 있다.
- header와 footer는 사실 div와 똑같은 역할
- HTML5부터 지원한다
- CSS에서 블록 엘리먼트라고 하는 엘리먼트들이다
```html
ex)
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>boostcourse</title>
</head>
<body>
  
  <header>header</header>
  <div id="container">
    <nav><ul>
      <li>home</li>
      <li>news</li>
      <li>sports</li>
    </ul></nav>
    <aside><ul>
      <li>로그아웃</li>
      <li>오늘의 날씨</li>
      <li>운세</li>
    </ul></aside>
  </div>
  <footer>footer</footer>
  
</body>
</html>
```
## 3) HTML 구조설계
- 구글에 html structure design 검색
## 4) class와 id 속성
- HTML을 만들 때 속성 중 class와 id를 어떻게 사용하는지
- class의 용도는 비슷한 스타일을 여러 군데에 같이 표현하기 위해서 CSS 클래스를 만들어두고, 클래스 이름을 부여해서 같은 스타일을 갖게 할 수 있다
- 회사마다 개발단계에서 약속하여 자신들만의 규칙을 사용하기도 함
```html
ex)
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>boostcourse</title>
</head>
<body>

<header>
  <h1>Company Name</h1>
  <img src="...." alt="logo">
</header>

<section id="nav_section">
  <nav><ul>
    <li>Home</li>
    <li>Home</li>
    <li>About</li>
    <li>Map</li>
  </ul></nav>

  <section id="roll_section">
    <button></button>
    <div><img src="ㅇㅇ" alt=""></div>
    <div><img src="ㅇㅇ" alt=""></div>
    <div><img src="ㅇㅇ" alt=""></div>
    <button></button>
  </section>
  <section>
    <ul>
      <li class="out_description">
        <h3>What we do</h3>
        <div>설명~~~</div>
      </li>
      <li class="out_description">
        <h3>What we do</h3>
        <div>설명~~~</div>
      </li>
      <li class="out_description">
        <h3>What we do</h3>
        <div>설명~~~</div>
      </li>
    </ul>
  </section>
</section>

<footer><span>Copyright @codesquad</span></footer>

</body>
</html>
```