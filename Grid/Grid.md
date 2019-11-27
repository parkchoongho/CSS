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

### auto-fill, auto-fit

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
      grid-auto-rows: 120px;
      grid-template-columns: repeat(auto-fit, 40px);
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
      <div class="first"></div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
      <div class="first"></div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
    </div>
  </body>
</html>
```

웹서비스를 구축할 때, 얼만큼의 데이터가 들어올지 예측할 수 없는 경우가 생긴다. 이런 경우에는, 특정 횟수만큼만 반복하는 것을 정하기가 쉽지 않은데 이럴 때, `auto-fit` 을 활용한다. 정해진 범위안에 정해진 크기만큼 최대한 반복하고 싶을 때 활용하는 것이 바로  `auto-fit`이다.

이렇게 `auto-fit` 을 사용하면 flexible한 웹 페이지를 만든 것처럼 보이지만 column의 길이도 결국 고정된 상태에서만 페이지가 작동한다. 따라서 여기서 실제 길이 값 대신, `minmax`를 활용하여 코드를 작성할 수 있다.

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
      grid-auto-rows: 120px;
      grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
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
      <div class="first"></div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
      <div class="first"></div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
    </div>
  </body>
</html>
```

이렇게 코드를 작성하면 상황에 따라 동작하는 responsive한 웹 페이지를 작성할 수 있다. 

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
      grid-auto-rows: 120px;
      grid-template-columns: repeat(auto-fill, minmax(50px, 1fr));
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
      <div class="first"></div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
      <div class="first"></div>
      <div class="second"></div>
      <div class="third"></div>
      <div class="fourth"></div>
    </div>
  </body>
</html>
```

그 다음, `auto-fit`을 `auto-fill` 로 바꿔보자. `auto-fill` 을 사용하면 `ghost-grid`가 생성된다. (`ghost-grid` 는 gird가 브라우저 상에 생기지만 그에 해당하는 블락이 없어 사용자 화면에는 보이지 않는 grid를 의미) 이것이 의미하는 것은 `auto-fill`은 기존에 있는 layout을 채워나가는 방식으로 동작한다는 것이다. (공간을 미리 배정해둔 grid를 생성한 뒤, 해당되는 cell을 그 안에 입력하는 방식)

**Tip**: 개념이 생소해서 조금 어려울 수 있는데, 핵심 차이점은 이것이다. `auto-fit`은 content를 stretch해서 browser를 꽉 채우는 방식이고, `auto-fill`은 최대한 모아서 grid를 만들고 content가 있으면 그 안에 채워넣는 방식으로 생각하면 쉽다.

다음은 auto-fill과 auto-fit 의 차이점을 보여주는 코드이다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>CSS Grid</title>
    <style>
      .container {
        margin: 40px;
        background-color: #00d2d3;
        padding: 10px;
        display: grid;
        grid-gap: 8px;
        grid-template-rows: 50px;
        grid-auto-rows: 50px;
      }
      .container:first-child {
        grid-template-columns: repeat(auto-fill, minmax(50px, 1fr));
      }
      .container:last-child {
        grid-template-columns: repeat(auto-fit, minmax(50px, 1fr));
      }
      .item {
        background-color: #feca57;
      }
    </style>
  </head>

  <body>
    <div class="container">
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
    </div>
    <div class="container">
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
    </div>
  </body>
</html>
```

### Justify Content, Align Content and Place Content

flexbox에 justify와 align이 있는 것처럼, grid에도 justify, align이 있다. 그런데 같은 justify에서도 grid에는 content와 item이 존재한다. `justify-content` 와 `justify-item` 에는 차이점이 존재한다.

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
      grid-auto-rows: 120px;
      grid-template-columns: repeat(4, 100px);
      justify-content: center;
      align-content: center;
      height: 100vh;
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

`justify-content` 의 경우에는 `justify-content:center` 로 코드를 작성하면 box 자체가 브라우저 상에서 중앙으로 이동한다. 만든 grid 전체를 움직이는 것이다. `align-content`의 경우에도 마찬가지다.

`place-content` 라는 property도 존재하는데 첫번째 값은 `align-content` 값이고 두번째 값은  `justify-content` 값이다.

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
      grid-auto-rows: 120px;
      grid-template-columns: repeat(4, 100px);
      place-content: start center;
      height: 100vh;
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

### Justify Items, Align Items and Place Items

box안에 있는 item을 움직이고 싶을 때 사용하는 것이 `justify-items`, `align-items` 이다.

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
      grid-auto-rows: 120px;
      grid-template-columns: repeat(4, 100px);
      justify-items: center;
      height: 100vh;
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
      <div class="first">1</div>
      <div class="second">2</div>
      <div class="third">3</div>
      <div class="fourth">4</div>
    </div>
  </body>
</html>
```

이렇게 코드를 작성하면 item이 box 중앙에 위치한 것을 볼 수 있다. box 자체를 움직이는 것이 아니라 box안에 있는 item을 위치시키는 property이다.

content와 마찬가지로 items에도 `place-items` 가 존재한다.

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
      grid-auto-rows: 120px;
      grid-template-columns: repeat(4, 100px);
      place-items: center center;
      height: 100vh;
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
      <div class="first">1</div>
      <div class="second">2</div>
      <div class="third">3</div>
      <div class="fourth">4</div>
    </div>
  </body>
</html>
```

`place-items` 라는 property도 존재하는데 첫번째 값은 `align-items` 값이고 두번째 값은  `justify-items` 값이다.

### Grid Column, Row Start and End

