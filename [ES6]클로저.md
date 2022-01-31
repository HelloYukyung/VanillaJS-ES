# [ES6] 클로저

클로저는 함수를 지칭하며 또 그 함수가 선언된 어휘적 환경의 조합이다.

먼저 자바스크립트의 어휘적 환경에 대해 알아보자.

```js
//! Lexical 환경
// (hoisting으로 선언된 변수와 함수가 스코프 최상단으로 불러와 진것과 같은 현상이 일어남 )
// one : 초기화 X
// addOne : function

let one;

//! Lexical 환경
// one : undifined
// addOne : function
one = 1;

//! Lexical 환경
// one : 1
// addOne : function

function addOne(num) {
  console.log(one + num);
}
// 위 환경과 같음
addOne(5);
//! 전역 Lexical 환경
// one : 1
// addOne : function

//! 내부 Lexical 환경
// num : 5
```

`addOne(5);`가 호출될 때 새로운 Lexical 환경 추가된다.  
이 환경에서는 함수가 넘겨받은 매개변수와 지역변수가 저장된다.  
함수가 호출되는 동안 내부 렉시컬 환경과 외부(전역) 렉시컬 환경을 2가지를 가지게 되는데,
내부 렉시컬 환경은 외부 렉시컬 환경에 대한 참조를 가진다.  
코드에서 변수를 찾을 때 내부에서 찾고 없으면 그 다음 외부 랙시컬 환경, 그 다음 전역 렉시컬환경으로 범위를 넓혀 찾게된다.  
`function addOne(num) { console.log(one + num); }`
에서는 먼저 내부 Lexical 환경에서 num : 5 를 찾고 그 다음 전역 Lexical 환경에서 one :1을 찾는다.

```js
function makeAdder(x) {
  return function (y) {
    // y를 가지고 있으며, 상위함수인 makeAdder의 매개변수 x에 접근가능함
    return x + y;
  };
}

const add3 = makeAdder(3);
console.log(add3(2)); // add3함수가 생성된 이후에도 상위함수인 makeAdder의 x에 접근가능
// 5

const add10 = makeAdder(10);
console.log(add(5));
console.log(add3(1));
```

위와 같은 것을 Closure라고 한다.  
Closure는 함수와 렉시컬 환경의 조합을 말하며, 함수가 생성될 당시의 외부변수를 기억하며, 생성된 이후에도 그 변수에 계속 접근이 가능하다.

add3과 add10은 서로 다른 환경을 가지고 있다.  
 따라서 `makeAdder(10)`이 호출되어도 아무런 영향을 미치지 않는다.  
add3에 아무런 영향을 미치지 않는다.

```js
function makeCounter() {
  let = num = 0; // 은닉화
  return function () {
    return num++;
  };
}
let counter = makeCounter();

console.log(counter()); // 0
console.log(counter()); // 1
console.log(counter()); // 2
```

내부함수에서 외부함수의 변수를 참조하고 그 값을 계속 기억한다.
