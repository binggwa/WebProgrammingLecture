# 3. CSS - FE
## 1) CSS 선언방법
- selector(선택자) { property : value; }
- ex) span { color : red; }
### style을 HTML 페이지에 적용하는 3가지 방법
- inline
- internal
- external
- 같은 셀렉터로 동일한 스타일을 적용했을 때, 위에서부터 우선적으로 부여된다.
### html 태그 위치에 따라 다름
- inline : <span style="color:red">
- internal : <head> 내부의 <style>, <body> 내부의 <span> html과 css가 공존해 선호되지 않음!
- external : 외부파일 .css 로 지정하기 <link rel="stylesheet" type="text/css" href="main.css" />
```html
ex)
<!DOCTYPE html>
<html>
<head>
    <!-- // internal -->
    <style>

        div > p {
          font-size:20px;    
        }

    </style>
    <link rel="stylesheet" href="css_basic.css">    <!-- // external -->

    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>boostcourse</title>
</head>
<body>
<div>
    <p style="color:blue;">웹 프론트엔드</p>    <!-- // inline -->
</div>
</body>

</html>

css_basic.css
div > p {
border : 1px solid slategray;
}
```
## 2) 상속과 우선순위 결정
- 상위에서 적용한 스타일이 하위에도 반영된다. 
- 중첩된 엘리먼트마다 매번 같은 색상과 글자 크기를 부여하지 않아도 된다.
- width 속성이 상속되면 하위 엘리먼트가 모두 같은 크기의 넓잇값을 가지는 등 문제가 생길 수 있어
- box-model이라고 불리는 속성들(width, height, margin, padding, border)와 같이 크기 배치 관련 속성들은 상속되지 않는다.
```html
ex)
<!DOCTYPE html>
<html>
<head>

    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>boostcourse</title>

    <style>
          div ul li div p {           <!--body 부분의 div, ul, li, div, p를 따라서 "내용 설명~" 부분만 스타일 적용-->
          color : blue;
          font-size : 30px;
          border : 2px solid slategray;
          padding : 30px;
        }
    </style>

</head>
<body>

<div>
    <span>my text is upper!</span>
    <ul>
        <li>
            <span>my text is dummy</span>
            <div>
                <p>내용 설명~</p>
            </div>
        </li>
        <li></li>
    </ul>
</div>

</body>

</html>
```
### Cascading
- CSS는 여러가지 스타일정보를 기반으로 경쟁에 의해 적절한 스타일이 반영된다.
- 어떤 것을 기준으로 최종적으로 반영하는지는 브라우저가 처리한다.
- 선언방식에 따른 차이
  - inline > internal > external
- 동일하면 나중 것이 먼저 적용된다.
```html
ex)
span {
    color : red;
}
span {
    color : blue;
}   
```
- 위의 경우 blue 적용
- 보다 구체적으로 표현된 것은 우선적으로 적용
```html
ex)
body > span {
color : red;
}
span {
color : blue;
}
```
- 위의 경우 red 적용
- id 값에는 더 높은 점수를 준다 ( id > class > element )
```html
ex)
<div id="a" class="b">
    text...
</div>

#a {
    color : red;
}
.b {
    color : blue;
}
div {
    color : green;
}
```
- 위의 경우 red
## 3) CSS Selector
- HTML의 요소를 tag, id, class, html 태그속성등을 통해 쉽게 찾아주는 방법
- element에 style을 지정하기 위해서, 3가지 기본 선택자를 사용할 수 있음
  - tag, id, class
- tag로 지정할 때
  - ex) span { color : red; } : 모든 span 태그에 지정됨
- id로 지정할 때
  - ex) #spantag { color ~ } : spantag라는 id를 가지고 있는 곳에 지정됨
- class로 지정할 때
  - ex) .spanClass ~
- id, class 요소 선택자와 함께 활용 가능
  - ex) div.class
- 그룹 선택 가능
  - ex) h1, span, div#id
- n번째 자식요소 선택 가능 (nth-child)
  - ex) #jisu > p:nth-child(2) {color:red;}
## 4) CSS 기본 Style 변경하기
```html
ex)
<!DOCTYPE html>
<html>
<head>

    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>boostcourse</title>

    <style>
        body > div {
          font-size : 32px;  /* 기본값이 원래 16px인데, 32px로 변경 가능 */
          background-color : #ff0;
          font-family : monospace, sans-serif;
        }
        .myspan {
          /* color : rgba(0,0,255,0.5); */
          color : #0000ff;
          /* font-size : 30px; */
          font-size : 2em;  /* em으로 기본값의 배수로 표현가능하다 */
        }
    </style>

</head>
<body>

<div>
    <span class="myspan">my text is upper!</span>
</div>

</body>

</html>
```
## 5) Element가 배치되는 방법 (CSS layout)
### 엘리먼트가 배치되는 방식
- 엘리먼트를 화면에 배치하는 것을 layout 작업이라고 하며, rendering 과정이라고도 함
- 편의상 배치 라고 할 것
- 엘리먼트는 위에서 아래로 순서대로 블럭을 이루며 배치되는 것이 기본
- 웹사이트의 배치는 다양하게 표현 가능해야 하기 때문에, css에는 추가적인 속성을 제공함
- 중요한 속성은 다음과 같다.
  - display (block, inline, inline-block)
  - position (static, absolute, relative, fixed)
  - float (left, right)
