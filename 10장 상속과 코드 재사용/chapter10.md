# 10장 상속과 코드 재사용

## Reference

- [오브젝트 - 조영호 저자(글)](https://product.kyobobook.co.kr/detail/S000001766367)

객체지향의 장점은 코드를 재사용하기 용이하다는 것이다. 전통적인 패러다임에서 코드 재사용은 코드를 복사후 수정하는 것이다. 객체지향에서는 코드를 재사용하기 위해서 새로운 코드를 추가한다. 상속은 클래스 안에 정의돈 인스턴스 변수와 메서드를 자동으로 새로운 클래스에 추가하는 구현 방법이다.

객체지향에서 상속 외에도 코드를 효과적으로 재사용할 수 있는 방법은 합성이 있다. 새로운 클래스의 인스턴스 안에 기존 클래스의 인스턴스를 포함시키는 것이다.

## 상속과 중복 코드

### DRY 원칙

중복 코드는 변경을 방해한다. 프로그램의 본질은 비즈니스와 관련된 지식을 코드로 변환하는 것이다. 안타깝게 이 지식은 항상 변한다. 그에 맞춰 코드 역시 변경해야한다.

중복 코드가 가지는 가장 큰 문제는 코드를 수정하는 데 필요한 노력을 몇 배로 증가시킨다. 함께 수정할 필요가 없다면 중복이 아니다.

모양이 유사하다는 것은 단지 중복의 징후일 뿐이다. 중복 여부는 코드가 변경에 반응하는 방식이다.

DRY원칙은 ‘반복하지 마라’라는 뜻의 Don’t Repeat Yourself의 첫 글자를 모아 만든 용어로 동일한 지식을 중복하지 말라는 것이다.

중복코드는 새로운 중복 코드를 부른다. 중복 코드를 제거하지 않고 코드를 수정할 수 있는 유일한 방법은 새로운 중복 코드를 추가하는 것 뿐이다.

중복 코드의 양이 많아질수록 버그의 수는 증가하며 그에 비례해 코드를 변경하는 속도는 점점 느려진다.

### 상속을 이용한 중복 제거

상속을 이용해 코드를 재사용하기 위해서는 부모 클래스의 개발자가 세웠던 가정이나 추론 과정을 정확하게 이해해야 한다.

상속은 결합도를 높인다. 그리고 상속이 초래하는 부모 클래스와 자식 클래스 사이의 강한 결합이 이 코드를 수정하기 어렵게 만든다.

- 상속을 위한 경고1: 자식 클래스의 메서드 안에서 super참조를 이용해 부모 클래스의 메서드를 직접 호출할 경우 두 클래스는 강하게 결합된다. super 호출을 제거할 수 있는 방법을 찾아 결합도를 제거하자.

## 취약한 기반 클래스 문제

부모 클래스의 변경에 의해 자식 클래스가 영향을 받는 현상을 취약한 기반 클래스 문제라고 부른다.

취약한 기반 클래스 문제는 상속이라는 문맥안에 결합도가 초래하는 문제점을 가리키는 용어다. 상속 관계를 추가할수록 전체 시스템의 결합도가 높아진다. 상속은 자식 클래스를 점진적으로 추가해서 기능을 확장하는 데는 용이하지만 높은 결합도로 인해 부모 클래스를 점전적으로 개선하는 것은 어렵게 만든다.

객체를 사용하는 이유는 구현과 관련된 세부사항을 퍼블릭 인터페이스 뒤로 캡슐화할 수 있기 때문이다. 갭슐화는 변경에 의한 파급효과를 제어할 수 있기 때문에 가치가 있다.

하지만 삭속은 부모 클래스의 퍼블릭 인터페이스가 아닌 구현을 변경하더라도 자식 클래스가 영향을 받기 쉬워진다. 상위 클래스에 가해지는 작은 변경으로 상속 계층에 속한 모든 자손들이 급격하게 요동칠 수 있다.

### 불필요한 인터페이스 상속 문제

java.util.Stack의 경우 Vector를 상속받고 있기에, 임의 위치에서 요소를 조회, 추가, 삭제할 수 있는 오퍼레이션을 제공한다. 이는 Stack의 규칙을 쉽게 위반할 수 있다.

인터페이스 설계는 제대로 쓰기엔 쉽게, 엉터리로 쓰기엔 어렵게 만들어야 한다.

- 상속으리 위한 경고2: 상속받은 부모 클래스의 메서드가 자식 클래스의 내부 구조에 대한 규칙을 깨트릴 수 있다.

### 메서드 오버라이딩의 오작용 문제

- 상속을 위한 경고3:  자식 클래스가 부모 클래스의 메서드를 오버라이딩할 경우 부모 클래스가 자신의 메서드를 사용하는 방법에 자식 클래스가 결합될 수 있다.

### 부모 클래스와 자식 클래스의 동시 수정 문제

결합도란 다른 대상에 대해 알고 있는 지식의 양이다. 상속은 기본적으로 부모 클래스의 구현을 재사용한다는 기본 전제를 따르기에 자식 클래스가 부모 클래스의 내부에 대해 속속히 알도록 강요한다.

- 상속을 위한 경고4: 클래스를 상속하면 결합도로 인해 자식 클래스와 부모 클래스의 구현을 영원히 변경하지 않거나, 자식 클래스와 부모 클래스를 동시에 변경하거나 둘 중 하나를 선택할 수밖에 없다.

## 추상화

### 추상화에 의존하자

부모 클래스와 자식 클래스 모두 추상화에 의존하도록 수정하면 된다. 코드 중복을 제거하기 위해 상속을 도입하기 위해서는 두 가지 원칙이 있다.

- 두 메서드가 유사하면 차이점을 메서드로 추출해라. 메서드 추출을 통해 두 메서드를 동일한 형태로 보이도록 만들 수 있다.
- 부모 클래스의 코드를 하위로 내리지 말고 자식 클래스의 코드를 상위로 올려라.

### 차이를 메서드로 추출하라

- 변하는 것으로부터 변하지 않는 것을 분리하라, 변하는 부분을 찾고 이를 캡슐화하라

### 중복 코드를 부모 클래스로 올려라

공통 코드를 옮길 때 인스턴스 변수보다 메서드를 먼저 이동시키는 게 편하다. 메서드를 옮기고 나서 그 메서드에 필요한 메서드나 인스턴스 변수가 무엇인지를 컴파일 에러를 통해 자동으로 알 수 있기 때문이다.

## 차이에 의한 프로그래밍

기존 코드와 다른 부분만 추가함으로써 애플리케이션의 기능을 확장하는 방법을 차이에 의한 프로그래밍이라 부른다. 상속을 이용하면 이미 존재하는 클래스의 코드를 쉽게 재사용할 수 있기 때문에 애플리케이션의 점진적인 정의가 가능해진다.

상속은 코드 재사용과 관련된 대부분의 경우에 우아한 해결 방법이 아니다. 객체지향에 능숙한 개발자들은 상속의 단점을 피하면서도 코드를 재사용할 수 있는 더 좋은 방법은 합성이다.