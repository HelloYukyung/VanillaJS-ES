# [VanilaJS] 버블링&캡처링

## 버블링

한 요소에 이벤트가 발생하면 이 요소에 할당된 핸들러가 동작하고, 이어서 부모의 핸들러가 동작하게 된다.  
가장 최상단의 조상요소를 만날 때까지 위 과정이 반복되면서 요소 각각에 할당된 핸들러가 동작한다.

```js
<form onclick="alert('form')">
  FORM
  <div onclick="alert('div')">
    DIV
    <p onclick="alert('p')">P</p>
  </div>
</form>
```

가장 안쪽의 P를 클릭하면 순서대로 "p">"div">"form"의 알람이 뜬다.

- 동작원리

1. `<p>`에 할당된 onclick 핸들러가 동작
2. 바깥의 `<div>`에 할당된 핸들러가 동작
3. 그 바깥의 `<form>`에 할당된 핸들러가 동작

document 객체를 만날 때까지, 각 요소에 할당된 onclick 핸들러가 동작한다.

이러한 흐름을 '이벤트 버블링이라고 부른다.

## event.target

부모 요소의 핸들러는 이벤트가 정확이 어디서 발생했는지에 대한 정보를 얻을 수 있다.  
event가 발생한 가장 안쪽의 요소는 타깃(target)요소라 불리며 evnet.target을 사용해 접근할 수 있다.

### event.target과 this 의 차이점

event.target은 실제 이벤트가 시작된 ‘타깃’ 요소이다.
버블링이 진행되어도 변하지 않는다.
this는 ‘현재’ 요소로, 현재 실행 중인 핸들러가 할당된 요소를 참조한다.

```js
form.onclick = function (event) {
  event.target.style.backgroundColor = "yellow";

  // chrome needs some time to paint yellow
  setTimeout(() => {
    alert("target = " + event.target.tagName + ", this=" + this.tagName);
    event.target.style.backgroundColor = "";
  }, 0);
};
```

위 코드를 참조했을 때
P 클릭시 : target = P this =FORM
DIV 클릭시 : target = DIV this =FORM
FORM 클릭시 : target = FORM this =FORM
