## Grid란?

Grid는 flexbox의 단점을 보완하기 위해 나왔다. (예를 들어, flexbox에 space-between을 주면, 아래로 내려가는 요소들이 브라우저 창의 양 끝단에 배치되는 등의 문제점이 존재. flexbox가 table system이 아닌 점을 보완하기 위해 나온것이 바로 grid!!) 

grid에는 기본적으로 row와 column이 존재한다. flexbox처럼 부모 요소에 grid를 주면 자식요소에 반영된다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>CSS Grid</title>
  </head>
  <style>
    .father {
      display: grid;
      grid-template-rows: 30px 60px;
      grid-template-columns: 20px 50px;
      grid-gap: 10px;
    }
    .child {
      background-color: burlywood;
    }
  </style>
  <body>
    <div class="father">
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
    </div>
  </body>
</html>
```

### grid-template-rows grid-template-columns

`grid-template-rows`와 `grid-template-columns`는 정해진 만큼만 보여줄 수 있다. (tow의 개수가 3개이고 column의 개수가 2개면 총 6개만이 화면에 나타나고 나머지는 숨겨진다.)  그런데 만약에 api 콜을 해서 예상한 것 보다 더 많은 수의 데이터가 왔을 경우에는 어떻게 해야 할까?

그런데, `grid-auto-rows`나 `grid-auto-columns`를 쓰면 자동으로 요소들을 모두 보여줄 수 있다.

```css
.father{
	display: grid;
    grid-template-rows: 300px 120px;
    grid-template-columns: 300px 120px;
    grid-auto-rows: 60px
}
```

이렇게 하면, 자동으로 4개 이후의 grid들은 60px의 높이를 가지고 300px, 120px 너비를 가지면서 배치된다.

```css
.father{
	display: grid;
    grid-template-rows: 300px 120px;
    grid-template-columns: 300px 120px;
    grid-auto-columns: 60px;
}
```

`grid-auto-columns` 도 물론 존재하지만, 위와 같이 코드를 작성하면 작동하지 않는다. 그 이유는 grid에는 초과로 존재하는 children요소를 row 에 놓을지 column에 놓을지 결정하는 속성이 있다. 그것이 바로 `grid-auto-flow` 이다.

```css
.father{
	display: grid;
    grid-template-rows: 300px 120px;
    grid-template-columns: 300px 120px;
    grid-auto-columns: 60px;
    grid-auto-flow: col;
}
```

 `grid-auto-flow`는 flex-direction 비슷하게 동작한다. grid-auto-flow의 defalut 값은 row이다. 이를 통해 수직으로 정렬할지, 수평으로 정렬할지를 정할 수 있다. 

`grid-gap`은 각각의 grid사이의 공간을 얼만큼 둘지를 정의해준다.

