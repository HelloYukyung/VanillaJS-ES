# [ES6] const

const 선언은 블록 범위의 상수를 선언한다.  
상수의 값은 재할당할 수 없으며 다시 선언할 수도 없다.

```js
const number = 42;

try {
  number = 99;
} catch (err) {
  console.log("err =>>", err);
  // err =>> TypeError: Assignment to constant variable.
}

console.log(number);
// 42
```

const 선언은 선언된 함수에 전역 또는 지역일 수 있는 상수를 만든다.
상수 초기자(initializer)가 필요하다.  
즉 선언되는 같은 문에 그 값을 지정해야 한다.

```js
const COLOR = "green";
COLOR = "red";
// 에러발생

const COLOR = "yellow";
// 상수를 재선언 하는 시도도 애러 발생

var COLOR = "yellow";
// var 선언 또한 위에서 상수로 예약되어 있어 에러

let COLOR = "yellow";
// 마찬가지로 에러
```

상수는 let 문을 사용하여 정의된 변수와 마찬가지로 블록 범위(block-scope)이다.  
상수의 값은 재할당을 통해 바뀔 수 없고 재선언될 수 없다.

상수는 같은 범위의 상수 또는 변수와 그 이름을 공유할 수 없다.

```js
const MY_FAV = 7;

if (MY_FAV === 7) {
  // 블록 범위로 지정된 MY_FAV 라는 변수를 만드므로 정상 동작
  const MY_FAV = 20;
  console.log("my favorite number is " + MY_FAV);
}
console.log(MY_FAV);

// my favorite number is 20
// 7
```

let에 적용한 "일시적 사각 지대"에 관한 모든 고려는, const에도 적용된다.

```js
// const는 오브젝트에도 잘 동작한다.
const MY_OBJECT = { key: "value" };

// 오브젝트 역시 덮어쓰면 오류가 발생한다.
MY_OBJECT = { OTHER_KEY: "value" };

// 하지만 오브젝트의 키는 보호되지 않는다.
// 따라서 아래 문장은 문제없이 실행된다.
// 오브젝트를 변경할 수 없게 하려면 Object.freeze() 를 사용한다.
// Object.freeze(MY_OBJECT);

MY_OBJECT.key = "otherValue";
// 배열에도 똑같이 적용된다.
const MY_ARRAY = [];
// 배열에 아이템을 삽입하는 건 가능하다.
MY_ARRAY.push("A");
// ["A"]

// 하지만 변수에 새로운 배열을 배정하면 에러가 발생한다.
MY_ARRAY = ["B"];
// TypeError: Assignment to constant variable.
```
