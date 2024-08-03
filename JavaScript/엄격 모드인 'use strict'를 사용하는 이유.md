# 엄격 모드인 'use strict'를 사용하는 이유

## 📌 Strict Mode란 무엇인가?

JavaScript에서 `use strict`는 엄격 모드를 활성화하는 지시어입니다.

JavaScript는 오랫동안 하위 호환성을 유지하며 발전해 왔습니다. 이는 오래된 코드가 깨지지 않고 작동한다는 장점이 있지만, 초기 설계의 실수나 불완전한 결정이 계속 유지되는 단점도 있습니다.

이를 해결하기 위해 ECMAScript 5(ES5)에서는 `엄격 모드(strict mode)`라는 새로운 기능이 도입되었습니다. 엄격 모드는 **JavaScript의 일부 비표준 기능을 비활성화하고, 오류를 더 명확하게 드러내어 코드의 안정성과 성능을 향상**시킵니다.

<br><br>

## 📌 Strict Mode 활성화 방법

엄격 모드를 활성화하려면 코드의 최상단에 `use strict`를 추가하면 됩니다. 이렇게 하면 해당 스크립트 전체가 엄격 모드로 실행됩니다.

```jsx
'use strict'

function myFunction() {
  // 엄격 모드가 활성화된 코드
}
```

특정 함수 내에서만 엄격 모드를 적용하고 싶다면 함수의 최상단에 `use strict`를 추가할 수 있습니다.

```jsx
function myFunction() {
  'use strict'
  // 이 함수 내에서만 엄격 모드가 활성화됩니다.
}
```

<br><br>

## ❓ Strict Mode의 장점

1. **오류 발견 용이:**
   - 선언되지 않은 변수를 사용하려 할 때 오류를 발생시켜 실수를 예방합니다.
   - 중복된 매개변수 이름을 허용하지 않습니다.
2. **보안 강화:** 전역 객체에 대한 접근을 방지합니다. 예를 들어, 함수 내에서 **this**를 사용할 때 전역 객체를 가리키지 않도록 합니다.
3. **성능 향상:** 일부 JavaScript 엔진에서 엄격 모드 코드는 최적화가 더 잘 이루어져 성능이 향상될 수 있습니다.

<br><br>

## 📌 Strict Mode 적용 예시

격 모드를 적용하면 선언되지 않은 변수에 값을 할당할 때 오류가 발생합니다.

### **JavaScript**

```jsx
// 비엄격 모드
nickname = 'heun'
console.log(nickname) // heun

// 엄격 모드
"use strict";
nickname = "heun"; // Uncaught ReferenceError: nickname is not defined
console.log(nickname);
```

이처럼 엄격 모드에서는 변수를 선언하기 전에 사용하면 오류가 발생합니다.

<br><br>

## ❓ 'use strict'를 꼭 사용해야 하나요?

꼭 사용할 필요는 없습니다! 그렇지만 모던 `JavaScript`는 '클래스’와 '모듈’이라는 진일보한 구조를 제공합니다. 이 둘을 사용하면 **자동으로 엄격 모드가 적용**됩니다. 따라서 이 둘을 사용하고 있다면 스크립트에 `use strict`를 붙일 필요가 없습니다.
즉, 코드를 클래스와 모듈을 사용해 구성한다면 `use strict`를 생략해도 됩니다. 하지만 아직 클래스와 모듈을 배우지 않았다면, 코드의 안전성과 품질을 높이기 위해 스크립트 상단에 `use strict`를 추가하는 것이 좋습니다!

<br><br>

## 📌 결론

엄격 모드는 **JavaScript 코드의 품질과 성능을 향상시키는 데 매우 유용**합니다. 클래스와 모듈을 사용하는 경우에는 자동으로 엄격 모드가 적용되므로 별도로 추가할 필요가 없습니다. 기존 코드와 혼합하여 사용할 때는 주의가 필요하며, 호환성 문제를 고려해야 합니다.

엄격 모드를 사용함으로써 **코딩 실수를 줄이고, 더 안전하고 효율적인 코드를 작성**할 수 있습니다. 모던 JavaScript 개발 환경에서는 엄격 모드를 사용하는 것이 표준적인 관행이므로, 이를 잘 이해하고 활용하는 것이 중요합니다.

<br><br>

### 블로그

- [[Javascript] 엄격 모드인 'use strict'를 사용하는 이유](https://velog.io/@jiheunkim/Javascript-%EC%97%84%EA%B2%A9-%EB%AA%A8%EB%93%9C%EC%9D%B8-use-strict%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0)
