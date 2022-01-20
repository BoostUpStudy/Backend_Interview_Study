## IoC(Inversion of Control) 제어의 역전

프로그램의 함수나 객체를 실행하는 코드 제어권을 개발자가 가지는 것이 아닌 제 3자가 가지는 개념입니다.

대부분의 프레임워크는 IoC 를 적용하여 코드의 제어권을 가집니다. 스프링도 객체의 생성, 의존관계 설정, 사용, 제거 등의 제어권을 IoC 컨테이너로 인해 관리되며 개발자는 POJO 만으로 기능 개발을 합니다.

<aside>
💡 POJO?    

Plain Old Java Object 로 오래된 방식의 순수 자바 오프젝트입니다. 추상적으로 복잡한 비지니스 로직이 포함된 무거운 객체가 프레임워크에 종속된다면 객체지향 프로그래밍의 원칙이 깨지게 됩니다. 즉 프레임워크를 사용에 필요한 객체지향적인 원리에 충실하면서, 환경과 기술에 종속되지 않고 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트를 뜻하는 말입니다.

</aside>

### 왜 IoC 가 필요한가?

IoC 는 객체지향 프로그래밍의 5원칙을 잘 지키기 위한 설계 프로그래밍 모델입니다. 개발자는 객체의 역할과 행동만 정의하고 제어권은 컨테이너에게 넘겨주며 생명주기 관리 및 의존관계를 주입하여 높은 응집도와 낮은 결합도를 얻을 수 있습니다.

다시말해 IoC 모델이 객체를 관리하는 독립적인 컨테이너와 객체의 행위를 정의하는 개발자의 역할이 분리되며 변경에 유연한 구조가 만들어지게 됩니다.

<aside>
💡 IoC 는 스프링만의 개념 또는 장점이 절대 아닙니다. 

IoC 는 스프링 프레임워크가 생기기 훨씬 전부터 존재하던 모델이며 현재 사용되는 거의 모든 프레임워크, 템플릿 메소드 디자인 패턴에서 적용되는 개념입니다.

</aside>

## DI(Dependency Injection) 의존성 주입

DI 는 범용적으로 정의된 IoC 모델의 구현 방식입니다. 스프링도 IoC를 구체적으로 DI라는 방식을통해서 의존성 역전 제어를 수행하고 있습니다.

### 의존성

```jsx
public class HasDependecyObject {
	private Obj obj = new Obj();
	
	public void method() {
		obj.run();
  }
}

public class Obj {
	public void method() {
    //
  }
}
```

위 코드에서 처럼 `HasDependencyObject` 는 `Obj` 에 의존하고 있습니다.

이 코드에서 `Obj` 객체의 행동 변경이 생길경우 의존하고 있는 `HasDependencyObject` 도 같이 코드가 변경될 가능성이 높습니다.

### 의존성 주입

이러한 의존성을 해소하기 위해 사용되는 기법으로 외부로부터 객체의 래퍼런스를 주입받아 참조하여 사용하는 방식입니다.

의존성 주입은 아래 3가지 조건을 충족해야 합니다.

- 클래스 모델이나 코드에는 런타임 시점의 의존관계가 드러나지 않는다. 그러기 위해서는 인터페이스에만 의존하고 있어야 한다.
- 런타임 시점의 의존관계는 컨테이너나 팩토리 같은 제3의 존재가 결정한다.
- 의존관계는 사용할 오브젝트에 대한 레퍼런스를 외부에서 제공해줌으로써 만들어진다.

**즉 객체 자신은 고정되어 있으며 제 3자에게 인터페이스를 주입받아 사용되는 것 입니다.**

```jsx
public class Controller {
	private Service service;
	public Controller(Service service) {
		this.service = service;
	}
}

public interface Service {
	void action();
}

public ActionService implements Service {
	@Override
	public void action() {
		//
	}
}

public class Factory {
	public Controller controller1() {
		return new Controller(new ActionService());
	}
}
```

