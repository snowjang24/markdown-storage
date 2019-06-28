# Javascript파일을 로컬에서 component화

항상 프레임워크를 쓰거나 한 파일에 몰아 넣는 식으로 작업했는데, 처음으로 javascript파일을 component로 나누어 사용해보았다. 여기서 알 수 없는 오류로 삽질하며 시간을 낭비했다. 인터넷에 아무리 찾아봐도 찾을 수가 없었지만 Jin의 도움으로 쉽게 해결할 수 있었다. 같은 실수를 반복하지 않기 위해 이렇게 글을 남긴다.

## import와 export 그리고 HTML에서의 javascript module 

미션으로 주어진 Amazon의 Carousel에서 Navigator를 분리하여 두 개의 컴포넌트로 만들어주려 했다. 

먼저 의도했던 파일 tree는 다음과 같다. `Carousel`과 `Navigator`를 나누어 `app.js`에서 불러와 사용하고자 했다.

```bash
├── javascript-amazon
|  ├── app.js
|  ├── index.html
|  ├── components
|  |   ├── Carousel.js
|  |   └── Navigator.js
|  ├── images
|  └── styles
```

이를 위해 Carousel과 Navigator에는 각각 다음과 같은 형태로 `export`하였다. 

```javascript
// ./components/Carousel.js
class Carousel {
    //Some Code...
}

export default Carousel
```

Carousel component를 기본으로 `export`하여 `app.js`에서 불러와 바로 사용하고자 했다. 이를 위해 `app.js`에서는 다음과 같은 방식으로 `import` 하였다.

```javascript
// ./app.js
import carousel from './components/Carousel'

const carousel = new Carousel({ leftBtn, rightBtn, numberOfCard });
```

그 결과 브라우저에서 빨간 X표를 볼 수 있었고, 알 수 없는 에러를 보게 되었다. 

```bash
app.js:1 Uncaught SyntaxError: Unexpected identifier
```

아래의 이 한 줄에 빨간줄이 생기며 문제가 있다고 뜬다.

```javascript
import Carousel from "./components/Carousel";
```

인터넷에 검색해보면 검색결과는 몇 없지만 가장 가능성 있어 보이는 원인을 발견했다. html에서 불러 올 때 `type`을 `module`로 불러오지 않아서 그렇다고 했다. 이를 해결하기 위해 `type="text/javascript"`였던 부분을 `type="module"`로 바꿔주었다.

```html
<script src="app.js" type="module"></script>
```

두근두근하며 다시 live server extension을 켰다. 하지만 이번에는 다른 이유로 빨간 X를 보게 되었다.

```bash
app.js:1 GET http://127.0.0.1:5500/javascript-amazon/components/Carousel net::ERR_ABORTED 404 (Not Found)
```

같은 위치에 다른 에러다. 코딩을 하다가 난 오류도 아니고 경로 하나 잡지 못하는 것에 대한 분노로 머리가 지끈지끈했다.

덮었다... 덮고 다음날 Jin에게 해결 방법을 물어보니 간단히 해결되었다.

`./components/Carousel`와 같이 javascript파일임을 명시하지 않아도 당연히 받아올 줄 알았지만 아니었다. html에서 app.js를 모듈의 형태로 불러올 때는, 정확히 파일을 명시해줘야 하는 것 같다. 

```javascript
import Carousel from "./components/Carousel.js";
```

자세한 이유는 다음에 다시 조사해보려 한다.