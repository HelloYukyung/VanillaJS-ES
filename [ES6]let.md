# [ES6] let

let 명령문은 블록 스코프의 범위를 가지는 지역 변수를 선언하며, 선언과 동시에 임의의 값으로 초기화할 수도 있다.

```js
let x = 1;

if (x === 1) {
  let x = 2;

  console.log(x);
  // 2
}

console.log(x);
// 1
```

let을 사용하면 블록 명령문이나 let을 사용한 표현식 내로 범위가 제한되는 변수를 선언할 수 있다.  
이는 let이 var 키워드와 다른 점으로, var는 변수를 블록을 고려하지 않고 현재 함수 (또는 전역 스코프) 어디에서나 접근할 수 있는 변수를 선언한다.  
 또한 let은 파서가 구문을 평가해야만 변수를 값으로 초기화(아래 참고)한다는 점도 var와 다르다.

## 스코프 규칙

let으로 선언한 변수는 자신을 선언한 블록과 모든 하위 블록을 스스로의 스코프로 가집니다. 이런 점에서는 let이 var와 유사하다. 그러나 둘의 중요한 차이는, var의 경우 스코프가 '자신을 선언한 블록'이 아니라, 자신의 선언을 포함하는 함수라는 점이다.

```js
function varTest() {
  var x = 1;
  if (true) {
    var x = 2; // 같은 변수
    console.log(x); // 2
  }
  console.log(x); // 2
}

function letTest() {
  let x = 1;
  if (true) {
    let x = 2; // 다른 변수
    console.log(x); // 2
  }
  console.log(x); // 1
}
```

```js
var x = "global";
let y = "global";
console.log(this.x); // "global"
console.log(this.y); // undefined
```

또한 프로그램 최상단에서 실행했을 때,var는 전역 객체에 속성을 추가하지만 let은 추가하지 않는다.

```js
let x = 1;

{
  var x = 2; // 재선언으로 인한 SyntaxError
}
```

var와 let을 아래와 같이 사용하면 SyntaxError이다. 호이스팅으로 인해 var가 블록 최상단으로 끌어올려져, 변수 재선언을 하는 것과 같아지기 때문이다.

## 재선언

```
if (x) {
  let foo;
  let foo; // SyntaxError
}
```

같은 변수를 같은 함수나 블록 스코프 안에서 다시 선언하려고 시도하면 SyntaxError가 발생한다.

```js
let x = 1;

switch (x) {
  case 0: {
    let foo;
    break;
  }
  case 1: {
    let foo;
    break;
  }
}
```

하지만 위 코드와 같이, 분기에 블록을 배치하면 블록 스코프도 생성하므로 재선언으로 인한 오류가 발생하지 않는다.

## 시간상 사각지대

let 변수는 초기화하기 전에는 읽거나 쓸 수 없다. (선언 구문에 초기 값을 지정하지 않은 경우 undefined로 초기화).  
 초기화 전에 접근을 시도하면 ReferenceError가 발생한다.

```js
function do_something() {
  console.log(bar); // undefined
  console.log(foo); // ReferenceError
  var bar = 1;
  let foo = 2;
}
```

var의 경우 선언 전에 접근할 시 undefined이며,
var 키워드와는 다르게 선언단계와 초기화 단계가 분리되어서 진행된다.  
그렇기 때문에 실행 컨텍스트에 변수를 등록했지만,
메모리가 할당이 되질 않아 접근할 수 없어 참조 에러(ReferenceError)가 발생한다.

"시간상" 사각지대인 이유는, 사각지대가 코드의 작성 순서(위치)가 아니라 코드의 실행 순서(시간)에 의해 형성되기 때문입니다.

```js
{
  // TDZ가 스코프 맨 위에서부터 시작
  const func = () => console.log(letVar); // OK

  // TDZ 안에서 letVar에 접근하면 ReferenceError

  let letVar = 3; // letVar의 TDZ 종료
  func(); // TDZ 밖에서 호출함
}
```

위 코드의 경우, let 변수 선언 코드가 그 변수에 접근하는 함수보다 아래에 위치하지만, 함수의 호출 시점이 사각지대 밖이므로 정상 동작한다.
