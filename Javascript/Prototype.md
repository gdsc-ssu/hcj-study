# Prototype (프로토타입)

**자바스크립트는 프로토타입 기반 언어**이다. 클래스 기반 언어에서는 '상속'을 사용하지만, 프로토타입 기반 언어에서는 어떤 객체를 원형(prototype)으로 삼고, 이를 복제함으로써 상속과 비슷한 효과를 얻는다.



## 1. Prototype 개념 이해

어떤 생성자 함수(Constructor)를 new 연산자와 함께 호출하면 생성자 함수(Constructor)에서 정의된 내용을 바탕으로 새로운 instance가 생성된다. 이때 **instance에는 `__proto__` 라는 프로퍼티가 자동으로 부여**되는데, **이 프로퍼티는 생성자 함수(Constructor)의 `prototype`이라는 프로퍼티를 참조**한다.

- `prototype` 과 `__proto__` 은 객체
- `prototype` 객체 내부에는 인스턴스가 사용할 메소드를 저장
- 인스턴스에서도 `__proto__` 를 통해 이 메소드들에 접근 (`__proto__` 는 **생략 가능**)



### constructor 프로퍼티

생성자 함수의 프로퍼티인 `prototype` 객체 내부에는 `constructor` 라는 프로퍼티가 있고, **생성자 함수(자기 자신)을 참조**한다. (`__proto__` 도 동일)

→ **인스턴스로부터 그 원형이 무엇인지를 알 수 있는 수단**



## 2.  Prototype Chain (프로토타입 체인)

### Method Override (메소드 오버라이드)

인스턴스가 동일한 이름의 프로퍼티 또는 메소드를 가지고 있으면 기존의 것을 새로운 것으로 덮어 씌운다. (class와 동일!)



### Prototype Chain (프로토타입 체인)

어떤 데이터의 `__proto__` 프로퍼티 내부에 다시 `__proto__` 프로퍼티가 연쇄적으로 이어진 것을 **프로토타입 체인**이라고 하고, 이 체인을 따라가며 검색하는 것을 **프로토타입 체이닝**이라고 한다.

ex) `arr`변수는 배열이므로 `arr.__proto__`는 `Array.prototype`를 참조하고, `Array.prototype` 또한 객체를 상속받아 동작하므로  `Array.prototype.__proto__`는 `Object.prototype` 를 참조한다.



프로토타입과 프로토타입 체인은 아래 이미지와 같은 구조로 이루어져 있다.

<img src="https://user-images.githubusercontent.com/70627979/163802782-04e300bf-f616-4339-8d21-cf5fd718d481.png" alt="image" style="zoom: 40%;" />



### 객체 전용 메소드의 예외사항

**`prototype`은 객체**이기 때문에, **`Object.prototype`이 언제나 프로토타입 체인의 최상단에 위치**한다. 따라서 객체에서만 사용할 메소드는 다른 데이터 타입처럼 프로토타입 객체 안에 정의할 수 없다.

- 객체만을 대상으로 동작하는 객체 전용 메소드들은 Object에 `static method`로 부여할 수 밖에 없다.

- 생성자 함수인 Object와 인스턴스 객체 리터럴 사이에는 **this를 통한 연결이 불가능**

  → '메소드명 앞의 대상이 곧 this' 대신에 this 사용을 포기하고, **대상 인스턴스를 인자로 직접 주입**해야 하는 방식으로 구현되어 있다.



## 참고자료

- [코어 자바스크립트 (도서)](http://www.yes24.com/Product/Goods/78586788)

