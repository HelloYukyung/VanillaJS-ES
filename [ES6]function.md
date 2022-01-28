# function

함수는 JavaScript에서 기본적인 구성 블록 중의 하나이다.  
함수는 작업을 수행하거나 값을 계산하는 문장 집합 같은 자바스크립트 절차이다.  
함수를 사용하려면 함수를 호출하고자 하는 범위 내에서 함수를 정의해야만 한다.

## 함수 정의(선언)

함수 정의(혹은 선언)은 3가지 함수 키워드로 구성되어 있다.

- 함수의 이름
- 괄호 안에서 쉼표로 분리된 함수의 매개변수 목록
- 중괄호`{}`안에서 함수를 정의하는 자바스크립트 표현

```js
function square(number) {
  return number * number;
}
```

예를들어 함수 square은 number라는 하나의 매개변수를 가진다.  
이 함수는 인수 (즉, number) 자체를 곱하여 반환하는 하나의 문장으로 구성되어 있다.  
return 문은 함수에 의해 반환된 값을 지정한다.

참고: 매개변수와 인수

- 매개변수:함수 등에서 사용되는 전달된 값을 받는 변수
- 인수:값, 변수, 참조 등 전달되는 값

```js
return number * number;
```

기본 자료형인 매개변수(number와 같은)는 값으로 함수에 전달된다.  
그러나 함수가 매개변수의 값을 바꾸더라도 이는 전역적으로 또는 함수를 호출하는 곳에는 반영되지 않는다.

```js
function myFunc(theObject) {
  theObject.make = "Toyota";
}

var mycar = { make: "Honda", model: "Accord", year: 1998 };
var x, y;

x = mycar.make;
// x 의 값은 "Honda"

myFunc(mycar);
y = mycar.make;
// y 의 값은 "Toyota"
// (make 속성은 myFunc에서 변경되었음)
```

만약 매개변수로 (예: Array이나 사용자가 정의한 객체와 같이 기본 자료형이 아닌 경우)를 전달하거나 함수가 객체의 속성을 변하게 하는 경우,위 코드처럼 그 변화는 함수 외부에서도 볼 수 있다.

## 함수 표현식

위에서 함수 선언은 구문적인 문(statement)이지만, 함수 표현식( function expression)에 의해서 함수가 만들어 질 수도 있다.  
이 같은 함수를 익명이라고 한다.  
이 말은 모든 함수가 이름을 가질 필요는 없다는 것을 뜻한다.  
예를 들어, 함수 square은 다음과 같이 정의 될 수도 있다.

```js
var square = function (number) {
  return number * number;
};
var x = square(4);
// x 의 값은 16
```

하지만, 함수 표현식에서 함수의 이름을 지정 할 수 있으며, 함수내에서 자신을 참조하는데 사용되거나, 디버거 내 스택 추적에서 함수를 식별하는 데 사용될 수 있다.

```js
var factorial = function fac(n) { return n<2 ? 1 : n\*fac(n-1) };

console.log(factorial(3));
```

## 함수 호출

함수를 정의하는 것은 함수를 실행한 것이 아니다.
함수를 정의하는 것은 간단히 함수의 이름을 지어주고, 함수가 호출될 때 무엇을 할지 지정 해주는 것이다.

예를 들어,함수 square를 정의했다면, 함수를 다음과 같이 호출할 수 있다.

```
square(5);

```

위의 문장은 5라는 인수를 가지고 함수를 호출한다.
함수는 이 함수의 실행문을 실행하고 값 25를 반환한다.

### 함수 호이스팅

```js
// 함수 참조
console.dir(add); // output: f add(x, y)
console.dir(sub); // output: undefined

// 함수 호출
console.log(add(2, 5)); // output: 7
console.log(sub(2, 5)); // output: Uncaught TypeError: sub is not a function

// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 표현식
var sub = function (x, y) {
  return x + y;
};
```

함수 선언문의 경우, 런타임 이전에 자바스크립트 엔진에서 먼저 실행되어, 함수 자체를 호이스팅 시킬 수 있다.

반면, 함수 표현식은 위에서 봤던 변수 호이스팅과 같이 런타임 이전에 해당 값을 undefined로 초기화만 시키고, 런타임에서 해당 함수 표현식이 할당되어 그때 객체가 된다.

```js
console.log(square); // square는 초기값으로 undefined를 가지고 호이스트된다.
console.log(square(5)); // TypeError: square는 함수가 아니다.
square = function (n) {
  return n * n;
};
```

## 함수의 범위

함수 내에서 정의된 변수는 변수가 함수의 범위에서만 정의되어 있기 때문에, 함수 외부의 어느 곳에서든 액세스할 수 있다.  
그러나, 함수가 정의된 범위 내에서 정의된 모든 변수나 함수는 액세스할 수 있다. 즉, 전역함수는 모든 전역 변수를 액세스할 수 있다.  
다른 함수 내에서 정의 된 함수는 부모 함수와 부모 함수가 액세스 할 수 있는 다른 변수에 정의된 모든 변수를 액세스할 수 있다.

```js
// The following variables are defined in the global scope
var num1 = 20,
  num2 = 3,
  name = "Chamahk";

// This function is defined in the global scope
function multiply() {
  return num1 * num2;
}

multiply();
// 60

// A nested function example
function getScore() {
  var num1 = 2,
    num2 = 3;

  function add() {
    return name + " scored " + (num1 + num2);
  }

  return add();
}

getScore();
// Chamahk scored 5
```
