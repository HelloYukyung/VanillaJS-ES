# [VanilaJS] addEventListener

이벤트 리스너는 DOM 객체에서 이벤트가 발생할 경우 해당 이벤트 처리 핸들러를 추가할 수 있는 오브젝트이다.

이벤트 리스너를 이용하면 특정 DOM에 위에 말한 Javascirpt 이벤트가 발생할 때 특정 함수를 호출한다.

```js
DOM객체. addEventListener(이벤트명, 실행할 함수명, 옵션)
```

```js
object.addEventListener("click", function () {
  console.log("clicked");
});
```

내가 아는 onClick 이벤트

## onclick과 addEventListener차이점?

addEventListener의 경우, 여러 개의 이벤트를 overwrite 할 수 있다.

```js
let obj = document.getElementById("trigger");
let do1 = () => {
  alert("do1");
};
let do2 = () => {
  alert("do2");
};
obj.onclick = do1;
obj.onclick = do2;
```

위 예제에서는 do2를 작성하면서 do1은 작동하지 않게 된다.

```js
obj.addEventListener("click", do1, false);
obj.addEventListener("click", do2, false);
```

addEventListener를 쓸 경우 do1과 do2 모두가 작성 순서대로 작동하게 된다. 한 클릭이 일어났을 때 여러가지 일이 동작하게 하고 싶다면, 하지만 함수는 분리되어 있다면 addEventListener로 작성하는 것이 필요할 것이다.

## javascript30 Day2에서

```js
function removeTransition(e) {
  if (e.propertyName !== "transform") return;
  e.target.classList.remove("playing");
}

function playSound(e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  const key = document.querySelector(`div[data-key="${e.keyCode}"]`);
  if (!audio) return;

  key.classList.add("playing");
  audio.currentTime = 0;
  audio.play();
}
const keys = Array.from(document.querySelectorAll(".key"));
keys.forEach((key) => key.addEventListener("transitionend", removeTransition));
// ...
window.addEventListener("keydown", playSound);
```

transitionend: transition이 완료된 이에 발생하는 이벤트  
keydown: keydown 이벤트 키가 눌렸을 때 발생하는 이벤트

event리스너를 통해 해당 이벤트가 발생할 때 함수를 실행시켜주었다.
