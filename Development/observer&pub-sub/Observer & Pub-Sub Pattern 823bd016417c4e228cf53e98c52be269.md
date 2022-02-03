# Observer & Pub-Sub Pattern

## Design Pattern

<aside>
💡 Design Pattern이란 SW를 설계할 때 발생하는 문제들의 대한 해결책들이다.

</aside>

SW는 긴 기간동안 많은 문제를 만나고 해결하는 과정에서 성장할 수 있었다. 거기서 선배님?들이 겪고, 앞으로 비슷한 문제를 겪었을 때 적용할 수 있도록 고민해놓은 해결방안들이다.

### Design Pattern 구조

- Context: 패턴이 적용될 수 있는 상황, 유용하지 못한 상황
- Problem: 패턴으로 해결될 필요가 있는 이슈들
- Solution: 문제를 해결하도록 하는 방법

### Design Pattern 종류

- Creational(생성) Pattern: 객체 생성과 관련된 패턴
- Structural(구조) Pattern: 객체를 조합해 더 큰 구조를 만드는 패턴
- Behavioral(행위) Pattern: 객체 사이의 알고리즘이나 책임분배에 관련된 패턴

## Observer

<aside>
💡 객체의 상태 변화를 관찰하는 관찰자들을 등록하고, 변화시 옵저버들에게 변화를 알리는 패턴

</aside>

![Observer들의 함수를 직접 호출한다.](Observer%20&%20Pub-Sub%20Pattern%20823bd016417c4e228cf53e98c52be269/Untitled.png)

Observer들의 함수를 직접 호출한다.

![Subject가 변화가 발생하면 Observer들의 notify함수를 실행한다.](Observer%20&%20Pub-Sub%20Pattern%20823bd016417c4e228cf53e98c52be269/Untitled%201.png)

Subject가 변화가 발생하면 Observer들의 notify함수를 실행한다.

- Subject: 관찰을 받는 관찰 대상
- Observer: 관찰 observer
- Subscribe(구독): subject에 observer를 추가하는 행위(observer가 subject를 구독한다)

> javascript의 addEventListener도 Observer Pattern이라고 할 수 있다. Event에 대해서 Observer(Listener)를 달아주기 때문이다.
> 

> javascript의 접근자 속성(getter, putter), Proxy객체를 활용해서도 만들 수도 있다. 속성이 바뀔 때(set)의 경우 비지니스 로직에 Observer를 달 수 있기 때문이다.
> 

## Pub-Sub

<aside>
💡 Topic을 제어해주는 Broker를 두고, Publisher와 Subscriber가 Broker에게 Topic을 구독또는 발행한다.

</aside>

![중간에 메시지 큐를 관리해주는 브로커를 통해서 전달된다.](Observer%20&%20Pub-Sub%20Pattern%20823bd016417c4e228cf53e98c52be269/Untitled%202.png)

중간에 메시지 큐를 관리해주는 브로커를 통해서 전달된다.

- Broker(Event Bus): 메시지(토픽)들을 전달
- Publisher: 메시지(토픽)을 생성및 전달
- Subscriber: 메시지(토픽)을 구독

## Observer VS Pub-Sub

<aside>
💡 가장 큰 차이점은 결합도이다. Observer Pattern은 객체들이 서로를 알고 있어야 하지만, Pub-Sub Pattern은 객체들은 Broker만 알고 서로를 모른다.
추가로, 구현 방식과 확장성이 있다.

</aside>

- 결합도: 객체와 객체의 관계의 의존성의 정도
    
    > 결합도가 높으면 수정과 확장에 불리하다. 하나의 변경점에 대해서 코드를 모두 추가하고 수정해야되기 때문이다.
    > 

![Pub-Sub은 한 단계를 더 거침으로써 결함도를 낮출 수 있다.](Observer%20&%20Pub-Sub%20Pattern%20823bd016417c4e228cf53e98c52be269/Untitled%203.png)

Pub-Sub은 한 단계를 더 거침으로써 결함도를 낮출 수 있다.

### 비교

|  | Observer | Pub-Sub |
| --- | --- | --- |
| 의존성 | 옵저버 패턴은 옵저버들이 객체들을 알고 있고, 객체들은 옵저버들의 기록을 가지고 있다. | publisher와 subscriber는 서로 몰라도 되고, 메시지 큐들이나 브로커를 통해서 소통한다. |
| 결합도 | 높음 | 낮음 |
| 구현 방식 | 대부분 동기 방식(이벤트 발생 시, 객체가 모든 옵저버의 적절한 메서드들을 호출) | 비동기 방식(메시지 큐 사용) |
| 확장성 | 하나의 애플리케이션에서 구현 | 크로스 애플리케이션 구현 |
| 응집도(이벤트 관점) | 높음 | 낮음 |
| 응집도(객체 관점) | 낮음 | 높음 |

> 확장성에서 하나의 어플리케이션과 크로스 어플리케이션은, Observer는 Observer Class에서 모두 구현할 수 있는 반면에 Pub-Sub는 Publisher와 Subscriber모두 따로 구현해야 한다는 의미이다.
이를 통해서, 응집도를 유추할 수 있는데 Observer는 필요한 코드가 비교적 모여있으므로 높은 응집도를 가지고, Pub-Sub은 반대이다.
> 

## 예상 질문

- 디자인 패턴이란 무엇인가요?
- 옵저버 패턴이란 무엇잇가요?
    
    
- 구독 발행 패턴이란 무엇인가요?
- 옵저버와 구독 발행의 차이점이 무엇인가요?
- 언제 옵저버와 구독 발행을 사용해야 할까요?

## 참고

- Design Pattern
    
    [[Design Pattern] 디자인 패턴 종류 - Heee's Development Blog](https://gmlwjd9405.github.io/2018/07/06/design-pattern.html)
    
- Observer
    
    [(Design Pattern) Observer Pattern 이란?](https://medium.com/@su_bak/design-pattern-observer-pattern-%EC%9D%B4%EB%9E%80-ef4b74303359)
    
- Observer VS Pub-Sub
    
    [[WebFlux] publisher(발행) - subscriber(구독) 패턴에 대해서](https://zorba91.tistory.com/291)