# Javascript DOM - 노드(Node)에 요소(Element)를 복수 삽입하는 다양한 방법

> https://javascript.info/dom-nodes
>
> https://learn.javascript.ru/multi-insert

Javascript의 주목적이라 할 수 있는 DOM을 조작하는 방법은 다양하다. 그 중 DOM을 수정하는 것은 웹 페이지를 만드는 데 있어 핵심이라고 할 수 있다. 

## Element 만들기 

DOM 노드를 만드는 방법은 두 가지가 있다. 하나는 우리가 흔히 아는 태그에 해당하는 노드(Node)를 생성하고, 다른 하나는 조금 생소할 수 있는 텍스트 노드(Text Node)를 생성한다.

* `document.createElement(tagName)`
* `document.createTextNode(text)`



```javascript
let div = document.createElement('div');
```



```javascript
let textNode = document.createTextNode('This is text');
```



```javascript
let div = document.createElement('div');
let textNode = document.createTextNode('This is text');
div.appendChild(textNode);
```



```javascript
let div = document.createElement('div');
div.innerHTML = 'This is text';
```

