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

### grid-template-rows, grid-template-columns

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

### grid-template-areas

`grid-template-areas` 는 css단에서 무언가를 그릴 수 있게하는 기능이다.

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
      grid-auto-rows: 150px;
      grid-gap: 10px;
      grid-template-areas: "header header header" "main main sidebar" "main main sidebar" "footer footer footer";
    }
    .first {
      grid-area: header;
      background-color: #e74c3c;
    }
    .second {
      grid-area: main;
      background-color: #f39c12;
    }
    .third {
      grid-area: sidebar;
      background-color: #f1c40f;
    }
    .fourth {
      grid-area: footer;
      background-color: #1abc9c;
    }
  </style>
  <body>
    <div class="father">
      <div class="first"></div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
    </div>
  </body>
</html>
```

이렇게 코드를 짜면 `grid-template-areas` 를 활용해 화면을 구성할 수 있다. first 클래스 selector는 `grid-area`가 header로 `grid-template-areas` 에서 가장 위쪽에 설정되어 있으므로 위에 들어가게 됩니다. fourth 클래스 selector는 footer로 `grid-template-areas` 에서 가장 밑쪽에 설정되어 있어 밑에 부분에 영향을 주게됩니다.

### fr & repeat

fr(fraction, 최대한 공간을 차지한다는 의미)은 grid에서 사용하는 단위로 반응형 웹을 디자인할 때, 다른 계산을 필요로 하지 않는 장점을 가진다.

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
      grid-auto-rows: 150px;
      grid-gap: 10px;
      grid-template-columns: 1fr 2fr 3fr 4fr;
    }
    .first {
      background-color: #e74c3c;
    }
    .second {
      background-color: #f39c12;
    }
    .third {
      background-color: #f1c40f;
    }
    .fourth {
      background-color: #1abc9c;
    }
  </style>
  <body>
    <div class="father">
      <div class="first"></div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
    </div>
  </body>
</html>
```

이렇게 코드를 작성하면 자동으로 브라우저 화면에 맞게 크기를 할당해준다. 첫번째 column은 1의 크기, 두번째는 그 2배, 3번째는 그 3배, 마지막 4번째는 4배 이렇게 화면에 크기를 할당해 배치한다.

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
      grid-auto-rows: 150px;
      grid-gap: 10px;
      grid-template-columns: repeat(3, 1fr) 4fr 2fr;
    }
    .first {
      background-color: #e74c3c;
    }
    .second {
      background-color: #f39c12;
    }
    .third {
      background-color: #f1c40f;
    }
    .fourth {
      background-color: #1abc9c;
    }
  </style>
  <body>
    <div class="father">
      <div class="first"></div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
    </div>
  </body>
</html>
```

repeat은 column을 반복시켜주는 함수이다. `grid-template-columns` 에서 `repeat(5, 1fr)` 라고 설정해주면 같은 크기의 column을 5개 생성한다.

위와 같이 코드를 작성하면 repeat 함수로 3개 뒤에 2개의 column이 생기는데 html 상 child 요소는 4개 밖에 없다. 1개를 초과했는데, 그것과 상관없이 column을 생성한다. (화면상에서는 아무것도 없는 것처럼 보인다.)

### minmax, max-content, min-content

`minmax`는 내가 사용할 object의 maximum과 minimum 크기를 지정해주는 도구이다.

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
      grid-auto-rows: 150px;
      grid-gap: 10px;
      grid-template-columns: minmax(200px, 1fr) minmax(50px, 2fr) repeat(3, 1fr);
    }
    .first {
      background-color: #e74c3c;
    }
    .second {
      background-color: #f39c12;
    }
    .third {
      background-color: #f1c40f;
    }
    .fourth {
      background-color: #1abc9c;
    }
  </style>
  <body>
    <div class="father">
      <div class="first"></div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
    </div>
  </body>
</html>
```

위에 코드는 총 5개의 column을 만든다. 첫번째 column은 최소 길이가 200px이고 최대 1fr까지 가진다. 이 말은 브라우저가 충분히 클때는 1fr의 길이를 가지지만 브라우저가 줄어들 때, 1fr이 200px보다 작아지면 이 column은 200px를 계속 유지하고 그 밑으로는 더 이상 줄어들지 않는다는 의미이다.

`max-content`는 안에 있는 content를 기반으로 사용할 수 있는 최대공간을 정할 수 있게 해주는 도구이다. Title을 설정할 때 유용하게 쓰이는 방식이다.

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

      grid-gap: 10px;
      grid-template-columns: minmax(min-content, 1fr) 1fr repeat(2, 1fr);
    }
    .first {
      background-color: #e74c3c;
    }
    .second {
      background-color: #f39c12;
    }
    .third {
      background-color: #f1c40f;
    }
    .fourth {
      background-color: #1abc9c;
    }
  </style>
  <body>
    <div class="father">
      <div class="first">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis
        repellat nulla eaque facere ullam ratione voluptas quia deserunt
        incidunt nam voluptatem fuga in enim alias unde, quo perspiciatis quas.
        Rerum.
      </div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
    </div>
  </body>
</html>
```

이렇게 `max-content` 를 활용하면 1번째 column의 content 크기가 너무커서 1번째 column만 화면에 나타나고 나머지는 나타나지 않는다.

`min-content`는 크기를 줄일 수 있는 만큼 줄이라는 의미다. (`max-content` 와 정반대의 의미!!) 

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

      grid-gap: 10px;
      grid-template-columns: minmax(min-content, 1fr) 1fr repeat(2, 1fr);
    }
    .first {
      background-color: #e74c3c;
    }
    .second {
      background-color: #f39c12;
    }
    .third {
      background-color: #f1c40f;
    }
    .fourth {
      background-color: #1abc9c;
    }
  </style>
  <body>
    <div class="father">
      <div class="first">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis
        repellat nulla eaque facere ullam ratione voluptas quia deserunt
        incidunt nam voluptatem fuga in enim alias unde, quo perspiciatis quas.
        Rerum.
      </div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
    </div>
  </body>
</html>
```

위 같은 경우는 1번째 column의 최소 크기를 `min-content`로 설정해 놓았기 때문에 화면 크기를 변경해도 다른 column을 침범하지 않고 1fr을 유지하면서 변화된다. (개인적으로 긴 content를 화면에 보여줄 때 `minmax` 의 첫번째 인자로 `min-content` 를 활용하는 것이 유용한것같다.)

참고링크: https://justmakeyourself.tistory.com/entry/grid-extra

