# Attribute와 Property의 차이점

## 📌 Attribute

`Attribute`는 **HTML의 요소의 속성**으로, 요소의 동작이나 스타일을 정의하고 초기값을 지정하는 데 사용됩니다. 이는 HTML 문서 내에서 정의되며, DOM을 통해 접근할 수 있습니다.

```html
<!-- div 엘리먼트의 id와 class 속성은 Attribute이다 -->
<div id="example" class="bold"></div>

<!-- input 엘리먼트의 type과 value 속성은 Attribute이다 -->
<input type="email" value="hi@example.com" />
```

<br>

### HTML

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Attribute vs Property</title>
  </head>
  <body>
    <input id="myInput" type="text" value="Hello" />
    <script src="script.js"></script>
  </body>
</html>
```

### JavaScript (script.js)

```jsx
document.addEventListener('DOMContentLoaded', function () {
  const myInput = document.getElementById('myInput')

  // HTML Attribute 접근
  console.log(myInput.getAttribute('value')) // Hello

  // HTML Attribute 변경
  myInput.setAttribute('value', 'World')
  console.log(myInput.getAttribute('value')) // World
})
```

위 예시에서, `value`는 `input` 요소의 Attribute입니다.

```html
<input id="myInput" type="text" value="Hello" />
```

JavaScript를 통해 `getAttribute`와 `setAttribute`를 사용하여 이 값을 읽고 변경할 수 있습니다.

<br><br>

## 📌 Property

`Property`는 **DOM의 속성**으로, JavaScript 객체의 프로퍼티로 동작합니다. 이는 주로 사용자와의 상호작용을 처리하는 데 사용됩니다. 쉽게 말하자면, Html의 `Attribute`를 DOM 내에서 표현하는 것이 `Property`라고 볼 수 있습니다.

<br>

## 🤔 DOM이란?

**DOM**(**Document Object Model**)은 **HTML, XHTML, XML 문서의 프로그래밍 인터페이스**입니다. DOM은 문서의 구조화된 표현을 제공하며, 프로그래밍 언어를 통해 문서의 내용과 구조를 변경할 수 있게 합니다. `DOM`은 웹 페이지가 로드될 때 브라우저에 의해 생성됩니다.

### DOM의 역할

- **동적 콘텐츠 생성 및 업데이트**: DOM을 통해 JavaScript는 웹 페이지의 콘텐츠를 동적으로 생성하고 업데이트할 수 있습니다.
- **사용자 상호작용 처리**: 이벤트 리스너를 사용하여 사용자 입력(클릭, 키보드 입력 등)을 처리하고 이에 반응할 수 있습니다.
- **데이터 바인딩**: DOM은 웹 애플리케이션이 데이터와 UI를 동기화하는 데 중요한 역할을 합니다.

<br>

### HTML

위와 동일합니다.

```html
<input id="myInput" type="text" value="Hello" />
```

### JavaScript (script.js)

```jsx
document.addEventListener('DOMContentLoaded', function () {
  const myInput = document.getElementById('myInput')

  // DOM Property 접근
  console.log(myInput.value) // Hello

  // DOM Property 변경
  myInput.value = 'World'
  console.log(myInput.value) // World

  // HTML attribute와 DOM property의 차이
  console.log(myInput.getAttribute('value')) // Hello (초기값 유지)
})
```

이 예시에서 `value`는 DOM Property로 사용됩니다. DOM Property는 JavaScript 객체의 속성으로 동작하며, `input` 요소의 현재 상태를 반영합니다. 예를 들어, **사용자가 입력 필드에 직접 값을 입력하면 DOM Property는 변경되지만, Attribute는 변경되지 않습니다.**

<br><br>

## 📌 Attribute VS Property

위의 설명과 예시를 토대로, **`Attribute`는 정적이고 `Property`는 동적이라는 것**을 확인할 수 있다. `Property`의 값을 변경해도 DOM 객체만 업데이트 되고 Html은 업데이트 되지 않아 `Attribute` 값은 그대로입니다.

- **HTML Attribute**: 기계의 초기 설정 값처럼, 처음에 설정된 값을 나타냅니다. 예를 들어, **세탁기의 초기 설정 온도는 30도**일 수 있습니다.
- **DOM Property**: 기계가 실제로 작동하면서 변경되는 현재 상태를 나타냅니다. 세탁기가 작동 중일 때 **사용자가 온도를 40도로 변경하면, 현재 온도는 40도**입니다. 그러나 **초기 설정 온도는 여전히 30도**로 남아 있습니다.

<br>

### 차이점 요약

1. **초기값 vs 현재 상태**:
   - `Attribute`는 **HTML 문서에 정의된 요소의 초기값**을 나타냅니다.
   - `Property`는 **요소의 현재 상태**를 나타내며, **사용자 입력이나 스크립트에 의해 동적으로 변경**될 수 있습니다.
2. **접근 방식**:
   - Attribute는 `getAttribute`와 `setAttribute` 메서드를 사용하여 접근하고 변경할 수 있습니다.
   - Property는 JavaScript 객체의 속성처럼 직접 접근하고 변경할 수 있습니다.
3. **동기화**:
   - HTML Attribute와 DOM Property는 **초기에는 동일한 값**을 가질 수 있지만, 이후에는 독립적으로 동작할 수 있습니다.
     - 사용자가 입력 필드의 값을 변경하면 DOM Property는 업데이트되지만, 초기 Attribute 값은 변하지 않습니다.
4. **사용 목적**:
   - `Attribute`는 주로 **요소의 초기 설정을 정의**하는 데 사용됩니다.
   - `Property`는 **요소의 현재 상태를 관리하고 사용자와의 상호작용을 처리**하는 데 사용됩니다.
5. **성능 차이**:
   - 일반적으로 **Property 접근**이 `getAttribute()`와 `setAttribute()` 메서드보다 약간 더 빠릅니다.

<br><br>

### 블로그

- [[HTML] Attribute와 Property의 차이점](https://velog.io/@jiheunkim/HTML-Attribute%EC%99%80-Property%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)
