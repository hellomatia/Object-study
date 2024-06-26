# 13장 서브클래싱과 서브타이핑

## Reference

- [오브젝트 - 조영호 저자(글)](https://product.kyobobook.co.kr/detail/S000001766367)

상속의 첫 번쨰 용도는 타입 계층을 구현하는 것이다. 타입 계층 안에서 부모 클래스는 일반적인 개념을 구현하고 자식 클래스는 특수한 개념을 구현한다.

타입 계층의 관점에서 부모 클래스는 자식 클래스의 일반화이고 자식 클래스는 부모 클래스의 특수화다.

상속의 두 번쨰 용도는 코드 재사용이다. 상속을 사용하면 점진적으로 애플리케이션의 기능을 확장할 수 있다. 하지만 재사용을 위해 상속을 사용할 경우 부모 클래스와 자식 클래스가 강하게 결합되기에 변경하기 어려운 코드를 얻게 될 확률이 높다.

상속은 코드 재사용이 아니라 타입 계층을 구현하는 것이다.

동일한 메시지에 대해 서로 다르게 행동할 수 있는 다형적인 객체를 구현하기 위해서는 객체의 행동을 기반으로 타입 계층을 구성해야 한다.

## 타입

### 개념 관점의 타입

개념 관점에서 타입은 우리가 인지하는 세상의 사물의 종류를 의미한다. 어떤 타입으로 분류될 때 그 대상을 타입의 인스턴스라고 부른다. 안스턴스를 객체라 부른다.

### 프로그래밍 언어 관점의 타입

연속된 비트에 의미와 제약을 부여하기 위해 사용된다. 비트 자체에는 타입이라는 개념이 존재하지 않는다. 비트에 담긴 데이터를 문자열로 다룰지, 정수로 다룰지는 전적으로 데이터를 사용하는 애플리케이션에 의해 결정된다.

- 타입에 수행될 수 있는 유효한 오퍼레이션의 집합을 정의한다.
- 타입에 수행되는 오퍼레이션에 대해 미리 약속된 문맥을 제공한다.

타입은 적용 가능한 오퍼레이션의 종류와 의미를 정의하여 코드의 의미를 명확하게 전달하고 개발자의 실수를 방지하기 위해 사용된다.

### 객체지향 패러다임 관점의 타입

객체지향에서 객체의 타입이란 객체가 수신할 수 있는 메시지의 종류를 정의하는 것이다. 객체가 수신할 수 있는 메시지의 집합을 가리키는 멋진 용어가 바로 퍼블릭 인터페이스이다.

객체지향에서는 객체가 수신할 수 있는 메시지를 기준으로 타입을 분류하기에 동일한 퍼블릭 인터페이스를 가지는 객체들은 동일한 타입으로 분류할 수 있다.

객체에게 가장 중요한 것은 속성이 아닌 행동이다.

## 타입 계층

### 타입 사이의 포함 관계

계층을 구성하느 두 타입 간의 관계에서 더 일반적인 타입을 슈퍼타입이라 부르고, 더 특수한 타입을 서브타입이라 부른다.

일반화란 어떤 타입의 정의를 좀 더 보편적이고 추상적으로 만드는 과정을 의미한다.

특수화는 어떤 타입의 정의를 좀 더 구체적이고 문맥 종속적으로 만드는 과정을 의미한다.

- 슈퍼타입
  - 집합이 다른 집함의 모든 멤버를 포함한다.
  - 타입 정의가 다른 타입보다 좀 더 일반적이다.
- 서브타입
  - 집합에 포함된 인스턴스들이 더 큰 집합에 포함된다.
  - 타입 정의가 다른 타입보다 좀 더 구체적이다.

### 객체지향 프로그밍과 타입 계층

- 슈퍼타입은 서브타입이 정의한 퍼블릭 인터페이스를 일반화시켜 상대적으로 범용적이고 넓은 의미로 정의한 것이다.
- 서브타입이란 슈퍼타입이 정의한 퍼블릭 인터페이스를 특수화시켜 상대적으로 구체적이고 좁은 의미로 정의한 것이다.

서브타입의 인스턴스는 슈퍼타입의 인스턴스로 간주될 수 있다.

## 서브클래싱과 서브타이핑

객체지향 프로그래밍 언어에서 타입을 구현하는 일반적인 방법은 클래스를 이용하는 것이다. 타입 계층을 구현하는 일반적인 방법은 상속을 이용하는 것이다. 상속을 이용해 타입 계층을 구현한다는 것은 부모 클래스가 슈퍼타입의 역할, 자식 클래스가 서브타입의 역할을 수행하는 것이다.

### 언제 상속을 사용해야 하는가?

상속의 올바른 용도는 타입 계층을 구현하는 것이다.

마틴 오더스키의 질문

- 상속 관계가 is-a관계를 모델링하는가?
- 클라이언트 입장에서 부모 클래스의 타입으로 자식 클래스를 사용해도 무방한가?

### is-a 관계

어휘적으로 is-a관계를 모델링할 경우에만 상속을 사용해야 한다.

슈퍼타입과 서브타입 관계에서는 is-a보다 행동 호환성이 더 중요하다. ex) 팽귄은 새인가? 그럼 날 수 있는가?

### 행동 호환성

타입의 이름 사이에 개념적으로 연관성이 있더라도 행동에 연관성이 없으면 is-a관계를 사용하지 말아야 한다.