- 이 속성을 중심으로 엘리먼트의 배치를 이해하는 것이 중요하다.
### 블록으로 쌓이는 엘리먼트 (display:block)
- display 속성이 block이거나 inline-block인 경우, 그 엘리먼트는 벽돌을 쌓듯 블록을 가지고 쌓인다.
```html
ex)
<div>block1</div>
<p>block2</p>
<div>block3</div>
```
- 이렇게 구현한 코드는 화면에 위에서 아래로 쌓이듯이 채워진다.
- 높이값을 더 주면 더 높은 크기로 엘리먼트가 쌓인다.
### 옆으로 흐르는 엘리먼트 (display:inline)
- display 속성이 inline인 경우는 우측으로, 아래쪽으로 빈자리를 차지하며 흐른다.
- inline 속성의 엘리먼트는 높이와 넓이를 지정해도 반영이 되지 않는다.
```html
<div>
  <span>나는 어떻게 배치되나요?</span>
  <span>좌우로 배치되는군요</span>
  <a>링크는요?</a>
  <strong>링크도 강조도 모두 좌우로 흐르는군요</strong>
  모두다 display 속성이 inline인 엘리먼트이기 때문입니다.
</div>
```
### 좀 다르게 배치시키기 (position 속성)
- position 속성을 사용하면 상대적/절대적으로 특정 위치에 엘리먼트를 배치하는 것이 수월하다.
1. position 속성은 기본 static이다. 그냥 순서대로 배치된다.
2. absolute 는 기준점에 따라서 특별한 위치에 위치한다. top/left/right/bottom으로 설정한다. 기준점을 상위엘리먼트로 단계적으로 찾아가는데, position이 기준점이다.
3. relative 는 원래 자신이 위치해야 할 곳을 기준으로 이동한다. top/left/right/bottom으로 설정
4. fixed 는 viewport(전체화면) 좌측, 맨위를 기준으로 동작한다.
```html
ex)
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>JS Bin</title>
</head>
<body>

<div class="wrap">
    <div class="static">static(default)</div>
    <div class="relative">relative(left:10px)</div>
    <div class="absolute">absolute(left:130px;top:30px)</div>
    <div class="fixed">fixed(top:250px)</div>
</div>

</body>
</html>

css

.wrap {
position:relative;
}

.wrap > div {
width:150px;
height:100px;
border:1px solid gray;
font-size:0.7em;
text-align:center;
line-height:100px;
}

.relative {
position:relative;
left:10px;
1top:10px;
}

.absolute {
position:absolute;
left:130px;
top:30px;
}

.fixed {
position:fixed;
top:250px;
}
```
### 간격을 다르게 해서 배치하기 (margin : 10px)
- margin으로 배치가 달라질 수 있다. 
- margin은 위/아래/좌/우 엘리먼트와 본인간의 간격이다. 그 간격만큼 내 위치가 달라진다.
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
</head>
<body>
  <div>left</div>
  <div class="bottom">bottom</div>
</body>
</html>

css
* {
border:1px solid gray;
}

.bottom {
margin-top : 100px;
margin-left : 100px;
}
```
### 기본 배치에서 벗어나서 떠있기 (float:left)
- float 속성으로 원래 flow에서 벗어날 수 있고 둥둥 떠다닐 수 있다.
- block 엘리먼트가 float된 엘리먼트는 의식하지 못하고 중첩해서 배치된다.
- 이런 독특함 때문에 웹사이트 레이아웃 배치에서 유용하게 활용된다.
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
</head>
<body>
  <div class="blue"></div>
  <div class="green"></div>
  <div class="red"></div>
</body>
</html>

div {
width:100px;height:100px;
border:1px solid gray;
font-size:0.7em;
}


.blue {
background-color:blue;
}

.green {
float:left;
background-color:green;
}

.red {
background-color:red;
/*숨겨진 녹색을 드러내기 위해 relative로 살짝옮김*/
position:relative;
left:10px;
}
```
### 하나의 블록엘리먼트는 box 형태임 (box-model)
- box의 크기와 간격에 관한 속성으로 배치를 추가 결정함
- margin, padding, border, outline으로 생성된다.
- box-shadow속성도 포함할 수 있는데, border 밖에 테두리를 그릴 수 있는 속성이다.
### 엘리먼트의 크기는 부모의 크기가 기본
- block 엘리먼트의 크기는 기본적으로는 부모의 크기만큼을 가진다.
- width:100%는 부모의 크기만큼을 다 갖는 것과 같다.
### box-sizing과 padding
- padding 속성을 늘리면 엘리먼트의 크기가 달라질 수 있다.
- box-sizing을 content-box가 아닌, border-box로 바꾼다면, padding때문에 box가 커지지 않게 할 수 있다.
### layout 구현 방법은?
- 전체 레이아웃은 float를 잘 사용해서 2단, 3단 컬럼 배치를 구현
- 최근에는 css-grid나 flex속성 등 layout을 위한 속성을 사용하기 시작했다
- 특별한 위치에 배치하기 위해서는 position absolute를 사용하고, 기준점을 relative로 설정한다
- 네비게이션과 같은 엘리먼트는 block 엘리먼트를 inline-block으로 변경해서 가로로 배치하기도 함
- 엘리먼트 안의 텍스트의 간격과, 다른 엘리먼트 간의 간격은 각각 padding과 margin 속성을 활용해서 위치시킨다