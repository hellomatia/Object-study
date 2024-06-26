# 8장 의존성 관리하기

## Reference

- [오브젝트 - 조영호 저자(글)](https://product.kyobobook.co.kr/detail/S000001766367)

잘 설계된 객체지향 애플리케이션은 작고 응집도 높은 객체들로 구성된다. 작고 응집도 높은 객체란 책임의 초점이 명확하고 한 가지 일만 잘하는 객체를 의미한다.

협력은 필수적이지만 과도한 협력은 설계를 곤경에 빠트릴 수 있다. 협력은 객체가 다른 객체에 대해 알 것을 강요한다. 이런 지식이 객체 사이의 의존성을 낳는다.

객체지향 설계의 핵심은 협력을 위해 필요한 의존성은 유지하면서 변경을 방해하는 의존성은 제거하는 데 있다.

## 의존성 이해하기

### 변경과 의존성

어떤 객체가 협력하기 위해 다른 객체를 필요로 할 때 두 객체 사이에 의존성이 존재하게 된다.

의존성은 실행 시점과 구현 시점에 서로 다른 의미를 가진다.

- 실행 시점: 의존하는 객체가 정상적으로 동작하기 위해서는 실행 시에 의존 대상 객체가 반드시 존재해야 한다.
- 구현 시점: 의존 대상 객체가 변경될 경우 의존하는 객체도 함께 변경된다.

### 의존성 전이

의존성은 전이될 수 있기 때문에 의존성의 종류를 직접 의존성과 간접 의존성으로 나누기도 한다.

직접 의존성: 한 요소가 다른 요소에 직접 의존하는 경우

간접 의존성: 직접적인 관계에 존재하지 않지만 의존성 전이에 의해 영향이 전파되는 경우

### 런타임 의존성과 컴파일타임 의존성

컴파일 의존성: 코드를 컴파일하는 시점을 가리키지만 문맥에 따라 코드 그 자체를 가리키는 시점에 발생하는 의존성이다. (⇒ 주인공: 클래스)

런타임 의존성: 코드가 실행되는 시점에서 발생하는 의존성이다. (⇒ 주인공: 객체)

어떤 클래스의 인스턴스가 다양한 클래스의 인스턴스와 협력하기 위해서는 협력할 인스턴스의 구체적인 클래스를 알아서는 안 된다. 실제로 협력할 객체가 어떤 것인지는 런터임에 해결해야 한다.

### 컨텍스트 독립성

클래스가 특정한 문맥에 강하게 결합될 수록 다른 문맥에서는 사용하기 어려워진다. 클래스가 사용될 특정한 문맥에 최소한 가정만으로 ㅇ이루어져 있다면, 다른 문맥에서 재사용하기 수월해진다. 이를 컨텍스트 독립성이라 한다.

### 의존성 해결하기

컴파일 타임 의존성을 실행 컨텍스트에 맞는 적절한 의존성으로 교체하는 것을 의존성 해결이라 부른다.

- 객체를 생성하는 시점에서 생성자를 통해 의존성 해결
- 객체 생성 후 setter메서드를 통해 의존성 해결
- 메서드 실행 시 인자를 이용해 의존성 해결

setter메서드를 이용하는 방식은 실행 시점에서 의존 대상을 변경할 수 있기에 설계를 더 유연하게 만들 수 있지만, 생성된 후 의존 대상을 설정하기에 객체의 상태가 불완전해 질 수 있다.

더 좋은 방식은 생성자 방식과 setter방식을 혼합하는 것이다. 항상 객체를 생성할 때 의존성을 해결해 완전한 상태의 객체를 생성한 후, 필요에 따라 setter메서드를 이용해 의존 대상은 변경할 수 있다.

메서드 인자를 사용하는 방식은 의존 대상이 매번 달라져야 하는 경우 유용하지만, 대부분의 매번 동일한 객체를 인자로 전달하고 있다면 생성자나 setter메서드를 이용해 의존성을 해결하는 것이 좋다.

## 유연한 설계

### 의존성과 결합도

객체지향 패러다임의 근간은 협력이다. 객체들은 협력을 통해 생명력을 불어넣는다. 객체들은 협력하기 위해 서로의 정보가 필요하다. 이러한 정보들은 객체들 사이의 의존성을 발생시킨다.

그렇기에 모든 의존성이 나쁜게 아니다. 하지만, 의존성이 강하면 문제가 될 수 있다.

바람직한 의존성은 재사용할 수 있다면, 그 의존성은 바람직한 것이다.

바람직한 의존성과 바람직하지 못한 의존성을 가리키는 좀 더 세련된 용어가 결합도이다. 두 요소 사이의 의존성이 바람직할 때, 느슨한 결합도라 하고 의존성이 바람직하지 못할 경우 강한 결합도라 한다.

### 지식이 결합을 낳는다

더 많이 알면 알수록 더 많이 결합된다. 더 많이 알고 있다는 것은 더 적은 컨텍스트에서 재사용 가능하다는 것을 의미한다. 결합도를 느슨하게 유지하려면 협력하는 대상에 대해 더 적게 알아야 한다.

이 목적을 달성할 수 있는 가장 효과적인 방법은 추상화이다.

### 추상화에 의존하라

추상화란 어떤 양상, 세부사항, 구조를 좀 더 명확하게 이해하기 위해 특정 절차나 물체를 의도적으로 생략하거나 감춤으로써 복잡도를 극복하는 방법이다.

### 명시적인 의존성

의존성의 대상을 생성자나, setter로 받는다는 의미는 퍼블릭 인터페이스에 드러낸다는 것이다. 이를 명시적인 의존성이라 부른다.

반면, 직접적으로 내부에서 의존성을 설정하는 것을 숨겨진 의존성이라 부른다.

의존성이 명시되지 않으면 의존성을 파악하기 위해 내부 구현을 직접적으로 살펴볼 수 밖에 없다. 의존성이 명시적이지 않으면 클래스를 다른 컨텍스트에서 재사용하기 위해 내부 구현을 직접 변경해야 한다.

의존성은 명시적으로 표현되어야 한다. 유연하고 재사용 가능한 설계란 퍼블릭 인터페이스를 통해 의존성이 명시적으로 드러나는 설계이다.

### new는 해롭다

대부분의 언어에서 클래스의 인스턴스를 생성할 수 있는 new 연산자를 제공한다. 하지만 안타깝게도 new를 잘못 사용하면 클래스 사이의 결합도가 극단적으로 높아진다.

- new 연산자를 사용하기 위해서는 구체 클래스의 이름을 직접 기술해야 한다.
- new 연산자는 생성하려는 구체 클래스뿐만 아니라 어떤 인자를 이용해 클래스의 새ㅣㅇ성자를 호출해야 하는지도 알아야 한다.

### 가끔은 생성해도 무방하다

클래스 안에서 객체의 인스턴스를 직접 생성하는 방식이 유용한 경우도 있다. 주로 협력한는 기본 객체를 설정하고 싶은 경우가 여기에 속한다.

### 표준 클래스에 대한 의존은 해롭지 않다

JDK의 표준 컬렉션 라이브러리에 속한 ArrayList의 경우 직접 생성하더라도 문제가 되지 않는다. 수정될 확률이 0에 가깝기 때문이다.

### 조합 가능한 행동

유연하고 재사용 가능한 설계는 객체가 어떻게하는지를 장황하게 나열하지 않고도 객체들의 조합을 통해 무엇을 하는지를 표현하는 클래스들로 구성된다.