위 코드와 같이 `Controller` 자신은 인터페이스에만 의존하며 행위는 고정되어 있습니다. 제 3자인 Factory 에게 `ActionService` 와의 의존관계를 주입받으며 행동이 결정되는 형태로 코드가 동작합니다.

> 위 예제는 객체의 생성 시점에 의존성이 주입되는 생성자 주입입니다.
의존성 주입 시점으로는 setter, field 주입도 존재합니다.
>

> Spring 은 xml 파일에 개발자가 정의한대로 제 3자인 IoC Container 로 인해 Bean 객체를 생성하고 의존성을 주입하는 방식으로 동작합니다.
>

## AOP(Aspect Oriented Programming) 관점지향프로그래밍

핵심 비지니스 기능과 공통 기능을 분리하여 공통기능의 중복과 객체간 관계 복잡도를 줄이는 프로그래밍 기법입니다.

예를 들어 객체들을 프로그래밍 한다면 로깅 관련 로직의 중복이 많이 발생합니다. 이러한 코드 전반적으로 공통되게 사용되는 로직을 Cross Cutting Concerns 이라고하며 해당 기능들을 모듈화하여 관리하는 것이 AOP 입니다.

AOP 를 적용하면 중복되는 코드 제거, 유지 보수성 향상, 유닛 테스트 편의성의 이점이 있습니다.

### 핵심 용어

- Target : Aspect 대상
- Aspect : 각 객체들의 공통 기능을 모듈화
- Advice : 실질적으로 Aspect가 '무엇'을 '언제' 수행할지를 정의
- JoinPoint : Advice가 적용될 위치, 적용할 위치 등 다양한 시점
- PointCut : JoinPoint는 Advice를 적용할 수 있는 위치의 모음이고 PointCut은 JoinPoint 이 실제로 적용할 위치를 의미

### Spring AOP

Spring 은 트랜잭션, 보안, 권한같은 중복되는 내용을 프록시 디자인 패턴을 이용하여 AOP 효과를 얻습니다.

프록시 패턴의 예시입니다.

```jsx
public interface Subject {
	void action1();
	void action2();
}

public class RealSubject implements Subject {
	@Override
	public void action1() {
		// 시간 측정 시작 로직
		// action1 logic
		// 시간 측정 종료 로직
	}
	@Override
	public void action2() {
		// 시간 측정 시작 로직
		// action2 logic
		// 시간 측정 종료 로직
	}
}
```

이처럼 `Subject` 인터페이스를 참조하는 객체들은 전부 메소드들에는 시간 측정에 대한 로직이 중복됩니다.

이것을 해소하기 위해서 프록시 패턴을 적용하겠습니다.

```jsx
public interface Subject {
	void action1();
	void action2();
}

public class RealSubject implements Subject {
	@Override
	public void action1() {
		// action1 logic
	}
	@Override
	public void action2() {
		// action2 logic
	}
}

public class Proxy implements Subject {
	private RealSubject realSubject;
	@Override
	public void action1() {
		// 시간 측정 시작 로직
		realSubject.action1();
		// 시간 측정 종료 로직
	}
	@Override
	public void action2() {
		// 시간 측정 시작 로직
		realSubject.action2();
		// 시간 측정 종료 로직
	}
}
```

이와 같이 Proxy 를 분리하여 인터페이스를 참조하는 객체들의 중복되는 시간 측정 로직을 감싸서 관리할 수 있습니다.

스프링은 이러한 프록시 디자인 패턴을 기반으로 런타임시 클래스를 빈 객체로 만들 때 같은 클래스 타입의 프록시 빈을 만들어 사용함으로써 AOP 효과를 얻습니다.

## 참고자료

[IoC](https://www.tutorialsteacher.com/ioc/inversion-of-control)

[POJO](https://siyoon210.tistory.com/120)

[Spring IoC, DI](https://biggwang.github.io/2019/08/31/Spring/IoC,%20DI%EB%9E%80%20%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C/)

[Spring DI, DL](https://it-mesung.tistory.com/120)

[AOP](https://annajinee.tistory.com/24)

[Spring AOP](https://devlog-wjdrbs96.tistory.com/398)