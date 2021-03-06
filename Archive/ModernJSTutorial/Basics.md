## 'use strict'

자바스크립트는 꽤 오랫동안 호환성 이슈 없이 (기존의 기능을 변경하지 않으며) 발전해왔고, 그래서 옛날 버젼의 스크립트도 아무런 문제없이 실행될 수 있었다. 하지만 이는 과거의 기능에서 오류나 버그도 그대로 유지한다는 뜻이다. ES5가 나오면서 과거의 기능 일부를 수정하게 되었는데, 이때 하위호환성을 유지하기위해 새로운 변경사항 대부분을 반영하지 않는 방식을 기본 형태 (default)로 지정했다. 이를 무시하고 새로운 스펙의 ES를 사용하고 싶을 경우 스크립트 최 상단에 `'use strict'`라는 문자열을 작성하면 된다. 만약 코드에서 **클래스**나 **모듈**을 사용하면 자동으로 `'use strict'`가 적용된다.

## 자료형

- Number - 정수 및 부동소수점 숫자를 포함하는 자료형, Infinity, -Infinity, NaN을 포함한다.
- BigInt - 내부 표현방식으로 인해, 아주 크거나 아주 작은 숫자는 Number로 나타낼 수 없다. 이때 BigInt를 사용하는데 정수 리터럴 뒤에 n을 추가해서 선언할 수 있다.
- String - 문자를 나타냄.
- Boolean - Boolean이다.
- null - null이다. 존재하지 않는, 비어 있는, 알 수 없는 값을 나타냄.
- undefined - undefined이다. 아직 할당되지 않은 상태를 나타냄.
- Object - 객체형을 제외한 자료형은 한가지만 표현할 수 있기 때문에 원시 자료형이라고 부름. 하지만 객체는 컬렉션이나 복잡한 개체를 표현할 수 있음. 함수도 객체형에 속한다.
- Symbol - 객체의 고유한 식별자를 만들 때 사용된다.

`typeof` 연산자를 사용해 피연산자의 자료형을 확인할 수 있는데, 특이한 점은 `typeof null`이 언어상의 오류로 `object`를 반환한다는 것, `typeof function`은 실제로는 object를 반환해야하지만 function을 반환한다는 것.

## 연산자

할당연산자 `=` 는 값을 변수에 할당하고 그 값을 반환한다. `a = (b = c + 1) + 1` 이런식으로 체이닝도 가능함. 

쉼표연산자`,`는 여러 표현식을 코드 한줄에서 평가할 수 있게 해주는데, 마지막 결과만 반환한다.

```js
let a = (1 + 2, 3 + 4); // , 연산자는 = 보다 우선순위가 낮아서 괄호가 없다면 a = 3, 7 에서 a에 할당되고 7은 무시됨

alert( a ); // 7 (3 + 4의 결과)

// 보통 , 연산자가 활용되는 부분은 다음과 같다
for(a=1, b=3, c=a*b ;a<10 ;a++){}
```

null 병합 연산자 `??`는 값이 확정되어있는 변수를 찾아준다. `a ?? b`의 결과를 보자

- `a`가 `null`이나 `undefined`가 아니면 `a`
- `a`가 `null`이나 `undefined`면 `b`

`x = a ?? b`는 사실 다음과 같다.

```js
x = ( a !== null && a != undefined ) ? a : b;
```

기본 값 할당에 사용할 수 있다.

```js
height = height ?? 100;
```

## 반복문 

`break/continue`와 레이블. 반복을 수행하다가 특정 조건에서 반복문을 탈출하거나 다음 이터레이션을 실행하기 위해 사용하는 키워드인 `break`나 `continue`를 중첩된 반복문에서 사용하다보면 까다로운 경우가 생기는데, 바로 특정한 뎁스까지만 탈출하도록 설정하는 행위가 불가능하다는 것이다. 이를 위해 필요한게 바로 레이블이다. 말 그대로 반복문에 레이블을 붙여 `goto` 처럼 특정 위치로 탈출하거나 해당 뎁스에서 다음 이터레이션을 수행할 수 있다.

```js
outer: for (let i = 0; i < 3; i++) {        // outer가 레이블이다.

  for (let j = 0; j < 3; j++) {

    let input = prompt(`(${i},${j})의 값`, '');

    // 사용자가 아무것도 입력하지 않거나 Cancel 버튼을 누르면 두 반복문 모두를 빠져나옵니다.
    if (!input) break outer; // (*)

    // 입력받은 값을 가지고 무언가를 함
  }
}
```

## 함수 

함수의 매개변수로 넘기는 값은 함수 내부에서 복사해서 사용하기 때문에 값을 수정해도 원래 변수 값에는 영향이 없다.

함수의 선언에는 두 방식이 있는데, 함수 리터럴을 작성만 하는 함수 선언문과 이를 변수에 할당하며 선언하는 함수 표현식이 그것이다. 함수 표현식에서 우리는 자바스크립트가 함수를 값으로 다룬다는 것을 알 수 있다.

```js
function sum1(a, b) {   // 함수 선언문
  return a + b;
}
let sum2 = function(a, b) { // 함수 표현식
  return a + b;
};
```

둘을 비교해보자.

- 선언문은 코드 흐름 중간에 독자적 구문 형태로 존재하지만 표현식은 할당문 우측에 위치한다.
- 표현식은 실행 흐름이 해당 함수에 도달했을 때 생성하기 때문에 그 전에 호출할 수 없다. 하지만 선언문은 스크립트가 실행되기전에 준히하는 초기화 단계에서 생성됩니다. 
- 선언문이 코드 블록 내에 위치하면 블록 내 어디서든 접근할 수 있지만 블록 밖에서는 접근할 수 없습니다. 밖의 블록에서 선언한 변수에 함수 표현식을 할당해야합니다. (스코프가 다르다?)