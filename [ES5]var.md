# [ES6] var

var문은 변수를 선언하고 선택적으로 초기화할 수 있다.  
var로 선언한 변수는 블록 범위를 가지지 않는다.  
즉, 블록 내에서 선언한 변수일지라도 값의 할당의 영향이 블록 바깥까지 미친다.
(블록문이 범위를 만들지 않음)

```js
var x = 1;

if (x === 1) {
  var x = 2;

  console.log(x);
  // 2
}

console.log(x);
// 2
```

## 선언된 변수와 선언되지 않은 변수의 차이점

1. 선언된 변수들은 변수가 선언된 실행 콘텍스트 안에서 만들어지는 반면, 선언되지 않은 변수들은 항상 전역변수이다.

```js
function x() {
  y = 1; // strict 모드에서는 ReferenceError를 출력합니다.
  var z = 2;
}

x();

console.log(y); // 1
console.log(z); // ReferenceError: z is not defined outside x
```

2. 선언된 변수들은 어떠한 코드가 실행되기 전에 만들어진다.  
   반면, 선언되지 않은 변수들은 변수들을 할당하는 코드가 실행되기 전까지는 존재하지 않는다.

```js
console.log(a);
// Uncaught ReferenceError: a is not defined
```

```js
var a;
undefined;
console.log(a);
//undefined;
// 브라우저에 따라 로그에 "undefined" 또는 "" 가 출력된다.
```

3. 선언된 변수들은 변수들의 실행 콘텍스트(execution context)의 프로퍼티를 변경하지 않는 반면, 선언되지 않은 변수들은 변경이 가능하다. (e.g 삭제 될 수도 있다.)

```js
var a = 1;
b = 2;

delete this.a; // false
delete this.b;

console.log(a, b);
//ReferenceError: b is not defined
//'b' 프로퍼티는 삭제되었으며, 어디에도 존재하지 않는다.
```

위와같은 3가지 다른 점 때문에 변수 선언 오류는 예기치않은 결과로 이어질 가능성이 높다.  
그러므로 함수 또는 전역 변수인지 여부와 상관없이 항상 변수를 선언해줘야 한다.
