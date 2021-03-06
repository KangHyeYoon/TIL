# 데이터 타입 Data type

자바스크립트의 값은 모두 데이터 타입을 가지며, 이는 primitive(원시 값) 또는 obiect(객체)이다. 

# 데이터 타입의 필요성

> **모든 값은 데이터 타입을 가진다.**

1. 값을 저장할 때 확보해야 하는 `메모리 공간의 크기`를 결정
2. 값을 참조할 때 한 번에 읽어 들여야 할 `메모리 공간의 크기`를 결정
3. 메모리에서 읽어 들인 `2진수 데이터를 어떻게 해석할 지` 결정

# primitive vs objexct

> 원시 타입

원시 타입의 특징은 immutable(불변)이다. 숫자 5는 항상 숫자 5이고, 문자열 “alpha”는 항상 문자열 “alpha”이다. 불변성이라는 말은 변수의 값이 바뀔 수 없다는 뜻이 아님에 주의하자. 숫자 5와 숫자 7을 더하면 두 숫자와는 ‘다른, 새로운’ 숫자 12가 나오고, 문자열 “alpha”와 문자열 “omega”를 더하면 두 문자열과는 ‘다른, 새로운’ 문자열 “alphaomega”이 나오는 것이 중요한 것이다.

> 객체

객체는 원시 타입과 달리 여러 형태와 값을 가질 수 있어 비교적 유연한 성질을 지닌다. 커스텀 데이터 타입을 만들 때 객체를 많이 사용한다. 자바스크립트에 내장된 객체 타입 몇 가지를 소개한다.

- Array
- Date
- RegExp
- Map과 WeakMap
- Set과 WeakSet

# 원시 타입 primitive type

## 숫자 타입 number type

배정밀도 64비트 부동소수점 형식만을 따른다. 정수, 실수, 2진수, 8진수, 16진수 리터럴 전부 어떻게 작성하든 저렇게 저장된다.

## 문자열 타입 string type

0개 이상의 16비트 유니코드 문자(UTF-16)의 집합으로 전 세계 대부분의 문자를 표현할 수 있다.

- 작은따옴표 ‘ ‘
- 큰따옴표 “ “
- 백틱 `

> 따옴표나 백틱으로 감싸지 않는다면 식별자로 인식된다.


```jsx
var str = hello;    // ReferenceError : hello is not defined
```

+ C의 경우 : 문자열 타입 제공 X. 문자의 배열로 문자열을 표현
+ Java의 경우 : 문자열을 객체로 표현

> 자바스크립트의 문자열 :  원시 타입이자 불변 값 immutable value


문자열이 생성되면 그 문자열을 변경할 수 없다.

## 템플릿 리터럴 tempelete literal

다양하고 편리한 문자열 처리 기능 제공. 런타임에 일반 문자열로 변환되어 처리됨. 따옴표 대신 백틱(`)을 사용한다.

> 멀티라인 문자열 multi-line literal

- 일반 문자열 : 줄바꿈이 허용되지 않음. 줄바꿈 등의 공백을 표현하려면 \를 통한 이스케이프 시퀀스 escape sequence를 사용해야 함.
- 템플릿 리터럴 : 명시적이고 직관적으로 뉴라인 표현이 가능함.

```jsx
var templete = `Hello
my name is
Kang`;
```

> 표현식 삽입 expression interpolation

- 일반 문자열 : + 연산자를 사용
- 템플릿 리터럴 : ${   } 리터럴로 표현식을 감싸서 표현


## 불리언 타입 boolean type

T o F

## undefined 타입

변수 선언에 의해 확보된 메모리 공간을 처음 할당이 이뤄질 때까지 쓰레기 값 garbage value이 들어있는 상태로 내버려 두지 않고 자바스크립트 엔진이 undefined로 초기화한다. 개발자가 의도적으로 사용하는 것은 권장하지 않으며, 변수에 값이 없음을 명시하고 싶을 때에는 null을 할당한다.

> 선언 declaration VS 정의 definition

C언어의 경우 선언과 정의는 “실제로 메모리 주소를 할당하는가”의 기준으로 이를 엄격하게 구분하지만, 자바스크립트는 변수를 선언하면 암묵적으로 정의가 이뤄지기 때문에 그 구분이 모호하다. (일반적으로 변수에서는 ‘선언’, 함수에서는 ‘정의’ 단어를 쓰는 것 정도의 간단한 차이이다. 의미는 똑같음)

## 심벌 타입 symbol type

변경 불가능한 원시 타입의 값. ES6에서 추가된 7번째 타입이다. 다른 값과 중복되지 않는 유일무이한 값이며, 이름이 충돌할 위험이 없는 객체의 유일한 프로퍼티(객체의 contents) 키를 만드는 데에 사용한다.

> 원시 값은 리터럴을 통해 생성하지만, 예외적으로 심벌은 Symbol() 생성자 함수를 호출하여 생성한다.

이때 생성된 심벌은

- 외부에 노출되지 않는다
- 다른 값과 절대 중복되지 않는 유일무이한 값이다

```jsx
const symbol1 = Symbol();
const symbol2 = Symbol(42);
const symbol3 = Symbol('foo');

console.log(typeof symbol1);
// expected output: "symbol"

console.log(symbol2 === 42);
// expected output: false

console.log(symbol3.toString());
// expected output: "Symbol(foo)"

console.log(Symbol('foo') === Symbol('foo'));
// expected output: false
```

# 객체 타입 object type

자바스크립트를 이루고 있는 거의 모든 것이 객체라고 해도 될 정도로, 자바스크립트는 객체 기반의 언어이다. 객체에 대해서는 이후 더 자세하게 알아보겠다