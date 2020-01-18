# Create-React-App 없이 리액트



```bash
npm init -y
npm install react react-dom
```
다음과 같이 `react`와 `react-dom`패키지를 다운로드하고 node_modules폴더에 들어가면 새로 react와 react-dom 폴더가 생겼다. 그 외에도 많은 폴더가 생겼는데 모두 react와 react-dom 패키지를 올바르게 사용하기 위해 필요한 패키지들이다.

`.gitignore` 을 만들고 아래와 같이 작성한다.

```javascript
node_modules
.DS_Store
dist
```

app폴더를 만들고 `index.js` 와 `index.css` 를 생선한다.

```javascript
var React = require("react");

class App extends React.Component {
  render() {
    return <div>Helllo world</div>;
  }
}
```

위의 코드를 babel은 아래와 같이 변환한다. 위의 코드를 JSX라고하고 이를 babel이 js코드로 변환한다.

```javascript
class App extends React.Component {
  render() {
    return React.createElement(
        "div", 
        null, 
        "Helllo world");
  }
}
```

아래와 같이 ReactDOM을 이용하여 `app`에 우리가 만든 컴포넌트를 붙여준다. 그리고 `index.css` 를 import한다.

```javascript
var React = require("react");
var ReactDOM = require("react-dom");
require("index.css");

class App extends React.Component {
  render() {
    return <div>Helllo world</div>;
  }
}

ReactDOM.render(
  <App />, 
  document.getElementById("app")
);
```

이대로 빌드하면 제대로 작동하지 않을 것이다. 

```bash
npm install --save-dev @babel/core @babel/preset-env @babe
l/preset-react webpack webpack-cli webpack-dev-server babel-
loader css-loader style-loader html-webpack-plugin
```

* @babel/core 
* @babel/preset-env 
* @babel/preset-react 
* webpack 
* webpack-cli 
* webpack-dev-server 
* babel-loader 
* css-loader 
* style-loader 
* html-webpack-plugin

devDependencies를 분리하여 개발할 때만 쓴다(빌드할 때).

```json
  "dependencies": {
    "react": "^16.9.0",
    "react-dom": "^16.9.0"
  },
  "devDependencies": {
    "@babel/core": "^7.5.5",
    "@babel/preset-env": "^7.5.5",
    "@babel/preset-react": "^7.0.0",
    "babel-loader": "^8.0.6",
    "css-loader": "^3.2.0",
    "html-webpack-plugin": "^3.2.0",
    "style-loader": "^1.0.0",
    "webpack": "^4.39.2",
    "webpack-cli": "^3.3.7",
    "webpack-dev-server": "^3.8.0"
  }
```



여기서 output은 `directory name/dist/index_bundle.js`와 같은데 우리가 웹팩을 실행하면 앞의 경로로 파일을 생성한다.

```javascript
var path = require("path");

module.exports = {
  entry: "./app/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "index_bundle.js"
  }
};
```

react에서 JSX를 javascript로 변환해주기 위해 두가지 바벨 규칙을 추가한다.

```javascript
var path = require("path");

module.exports = {
  entry: "./app/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "index_bundle.js"
  },
  module: {
    rules: [
      { test: /\.(js)$/, use: "babel-loader" },
      { test: /\.css$/, use: ["style-loader", "css-loader"] }
    ]
  }
};

```

* babel-loader
  * 자바스크립트 파일을 변환하여 붙여줌
* style-loader
  * CSS파일을 변환하여 붙여줌
* css-loader
  * `url(../background.png')`를 `require('')`로 바꿔줌

그리고 현재 모드는 개발이기 때문에 `development`를 추가한다. 배포할 때는 `production`으로 변경하면 된다.

```javascript
var path = require("path");

module.exports = {
  entry: "./app/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "index_bundle.js"
  },
  module: {
    rules: [
      { test: /\.(js)$/, use: "babel-loader" },
      { test: /\.css$/, use: ["style-loader", "css-loader"] }
    ]
  },
  mode: "development"
};
```

`html-webpack-plugin`는 index.html을 생성하고 거기에 index_bundle.js를 embed한다.

```javascript
var path = require("path");
var HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./app/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "index_bundle.js"
  },
  module: {
    rules: [
      { test: /\.(js)$/, use: "babel-loader" },
      { test: /\.css$/, use: ["style-loader", "css-loader"] }
    ]
  },
  mode: "development",
  plugins: [
    new HtmlWebpackPlugin({
      template: "app/index.html"
    })
  ]
};
```

`@babel/preset-env`는 class같은 최신 JS를 옛 브라우저도 지원할 수 있도록 바꿔주는 것을 돕는다.

 `@babel/preset-react` 는 리액트 내의 JSX를 컴파일 하는것을 도와준다.

```json
{
  "name": "create-react",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "babel": {
    "presets": [
      "@babel/preset-env",
      "@babel/preset-react"
    ]
  },
  "scripts": {
    "create": "webpack",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

rmfl

```bash
npm run create
```

에러가 난다. 

```bash
ERROR in ./app/index.js
Module not found: Error: Can't resolve 'index.css' in '/Users/soonho/project/temp/create-react/app'
 @ ./app/index.js 23:0-20
```

해당 지점으로가서 `index.css`를 `./index.css`로 수정하고 다시 create한다.

성공한다. dist에 만들어진 파일을 확인한다. index.html에 제대로 script링크로 index_bundle을 불러오는지 볼 수 있다.