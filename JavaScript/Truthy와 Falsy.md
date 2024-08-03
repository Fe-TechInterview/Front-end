# Truthy와 Falsy

## 📌 Truthy와 Falsy란 무엇인가?

JavaScript에서 `Truthy`와 `Falsy`는 조건문에서 `true` 또는 `false`로 평가되는 값을 설명하는 개념입니다. 조건문에서 Boolean으로 변환될 때 `true`로 평가되는 값을 `Truthy`, `false`로 평가되는 값을 `Falsy`라고 합니다. 이 개념을 이해하면 조건문을 보다 직관적으로 작성할 수 있습니다!

<br><br>

## 📌 Truthy와 Falsy 값

### Falsy 값

Falsy 값은 조건문에서 **`false`로 평가되는 값**입니다. JavaScript에서 Falsy 값은 다음과 같습니다:

- `false`
- `0` (숫자 0)
- `0` (음수 0)
- `0n` (BigInt 형식의 0)
- `""` (빈 문자열)
- `null`
- `undefined`
- `NaN` (Not-a-Number)

이 값들은 조건문에서 모두 `false`로 평가됩니다.

```jsx
if (!false) console.log('Falsy') // Falsy
if (!0) console.log('Falsy') // Falsy
if (!'') console.log('Falsy') // Falsy
if (!null) console.log('Falsy') // Falsy
if (!undefined) console.log('Falsy') // Falsy
if (!NaN) console.log('Falsy') // Falsy
```

<br>

### Truthy 값

**Falsy 값이 아닌 모든 값은 Truthy 값**입니다. 일반적으로 Truthy 값은 조건문에서 `true`로 평가됩니다.

```jsx
if (true) console.log('Truthy') // Truthy
if (1) console.log('Truthy') // Truthy
if ('non-empty string') console.log('Truthy') // Truthy
if ({}) console.log('Truthy') // Truthy
if ([]) console.log('Truthy') // Truthy
if (function () {}) console.log('Truthy') // Truthy
```

**빈 객체 `{}`와 빈 배열 `[]`도 Truthy 값**입니다.

<br><br>

## 📌 Truthy와 Falsy의 활용

### 조건문에서의 활용

Truthy와 Falsy 값은 조건문에서 자주 사용됩니다. 예를 들어, **변수에 값이 있는지 확인할 때 유용**합니다.

```jsx
let username = 'Heun'

if (username) {
  console.log(`Hello, ${username}!`) // Hello, Heun!
} else {
  console.log('Hello, Everyone!')
}
```

여기서 `username`이 Truthy 값이므로 조건문이 참으로 평가되어 `Hello, Heun!`이 출력됩니다.

<br>

### 논리 연산자 활용

**논리 연산자 `&&`와 `||`를 사용하여 조건부 값을 설정**할 때도 Truthy와 Falsy 개념이 유용합니다.

```jsx
let defaultName = 'Guest'
let name = username || defaultName
console.log(name) // Heun
```

여기서 `username`이 Truthy 값이므로 `name`은 `username`의 값을 갖습니다. 만약 `username`이 Falsy 값이었다면 `name`은 `defaultName`의 값을 갖게 됩니다.

```jsx
let isLoggedIn = true
isLoggedIn && console.log('User is logged in') // User is logged in
```

여기서 `isLoggedIn`이 Truthy 값이므로 `&&` 연산자의 오른쪽 표현식이 실행됩니다.

<br><br>

## 📌 Truthy와 Falsy의 장점

1. **코드 간결화:** 불필요한 비교 연산 없이 값의 존재 여부를 간단하게 확인할 수 있습니다.
2. **가독성 향상:** 조건문을 보다 직관적으로 작성할 수 있어 코드의 가독성이 높아집니다.
3. **유연한 조건 처리:** 다양한 데이터 타입을 조건문에서 유연하게 처리할 수 있습니다.

<br><br>

## 📌 결론

Truthy와 Falsy는 **JavaScript의 조건문을 간결하고 명확하게 작성할 수 있는 강력한 개념**입니다. 이를 잘 이해하고 활용하면, 코드의 가독성과 유지 보수성이 크게 향상됩니다. JavaScript 개발에서는 이러한 개념을 잘 이해하고, 적절히 활용하는 것이 중요합니다.

모든 JavaScript 값이 **Truthy나 Falsy로 평가될 수 있다는 점**을 명심하고, 이를 바탕으로 조건문을 보다 효율적으로 작성해 보세요.

<br><br>

### 블로그

- [[Javascript] Truthy와 Falsy](https://velog.io/@jiheunkim/Javascript-Truthy%EC%99%80-Falsy)
