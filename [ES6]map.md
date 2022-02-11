# [ES6] map

map() 메서드는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환한다.

```js
let numbers = [1, 2, 3, 4, 5];

let result = numbers.map((num) => {
  return num * num;
});
```
