# Javascript - 직접 구현하면서 배우는 Promise

## 비동기와 콜백

### 비동기? 동기?

자바스크립트에 대해 공부하거나, 이와 관련된 프레임워크에 대해 공부하다보면 비동기라는 단어를 자주 볼 수 있다. 자바스크립트에서 비동기는 빼놓을 수 없는 부분이다. 비동기를 공부하기에 앞서 먼저 동기에 대해 알아야 한다.

먼저 **동기(Synchronous)**는 간단하다.

```javascript
const pause = (milliseconds) => {
	let dt = new Date();
	while ((new Date()) - dt <= milliseconds) {}
} 

console.log("Hello! wait for 3seconds!");
pause(3000);
console.log("Thanks for waiting!");
```

