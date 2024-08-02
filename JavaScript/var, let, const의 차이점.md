# var, let, const의 차이점

## 📌 var, let, const란 무엇인가?
JavaScript에서 **변수를 선언하는 방법**에는 `var`, `let`, `const` 세 가지가 있습니다. 이들은 각기 다른 특성과 사용 방법을 가지고 있으며, 이를 이해하는 것은 코드 작성 시 매우 중요합니다.

<br><br>

## 📌 var, let, const의 차이점
### 요약
> `var`은 중복 선언, 재할당 모두 가능!
`let`은 중복 선언 X, 재할당 가능!
`const`는 중복 선언, 재할당 모두 X!

### var
`var`는 ES6 이전에 변수를 선언하는 유일한 방법이었습니다. `var`로 선언된 변수는 **함수 스코프를 가지며, 호이스팅(hoisting)이 적용**됩니다.

```jsx
function varExample() {
  console.log(x); // undefined (호이스팅)
  var x = 10;
  console.log(x); // 10
}

example();
```
`var`는 **블록 스코프를 무시하고 함수 스코프를 따릅니다.** 이는 의도하지 않은 변수 재선언과 값 변경의 원인이 될 수 있습니다.

```jsx
if (true) {
  var y = 20;
}
console.log(y); // 20 (블록 스코프 무시)
```

### let
`let`은 ES6에서 도입된 새로운 변수 선언 방식으로, **블록 스코프를 따릅니다.** 호이스팅이 되지만 초기화되지 않은 상태로 남아 있어서 참조 오류가 발생할 수 있습니다.
```jsx
function letExample() {
  // console.log(a); // ReferenceError (초기화되지 않은 상태)
  let a = 10;
  console.log(a); // 10
}

example();
```

`let`은 동일한 스코프 내에서 **재선언이 불가능**하며, **변수를 블록 스코프 내에서만 접근할 수 있게** 합니다.

```jsx
if (true) {
  let b = 30;
  console.log(b); // 30
}
// console.log(b); // ReferenceError (블록 스코프)
```

### const
`const`는 **상수를 선언할 때 사용**되며, **선언과 동시에 초기화**해야 합니다. `const`로 선언된 변수는 **재할당이 불가능**하지만, **객체나 배열의 경우 내부 값은 변경이 가능**합니다.

```jsx
const c = 40;
// c = 50; // TypeError (재할당 불가)

const obj = { name: "Alice" };
obj.name = "Heun"; // 객체의 프로퍼티는 변경 가능
console.log(obj.name); // Heun

const arr = [1, 2, 3];
arr.push(4); // 배열 요소 추가 가능
console.log(arr); // [1, 2, 3, 4]
```
`const` 또한 **블록 스코프를 따르며, 재선언이 불가능**합니다.

```jsx
if (true) {
  const d = 50;
  console.log(d); // 50
}
// console.log(d); // ReferenceError (블록 스코프)
```

<br><br>

## ❓ var, let, const의 사용
### var
> ES6 이전의 코드나, 특정 함수 스코프가 필요한 상황에서 사용하지만, 최신 코드에서는 권장되지 않습니다.

### let
> 재할당이 필요한 변수나 블록 스코프가 필요한 상황에서 사용합니다.

### const
> 재할당이 필요 없는 상수나 객체, 배열을 선언할 때 사용합니다. 대부분의 경우 `const`를 기본으로 사용하고, 필요할 때만 `let`을 사용하는 것이 좋습니다.

<br><br>

## 📌 var, let, const의 장점과 단점
### 장점
>
- 다양한 스코프를 제공하여 개발자가 유연하게 변수 관리를 할 수 있습니다.
- `const`와 `let`은 블록 스코프를 제공하여 코드의 안정성을 높이며, `const`는 재할당을 방지하여 예측 가능한 코드를 작성할 수 있습니다.

### 단점
>
`var`는 블록 스코프를 무시하여 의도치 않은 변수 재선언과 값 변경의 위험이 있으며, `const`는 객체나 배열의 내부 값을 변경할 수 있어 완전한 불변성을 제공하지 않습니다. 또한, `let`과 `const`는 선언 전에 접근 시 참조 오류가 발생할 수 있습니다.

<br><br>

## 📌 결론
`var`, `let`, `const`는 각기 다른 특성과 사용 방법을 가지고 있어 상황에 맞게 사용하는 것이 중요합니다! 최신 JavaScript 코드에서는 대부분 `let`과 `const`를 사용하여 코드의 가독성과 안정성을 높이는 것을 권장합니다🤗

`var`는 함수 스코프를 가지며, 의도치 않은 재선언과 값 변경의 위험이 있으므로 가능하면 사용을 피하는 것이 좋습니다. `let`은 **재할당이 필요한 변수에 사용**하고, `const`는 **재할당이 필요 없는 상수나 객체, 배열에 사용**하여 안전하고 효율적인 코드를 작성할 수 있습니다!

<br><br>

### 블로그

- [[Javascript] var, let, const의 차이점](https://velog.io/@jiheunkim/Javascript-var-let-const-%EC%B0%A8%EC%9D%B4%EC%A0%90)