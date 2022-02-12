# [ES6] async-await

async function()은 await 키워드가 비동기 코드를 호출할 수 있게 해주는 함수다.

## async

```js
function hello() {
  return "Hello";
}
hello();
// 'Hello'
```

```js
async function hello() {
  return "Hello";
}
hello();
// Promise {<fulfilled>: 'Hello'}
```

async 키워드를 사용하면 반환받는 값은 Promise를 반환한다.

## await

```js
function printAfter(seconds) {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("print " + seconds);
      resolve(seconds);
    }, seconds * 1000);
  });
}

async function log() {
  const data1 = await printAfter(3); // 3 초 뒤 출력
  const data2 = await printAfter(5); // 8 초 뒤 출력
  console.log(data1, data2);
}

log();
// print 3
// print 5
// 3 5
```

await 키워드는 async 함수 내부에서만 사용된다.

await 키워드를 붙여서 프로미스를 사용하면 해당 프로미스가 처리됨 상태가 될 때까지 기다린다.
