# 화살표 함수

화살표 함수 표현(arrow function expression)은 전통적인 함수표현(function)의 간편한 대안이다.  
 하지만, 화살표 함수는 몇 가지 제한점이 있고 모든 상황에 적용될 수 는 없다.

```js
let sum = (a, b) => a + b;
```

```js
let sum = function (a, b) {
  return a + b;
};

alert(sum(1, 2)); // 3
```

화살표 함수로 표현된 `(a,b)=> a+b`는 인수 a와 b를 받는 함수이며, 실행되는 순간 표현식 `a+b`를 반환한다.

```js
let sayHi = () => alert("안녕하세요!");

sayHi();
```

인수가 하나도 없을 땐 괄호를 비워놓으면 된다.  
이 때 괄호는 생략할 수 없다.

```js
let age = prompt("나이를 알려주세요.", 18);

let welcome = age < 18 ? alert("안녕") : () => alert("안녕하세요!");

welcome();
```

화살표 함수는 처음 접하면 가독성이 떨어지나 이는 익숙하지 않기 때문이다.
타이핑을 적게 해도 함수를 만들 수 있다는 장점이 있습니다.

## 본문이 여러 줄인 화살표 함수

평가해야 할 표현식이나 구문이 여러개인 함수인 경우 중괄호를 사용해 평가해야 할 코드를 넣어준다.
그리고 중괄호를 사용했다면, `return` 지시자를 사용해 명시적으로 결과값을 반환해 주어야 한다.

```js
let sum = (a, b) => {
  let result = a + b;
  return result;
};

alert(sum(1, 2)); // 3
```

### 예제1

```js
function ask(question, yes, no) {
  if (confirm(question)) yes();
  else no();
}

ask(
  "동의하십니까?",
  function () {
    alert("동의하셨습니다.");
  },
  function () {
    alert("취소 버튼을 누르셨습니다.");
  }
);
```

다음 코드를 화살표 함수로 바꿔보기

```js
function ask(question, yes, no) {
  if (confirm(question)) yes();
  else no();
}

ask(
  "동의하십니까?",
  () => alert("동의하셨습니다."),
  () => alert("취소 버튼을 누르셨습니다.")
);
```

- this나 super에 대한 바인딩이 없고, methods 로 사용될 수 없다.
- new.target키워드가 없다.
- 일반적으로 스코프를 지정할 때 사용하는 call, apply, bind methods를 이용할 수 없다.
- 생성자(Constructor)로 사용할 수 없다.
- yield를 화살표 함수 내부에서 사용할 수 없다.
