# method & this

```js
let user = {
  name: "John",
  age: 30,
};
```

객체는 사용자(user), 주문(order) 등과 같이 실제 존재하는 개체(entity)를 표현하고자 할 때 생성된다.  
사용자는 현실에서 장바구니에서 물건 선택하기, 로그인하기, 로그아웃하기 등의 다양한 행동을 한다.  
이와 마찬가지로 사용자를 나타내는 객체 user도 특정한 행동을 할 수 있다.  
자바스크립트에선 객체의 프로퍼티에 함수를 할당해 객체에게 행동할 수 있는 능력을 부여해준다.

```js
let user = {
  name: "John",
  age: 30,
};

user.sayHi = function () {
  alert("안녕하세요!");
};

user.sayHi();
// 안녕하세요!
```

함수 표현식으로 함수를 만들고, 객체 프로퍼티 user.sayHi에 함수를 할당해 주었다.  
객체에 할당된 함수를 호출하면 user가 인사를 해준다.  
이렇게 객체 프로퍼티에 할당된 함수를 메서드(method)라고 부른다.  
위 예시에선 user에 할당된 sayHi가 메서드이다.

```js
let user = {
  name: "John",
  age: 30,
};

// 함수 선언
function sayHi() {
  alert("안녕하세요!");
}

// 선언된 함수를 메서드로 등록
user.sayHi = sayHi;

user.sayHi();
// 안녕하세요!
```

메서드는 이미 정의된 함수를 이용해서 만들 수도 있다.

## 메서드와 this

메서드는 객체에 저장된 정보에 접근할 수 있어야 제 역할을 할 수 있다.  
대부분의 메서드가 객체 프로퍼티의 값을 활용한다.  
`user.sayHi()`의 내부 코드에서 객체 `user`에 저장된 이름(name)을 이용해 인사말을 만드는 경우가 이런 경우에 속한다.  
메서드 내부에서 this 키워드를 사용하면 객체에 접근할 수 있다.  
이때 '점 앞’의 this는 객체(현재객체)를 나타낸다.  
정확히는 메서드를 호출할 때 사용된 객체를 나타낸다.

```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(this.name);
  },
};

user.sayHi();
```

user.sayHi()가 실행되는 동안에 this는 user를 나타낸다.

```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(user.name); // 'this' 대신 'user'를 사용
  },
};

user.sayHi();
```

this를 사용하지 않고 외부 변수를 참조해 객체에 접근하는 것도 가능하다.  
그런데 이렇게 외부 변수를 사용해 객체를 참조하면 예상치 못한 에러가 발생할 수 있다.

```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(user.name); // Error: Cannot read property 'name' of null
  },
};

let admin = user;
user = null; // user를 null로 덮어씀

admin.sayHi(); // sayHi()가 엉뚱한 객체를 참고하면서 에러발생
```

user를 복사해 다른 변수에 할당(admin = user)하고, user는 전혀 다른 값으로 덮어썼다고 가정해보자.  
sayHi()는 원치 않는 값인(null)을 참조할 것이다.  
alert 함수가 user.name 대신 this.name을 인수로 받았다면 에러가 발생하지 않았을 것이다.

## 자유로운 this

자바스크립트에선 모든 함수에 this를 사용할 수 있다.  
동일한 함수라도 다른 객체에서 호출했다면 'this’가 참조하는 값이 달라진다.

```js
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert(this.name);
}

sayHi(); // this == undefined
// undefined
// 객체가 없어도 함수를 호출할 수 있다.

// 별개의 객체에서 동일한 함수를 사용
user.f = sayHi;
admin.f = sayHi;

// 'this'는 '점(.) 앞의' 객체를 참조
// this 값이 달라짐
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin["f"](); // Admin (점과 대괄호는 동일하게 동작함)
```
