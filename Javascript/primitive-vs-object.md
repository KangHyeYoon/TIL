자바스크립트가 제공하는 7가지 데이터 타입(숫자, 문자열, 불리언, null, undefined, 심벌, 객체)은 크게 원시 타입과 객체 타입으로 구분할 수 있다. 이들은 크게 세 측면에서 다르다.

> 변경 가능 여부
> 
- 원시 타입: 변경 불가능한 값 immutable type
- 객체 타입: 변경 가능한 값 mutable type

> 변수(확보된 메모리 공간)에 할당했을 시
> 
- 원시 타입: 실제 값 저장
- 객체 타입 : 참조 값 저장

> 값 전달 방법
> 
- 원시 타입: 값에 의한 전달(원본의 원시 값 복사) pass by value
- 객체 타입: 참조에 의한 전달(원본의 참조-메모리 주소-값 복사) pass by reference

# 원시 값 primitive

한 번 생성된 원시 값은 읽기 전용 read only로써, 변경할 수 없다. 변수에 재할당이 불가능하다는 소리가 아니라 값 자체에 대한 진술인 것이다.

![primitive](https://user-images.githubusercontent.com/97890886/162573698-0cf741e4-a4d0-46c8-ab0c-423987e75490.png)

변수를 선언하고, 할당하고, 재할당하는 과정에서 변수가 참조하는 메모리 공간의 주소가 변경된 이유는 변수에 할당된 원시 값이 `변경 불가능`한 값이기 때문이다. 만약 변수가 변경 가능했다면, 같은 메모리 주소 내에서 원시 값 자체를 바꾸면 그만일 것이다.

즉, 불변성을 갖는 원시 값을 할당한 변수는 재할당 이외에 변수 값을 변경할 수 있는 방법이 없다.

## 원시 값으로써의 문자열의 의미

자바스크립트에서의 문자열은 다른 원시 값과 비교할 때 독특한 점이 있다. 숫자 등은 IEEE-764 부동소수점에 따라 항상 8바이트 double형으로 저장되지만, 문자는 하나당 2바이트로, 문자열이 몇 개의 문자로 이루어져 있느냐에 따라 데이터의 크기(그러니까 참조할 메모리의 크기)가 다르다. 그래서 C언어나 JAVA 등 자료형으로 데이터 타입을 먼저 선언하는 경우 문자열을 정적인 데이터 타입으로 정하기 힘든 것이다. 이런 의미에서  자바스크립트의 문자열은 강력하고 편한 기능이다.

# pass by value

![pass-by-value](https://user-images.githubusercontent.com/97890886/162573712-ac21d584-6432-41d7-9329-2f293d3c940c.png)

> 값에 의한 전달
> 

변수 score에 80을 할당하고, 변수 copy에는 score의 값을 할당한 모습이다. 원시 값은 pass by value로 동작하므로 값 자체가 그대로 복사되는 원리이다.

```jsx
var score = 80;
var copy = score;

console.log(score);     // 80
console.log(copy);      // 80

score = 100;

console.log(score);     // 100
console.log(copy);      // 80
```

지금까지 계속해서 메모리 구조와 함께 알아봤기 때문에 알겠지만, 원시값은 불변이므로 메모리 자체가 바뀌는 것이 아닌, 새로운 메모리에 값이 재할당되는 것 뿐이다. 즉 score과 copy는 같은 값인 80을 가지고 있으나, copy는 새로운 메모리에 score의 값인 80이 복사된 변수일 뿐이므로 score의 80과 copy의 80은 엄연히 다르다. score의 값이 100으로 바뀌었다면, 저 그림에서 더 밑으로 내려가서 새로운 메모리 공간이 생성되고 그곳에 값 100이 할당되고, 이를 식별자 score이 가리키면서 링크됐을 것이다. copy 식별자와 링크된 80이라는 값과는 전혀 상관없는 일이다.

그러므로 score의 값을 변경해도 완전히 다른 copy의 값은 변하지 않는다.

> 참고
> 

`값에 의한 전달`이라는 표현은 사실 상당히 모호하다. ECMAScript 사양에는 변수를 통해 메모리를 어떻게 관리할지 명확히 정의되어 있지 않을 뿐더러, 같은 표현이지만 다르게 동작하는 경우도 있다, (파이썬도 위와 비슷하게 동작하지만, 파이썬의 경우 2행에서부터 두 변수가 같은 값을 가리키다가 둘 중 한 쪽이 재할당 된 순간 분리되는 원리이다.) 또한 사실 엄격하게 표현하면 **변수에는 값이 전달되는 것이 아닌 메모리 주소가 전달되기 때문**에 이 표현은 바람직한 표현이 아니다. 

그러나 여기서 가장 중요한 점은 바로 이것이다.

<aside>
❕ 결국 두 변수의 원시 값은 서로 다른 메모리 공간에 저장된 별개의 값이기 때문에, 어느 한 쪽에서 재할당을 통해 값을 변경하더라도 서로 간섭할 수 없다.

</aside>

# 객체 object

primitive는 불변값이고 한 번 선언하면 값의 내용을 변경하지 못했다. 객체는 프로퍼티와 달리 값 자체가 유동적이다.  동적으로 추가되고 삭제할 수 있으며 프로퍼티 값에도 제약이 없다(그러니까 내부 내용이 얼마나, 무엇이 있든 괜찮다). 따라서 객체는 원시값처럼 먼저 확보해야 할 `메모리 공간의 크기를 사전에 정해둘 수 없다`.  자바스크립트 엔진은 이렇게 무시무시한 객체를 어떻게 관리할까?

> 자바스트립트 객체의 관리 방식
> 
- 해시 태이블 hash table

프로퍼티 키key를 인덱스로 사용하여 접근하는 방식이다. 물론 이보다 훨씬 복잡하고 나은 방법으로 객체를 구현하지만, 기본적으로 이 원리를 따른다는 것이다. C++나 자바 같은 클래스 기반 객체지향 프로그래밍 언어는 일단 1. 클래스를 정의한다 2. 이후 이미 정의된 클래스를 기반으로 객체(인스턴스)를 만든다. 그래서 이들은 객체가 생성된 이후 프로퍼티를 추가하거나 삭제하는 것이 불가능하다. 그러나 자바스크립트는 가능하다. 허용하는 것이 많다는 것은, 그만큼 성능이 후달리게 되거나 보안이 취약해짐을 의미하기도 한다(...) 그래서 요즘은...

- 히든 클래스 hidden class

요 방식을 사용하여 C++와 근접한 정도의 성능을 보장한다고 한다.

## 변경 가능한 값으로써의 객체

객체는 C언어의 포인터와 아주 유사하게 동작한다. 원시 값은 score라는 변수와 80이라는 값(이 들어있는 메모리)이 직접적으로 link됐지만, 객체는 person이라는 변수와 name: ‘Kang’이라는 값(이 들어있는 메모리)의 주소(가 들어있는 메모리)가 link된다. 즉, 중간에 유통업체가 하나 더 끼어있다.

![object-](https://user-images.githubusercontent.com/97890886/162573736-22427e9a-8a40-4897-9fa6-b2d39c00f553.png)


원시 값과는 다르게 재할당 없이도 객체를 직접 변경(프로퍼티를 동적으로 추가하거나 삭제, 갱신, 프로퍼티 자체를 삭제 등 모든 작업)할 수 있다. 재할당을 하지 않았으므로 메모리에 저장된 객체를 직접 수정할 수 있고, 변수의 참조 값(으로 갖고 있는 ‘진짜 값’의 메모리의 주소)은 변경되지 않는다.

객체가 요렇게 된 이유는... 아까 말했듯이 객체 자체가 겁나 유연한 구조이기 때문에 객체를 관리하는 것은 상당히 힘들고, 재할당을 할 때마다 새로운 메모리 공간을 만들고 해지하는 것은 매우 복잡하며 엄청난 비용을 요구한다. 그래서 이렇게 관리까지 유연하게 해 버리네...

이 방식은 당연하겠지만 부작용을 유발하는데, 바로 여러개의 식별자가 하나의 객체를 공유할 수 있게 된다는 점이다. 이는 심각한 부작용을 유발하기도 하며, 객체의 값(의 메모리 주소) 전달 방식인 pass by reference를 공부하면서 알아보겠다.

> 얕은 복사 vs 깊은 복사
> 

```jsx
// shallow copy 얕은 복사
// 복사본과 원본은 다른 객체지만 참조 값을 복사하는 원리를 사용한다.
const obj = {
    x : { y : 1},
};

const c1 = {... obj};

// 한 단계(바로 밑의 프로퍼티인 x)까지만 참조 값을 복사한다
console.log(obj.x === c1.x);    // true

// 중첩되어 있는 또 다른 객체까지는 복사하지 않는다
// === x 객체 내부의 프로퍼티 값이 서로 다르므로
// 객체 자체가 완전히 일치하지는 않는다.
console.log(obj === c1);    // false

// deep copy 깊은 복사
const _ = require('lodash');
const c2 = _.cloneDeep(obj);

// 원시 타입 처럼 객체에 중첩되어 있는 모든 객체를 모두 복사하여
// 완전히 새로운 복사본을 만든다
console.log(obj.x === c1.x);    // false
console.log(obj === c1);    // false
```

기존에 봤던 pass by value를 깊은 복사, pass by reference를 얕은 복사라고 부르기도 한다.

# pass by reference

객체를 가리키는 변수를 다른 변수에 할당할 때, 원본의 `참조 값이 복사`되어 전달하는 방법이다.

```jsx
var person = {
    name: 'K';
};

var copy = person;
```

![pass-by-reference](https://user-images.githubusercontent.com/97890886/162573751-e09255df-4698-4aad-80fd-78436d101f73.png)

이제 아까 봤던 객체 구성의 치명적인 단점인 `여러 개의 식별자가 하나의 객체를 공유`한다는 말이 무엇을 의미하는지 알 수 있다.

- score에는 객체 값이 직접적으로 들어있지 않고, 객체 값의 메모리 주소(==참조 값)가 담겨 있다.
- + score에 copy를 할당하면 score의 참조 값이 copy로 복사되고, 서로 다른 두 식별자는 결국 같은 객체를 가리키게 된다.

> 이는 곧 어느 한 쪽이 객체를 변경하면 객체를 공유하는 다른 변수들도 영향을 받음을 의미한다.
> 

# p.b.v 와 p.b.r

- 동일한 점

> 식별자가 기억하는 메모리 공간에 저장되어 있는 값을 복사하여 전달한다
> 
- 다른 점

> 변수에 저장되어 있는 값(식별자가 기억하는 메모리 공간)이 원시 값이냐, 참조 값이냐의 차이
> 

결국 엄격히 말하자면, 자바스크립트에는 값에 의한 전달만이 존재한다고 할 수 있다. 원시값과 객체의 전달 방식의 차이(그러니까 원본과 사본이 서로 영향을 주고받는지에 대하여)를 설명하느라 이런것 뿐이다. 자바스크립트에는 포인터가 존재하지 않으므로, 포인터와 비슷해 보여도 동작 원리가 완벽히 일치하지 않음에 주의하자.

# 마지막 퀴즈

```jsx
var person1 = {
    name: 'kang',
};
var person2 = {
    name: 'kang',
};

// 두 변수가 가리키는 객체는 내용은 같지만, 다른 메모리에 저장된 별개의 객체다.
console.log(person1 === person2);   // false

// 프로퍼티 값을 참조하는 연산자는 값으로 평가될 수 있는 표현식이다.
// 두 표현식은 전부 값 'kang'으로 평가되어 같다.
console.log(person1.name === person2.name);   // true
```