행동의 호환 여부를 판단하는 기준은 클라이언트의 관점이다. 클라이언트가 두 타입이 동일하게 행동할 것이라고 기대한다면 두 타입을 타입 계층으로 묶을 수 있다.

### 클라이언트의 기대에 따라 계층 분리하기

행동 호환성을 만족시키지 않는 상속 계층을 그대로 유지한 채 클라이언트의 기대를 충족시킬 수 있는 방법은 찾기가 쉽지 않다. 문제를 해결할 수 있는 방법은 클라이언트의 기대에 맞게 상속 계층을 분리하는 것 뿐이다.

인터페이스를 클라이언트의 기대에 따라 분리함으로써 변경에 의해 영향을 제어하는 설계 원칙을 인터페이스 분리 원칙이라 부른다.

- 소프트웨어에 이상적인 설계 같은 것은 없다.

자연어에 현혹되지 말고 요구사항 속에서 클라이언트가 기대하는 행동에 집중하자. 클래스의 이름 사이에 어떤 연관성이 있다는 사실은 아무런 의미도 없다.

### 서브클래싱과 서브타이핑

- 서브 클래싱: 다른 클래스의 코드를 재사용할 목적으로 상속을 사용하는 경우
- 서브 타이핑: 타입 계층을 구성하기 위해 상속을 사용하는 경우

개념적으로 서브타입이 슈퍼타입의 퍼블릭 인터페이스를 상속받는 것처럼 보이게 된다. 그에 반해 서브클래싱은 클래스의 내부 구현 자체를 상속받는 것에 초점을 맞춘다.

서브타이핑 관계가 유지되기 위해서는 서브타입이 슈퍼타입이 하는 모든 행동을 동일하게 할 수 있어야 한다.

자식 클래스와 부모 클래스 사이의 행동 호환성은 부모 클래스에 대한 자식 클래스의 대체 가능성을 포함한다.

## 리스코프 치환 원칙

바바라 리스코프는 올바른 상속 관계의 특징을 정의하기 위해 리스코프 치환 원칙을 발표했다.

리스코프 치환 원칙은 서브타입은 그것의 기반 타입에 대해 대체 가능해야 한다는 것이다. 리스코프 치환 원칙은 앞에 논의한 행동 호환성을 설계 원칙으로 정리한 것이다. 리스코프 치환 원칙에 따르면 자식 클래스가 부모 클래스와 행동 호환성을 유지하여 부모 클래스를 대체할 수 있도록 구현된 상속 관계만을 서브타이핑이라고 부른다.

Stack과 Vector는 리스코프 치환 원칙을 위반하는 전형적인 예이다. 클라이언트는 Vector에 대해 기대하는 행동을 Stack에 대해서는 기대할 수 없기 때문이다.

### 클라이언트와 대체 가능성

리스코프 치환 원칙은 자식 클래스가 부모 클래스를 대체하기 위해서 부모 클래스에 대한 클라이언트의 가정을 준수해야 한다는 것을 강조한다.

리스코프 치환 원칙은 클라이언트와 격리한 채로 본 모델은 검증하는 것이 불가능하다는 중요한 결론을 이끈다.

상속 관계는 클라이언트의 고나점에서 자식 클래스가 부모 클래스를 대체할 수 있을때만 올바르다.

### is-a 관계 다시 살펴보기

is-a관계에서 중요한 것은 객체의 속성이 아닌 객체의 행동이다. 일반적으로 클라이언트를 고려하지 않은 채 개념과 속성의 측면에서 상속관계를 정할 경우 리스코프 치환 원칙을 위반하는 서브클래싱이 이르게 될 확률이 높다.

### 리스코프 치환 원칙은 유연한 설계의 기반이다

새로운 자식 클래스를 추가하더라도 클라이언트의 입장에서 동일하게 행동하기만 한다면 클라이언트를 수정하지 않고도 상속 계층을 확장할 수 있다.

리스코프 치환 원칙을 따르는 설계는 유연한 설계뿐만 아니라 확장성이 높다.

일반적으로 리스코프 치환 원칙 위반은 잠재적인 개방-폐쇄 원칙 위반이다.

## 계약에 의한 설계와 서브타이핑

클라이언트와 서버 사이의 협력을 의무와 이익으로 구성된 계약의 관점에서 표현하는 것을 계약에 의한 설계라고 부른다. 계약에 의한 설계는 클라이언트가 정상적으로 메서드를 실행학 위해 만족시켜야 하는 사전조건과 메서드가 실행된 후에 서버가 클라이언트에 보장해야 하는 사후조건, 메서드 실행 전과 실행 후에 인스턴스가 만족시켜야 하는 클래스 불변식의 세 가지 요소로 구성된다.

- 서브타입이 리스코프 치환 원칙을 만족시키기 위해서는 클라이언트와 슈퍼타입 간에 체결된 ‘계약’을 준수해야 한다.

### 서브타입과 계약

- 서브타입에 더 강력한 사전조건을 정의할 수 없다.
- 서브타입에 슈퍼타입과 같거나 더 약한 사전조건을 정의할 수 있다.
- 서브타입에 슈퍼타입과 같거나 더 강한 사후조건을 정의할 수 있다.
- 서브타입에 더 약한 사후조건을 정의할 수 없다.