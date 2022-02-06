# [ES6] Promise

Promise 객체는 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타낸다.

```js
const promise = new Promise((resolve, reject) => {
  try {
    ...비동기 작업
    resolve(결과);
  } catch (err) {
    reject(err);
  }
});
```

## Promise의 상태

Promise는 3가지 상태를 갖는다.

- Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
- Fulfilled(이행,완료) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

```js
new Promise();
```

위와같이 Promise 메서드를 호출하면 Pending(대기)상태가 된다.

```js
new Promise(function (resolve, reject) {
  // ...
});
```

new Promise() 메서드를 호출할 때 콜백 함수를 선언할 수 있으며, 콜백 함수의 인자는 resolve, reject다.

```js
function getData() {
  return new Promise(function (resolve, reject) {
    var data = 100;
    resolve(data);
  });
}

// resolve()의 결과 값 data를 resolvedData로 받음
getData().then(function (resolvedData) {
  console.log(resolvedData); // 100
});
```

여기서 콜백 함수의 인자 resolve를 위와 같이 실행하면 이행(Fulfilled) 상태가 되고 then을 이용해 처리 결과값을 받을 수 있다.

```js
function getData() {
  return new Promise(function (resolve, reject) {
    reject(new Error("Request is failed"));
  });
}

// reject()의 결과 값 Error를 err에 받음
getData()
  .then()
  .catch(function (err) {
    console.log(err); // Error: Request is failed
  });
```

reject를 위와 같이 호출하면 실패(Rejected) 상태가 된다.  
그리고, 실패 상태가 되면 실패한 이유(실패 처리의 결과 값)를 catch()로 받을 수 있다.
