Promise를 선언할 때, resolve와 reject가 있다.

resolve()를 실행하면 다음

```javascript
new Promise(function (resolve, reject) {
  resolve();
});

Promise {<resolved>: undefined}
  __proto__: Promise
  [[PromiseStatus]]: "resolved"
  [[PromiseValue]]: undefined
```

```javascript
// reject에 인자를 넘겨주지 않았을 때
new Promise(function (resolve, reject) {
  reject();
});

Promise {<rejected>: undefined}
  __proto__: Promise
  [[PromiseStatus]]: "rejected"
  [[PromiseValue]]: undefined

// reject에 인자를 넘겨주었을 때
new Promise(function (resolve, reject) {
	reject("Hello");
});

Promise {<rejected>: "Hello"}
  __proto__: Promise
  [[PromiseStatus]]: "rejected"
  [[PromiseValue]]: "Hello"
```

```javascript
// resolve, reject
new Promise(function (resolve, reject) {
  resolve();
	reject();
});

// reject, resolve
new Promise(function (resolve, reject) {
  reject();
  resolve();
});
```

