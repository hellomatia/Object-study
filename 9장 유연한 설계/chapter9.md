# 9장 유연한 설계

## Reference

- [오브젝트 - 조영호 저자(글)](https://product.kyobobook.co.kr/detail/S000001766367)

## 개방-패쇄 원칙

소프트웨어 개체는 확장에 대해 열려 있어야 하고, 수정에 대해서는 닫혀 있어야 한다.

- 확장에 대해 열려 있다: 애플리케이션의 요구사항이 변경될 때 이 변경에 맞게 새로운 동작을 추가해서 애플리케이션의 기능을 확장할 수 있다.
- 수정에 대해 닫혀 있다: 기존 코드를 수정하지 않고도 애플리케이션의 동작을 추가하거나 변경할 수 있다.

### 컴파일타임 의존성을 고정시키고 런타임 의존성을 변경하라

런타임 의존성은 실행시에 협력에 참여하는 객체들 사이의 관계다. 컴파일타임 의존성은 코드에서 드러나는 클래스들 사이의 관계다.

### 추상화가 핵심이다

개방-폐쇄 원칙의 핵심은 추상화에 의존하는 것이다. 추상화란 핵심적인 부분만 남기고 불필요한 부분은 생략함으로써 복잡성을 극복하는 기법이다.

## 생성 사용 분리

유연하고 재사용 가능한 설계를 원한다면 객체와 관련된 두 가지 책임을 서로 다른 객체로 분리해야 한다. 하나는 객체를 생성하는 것이고, 다른 하나는 객체를 사용하는 것이다. 한 마디로 객체에 대한 생성과 사용을 분리해야 한다.

소프트웨어 시스템은 시작 단계와 실행 단계를 분리해야 한다.

### FACTORY 추가하기

생성과 사용을 분리하기 위해 객체 생성에 특화된 객체를 FACTORY라 부른다.

### 순수한 가공물에게 책임 할당하기

FACTORY는 도메인 모델에 속하지 않는다. 순수하게 기술적인 결정이다. 전체적으로 결합도를 낮추고 재사용성을 높이기 위해 도메인 개념에게 할당돼 있던 객체 생성을 도메인 개념과 아무런 관련없는 가공의 객체로 이동시킨 것이다.

객체로 분해하는 데는 표현적 분해와 행위적 분해다.

표현적 분해는 도메인에 존재하는 사물 또는 개념을 표현하는 객체들을 이용해 시스템을 분해하는 것이다.

모든 책임을 도메인 객체에 할당하면 낮은 응집도, 높은 결합도, 재사용성 저하와 같은 심각한 문제점에 봉착하게 될 가능성이 높아지게 된다. 이 경우에 표현할 객체가 아닌 설계자가 편의를 위해 임의로 만들어낸 가공의 객체에게 책임을 할당해서 문제를 해결해야 한다. 이를 순수한 가공물이라 부른다.

순수한 가공물은 표현적 분해보다는 행위적 분해에 의해 생성되는 것이 일반적이다.

## 의존성 주입

객체가 아닌 외부의 독립적인 객체가 인스턴스를 생성한 후 이를 전달해서 의존성을 해결하는 방법을 의존성 주입이라 부른다. 외부에서 의존성의 대상을 해결한 후 이를 사용하는 객체 쪽으로 주입하기 때문이다.

setter 주입의 단점은 객체가 올바로 생성되기 위해 어떤 의존성이 필수적인지를 명시적으로 표현할 수 없다. setter메서드는 객체가 생성된 후에 호출돼야 하기 때문에 setter메서드 호출을 누락하면 비정상적인 상태로 생성된다.

메서드 주입은 메서드 호출 주입이라 부르며 메서드가 의존성을 필요로 하는 유일한 경우에 사용할 수 있다. 생성자 주입을 통해 의존성을 전달 받으면 객체가 올바른 상태로 생성되는 데 필요한 의존성을 명확하게 표현할 수 있다는 장점이 있지만 주입된 의존성이 한 두 개의 메서드에서만 사용된다면 각 메서드의 인자로 전달하는 것이 더 나은 방법일 수 있다.

### 숨겨진 의존성은 나쁘다

가능하다면 의존성을 명시적으로 표현할 수 있는 기법을 사용하라. 의존성 주입은 의존성을 ㅁ여시적으로 명시할 수 있는 방법 중 하나일 뿐이다.

## 의존성 역전 원칙

### 추상화와 의존성 역전

구체 클래스는 의존성의 시작점이 어야 한다. 의존성이 목적지가 되어서는 안된다.

- 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안 된다. 둘 모두 추상화에 의존해야 한다.
- 추상화는 구체적인 사항에 의존해서는 안된다. 구체적인 사항은 추상화에 의존해야 한다.

이를 의존성 역전 원칙이라 부른다.

### 의존성 역전 원칙과 패키지

역전은 의존성의 방향뿐만 아니라 인터페이스의 소유권에도 적용된다. 의존성 역전 원칙에 따라 상위 수준의 협력 흐름을 재사용하기 위해서는 추상화가 제공하는 인터페이스의 소유권 역시 역전시켜야 한다.

## 우연성에 대한 조언

### 유연한 설계는 유연성이 필요할 때만 옳다

유연하고 재사용 가능한 설계가 항상 좋은 건 아니다. 설계의 미덕은 단순함과 명확함으로부터 나온다. 변경하기 쉽고 확장하기 쉬운 구조를 만들기 윟새서는 단순함과 명확함의 미덕을 버리게 될 가능성이 높다.

미래에 변경이 일어날지도 모른다는 막연한 불안감은 불필요하게 복잡한 설계를 낳는다. 아직 일어나지 않은 변경은 변경이 아니다.

설계가 유연할수록 클래스 구조와 객체 구조 사이의 거리는 점점 멀어진다.

불필요한 유연성은 불필요한 복잡성을 낳는다. 단순하고 명확한 해법이 그런대로 만족스럽다면 유연성을 제거하라.

### 협력과 책임이 중요하다

다양한 컨텍스트에서 협력을 재사용할 필요가 없다면 설계를 유연하게 만들 당위성도 사라진다.

객체를 생성할 책임을 담당할 객체나 객체 생성 메커니즘을 결정하는 시점은 책임 할당의 마지막 단계로 미뤄야 한다.

책임의 불균형이 심화되고 있는 상태에서 객체의 생성 책임을 지우는 것은 설계를 하부의 특정 메커니즘에 종속적으로 만들 확률이 높다.