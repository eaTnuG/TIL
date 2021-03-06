# Factory Method - a.k.a Virtual Constructor

## Intent

팩토리 메소드는 상위클래스에서 객체 생성을 위한 인터페이스를 제공하고, 하위클래스에서 객체의 타입을 수정할 수 있게 해주는 방법으로, creational design pattern 중 하나이다.

## Problem

물류 매니지먼트 어플리케이션을 만든다고 상상해보자. 첫번째 버전에서는 트럭을 통한 운송밖에 다룰 수 없다. 따라서 코드의 대부분이 `Truck` 클래스 내부에 존재할 것이다.

시간이 지나고 앱이 커져서, 하루에도 몇번씩이나 해상물류의 형태도 앱에 포함시켜 달라는 요청이 들어온다. 좋은 소식이지만, 코드는 어떻게 하지?

지금 대부분의 코드는 `Truck` 클래스와 연결되어있다. 앱에 `Ship` 클래스를 추가하는 작업은 전체 코드베이스의 수정을 필요로 할 것이다. 게다가 추후에 또 다른 운송수단을 추가하기로 할 경우, 똑같은 작업을 또 반복해야 할 것 이다.

결국 코드는 지저분해 질 것이고, 운송수단 객체의 타입에 따라 코드의 흐름이 변하는 어지러운 형태가 될 것이다.

## Solution

팩토리 메소드 패턴은 객체 생성 호출을 `new` 키워드를 사용해 직접하는 대신에 특별한 `팩토리` 메소드를 사용할 것을 제안한다. 걱정마라, 객체는 여전히 `new` 키워드를 호출해서 생성되만, 이 작업은 `팩토리` 메소드 내부에서 이루어지는 것이다. 팩토리 메소드에서 리턴된 객체는 보통 프로덕트라고 부른다.

그냥 설명만 읽어봤을때는 별로 차이가 없어보인다. 그냥 생성자를 프로그램의 다른 부분에서 호출할 뿐인거 같다. 하지만 이제 팩토리 메소드를 오버라이딩해서 반환되는 객체의 타입을 바꿀 수 있다는 것을 생각하자.

약간의 제약사항은 있다. 하위클래스는 공통된 베이스 클래스나 인터페이스가 있을 경우에만 서로 다른 타입의 프로덕트를 반환할 수 있다. 또한 베이스 클래스의 팩토리 메소드가 리턴하는 타입도 인터페이스에 정의되어 있어야한다.

예를들어 `Truck`과 `Ship` 클래스는 `Transport` 인터페이스를 implement 해야하고, 인터페이스는 `deliver` 라는 메소드를 갖고있다. 각 클래스는 이 메소드를 다른 형태로 구현한다: 트럭은 육지로, 배는 물 위로 화물을 운반하니까. `RoadLogistics` 클래스의 팩토리 메소드는 트럭 오브젝트를, `SeaLogistics`클래스는 배 오브젝트를 리턴한다.

팩토리 메소드를 이용하는 코드( 보통 클라이언트 코드라고 부른다 )는 다양한 하위 클래스들에서 반환된 프로덕트들의 차이를 알지 못한다. 그저 모든 프로덕트들을 한층 가려진 `Transport` 인터페이스로 사용할 뿐이다. 모든 프로덕트가 `deliver` 메소드를 가지고 있다면 클라이언트 쪽에서 내부 사정을 알 필요가 없다.

## Structure

![uml](https://github.com/eaTnuG/TIL/blob/master/statics/factory_method.png)

1. creator나 그 하위클래스들로 생성될 수 있는 모든 오브젝트의 공통부분인 product는 인터페이스를 선언한다.
2. concept product는 product 인터페이스의 서로 다른 구현체들이다.
3. creator 클래스는 새로운 프로덕트 객체를 리턴하는 팩토리 메소드를 선언한다. 리턴타입과 프로덕트 인터페이스의 타입이 매치되어야한다.

팩토리메소드를 추상메소드로 선언해서 모든 하위클래스가 강제로 그들만의 메소드를 구현하도록 강요할 수 도 있고, 베이스 팩토리 메소드가 기본 프로덕트 타입을 리턴하도록 할 수 도 있다.

이름은 creator이지만 프로덕트 생산이 이 클래스의 근본적인 responsiblity는 아니다. 보통 creator 클래스는 프로덕트와 연관된 코어 비즈니스로직을 가지고 있다. 팩토리 메소드는 이 비즈니스로직과 concrete product 클래스간의 연관성을 줄여준다.

4. concrete creator는 베이스 팩토리 메소드를 오버라이딩해서 다른 타입의 프로덕트를 생산해낸다.

## Psuedocode

는 생략했다.

## Applicability

- 어떤 오브젝트가 상호작용하거나 의존하게 될 상대의 타입을 미리 알 수 없을 떄 사용할 수 있다.
- 당신의 라이브러리나 프레임워크 사용자에게 확장할 수 있는 옵션을 주고싶을 떄 사용할 수 있다.
- 객체를 매번 새로 생성하는 대신 재사용함으로서 시스템 자원을 아끼고 싶을 떄 사용할 수 있다.

## How to implement

도 생략했다.

## Pros and Cons

- P] creator 와 concrete products 간의 높은 결합도 문제를 해결할 수 있다.
- P] 단일책임원칙을 지킬 수 있다.
- P] 개방/폐쇄 원칙을 지킬 수 있다.
- C] 하위클래스가 많아져서 코드가 복잡해질 수 있다.
