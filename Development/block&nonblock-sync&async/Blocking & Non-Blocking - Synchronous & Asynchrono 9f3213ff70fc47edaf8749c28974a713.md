# Blocking & Non-Blocking - Synchronous & Asynchronous

## 🐌 용어 정리

- 제어권: 코드를 실행할 권리
    
    > 제어권을 가진 Context는 자신을 실행한 후, 부모(자신을 호출한) Context로 제어권을 돌려준다.
    > 

## 🧞‍♀️ 블로킹 / 논블로킹

<aside>
💡 제어권을 어떻게 처리하느냐?

</aside>

- 블로킹(Blocking)
    
    제어권을 넘겨준다.
    
    ![A함수가 B함수를 부르는 과정 - 블로킹](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled.png)
    
    A함수가 B함수를 부르는 과정 - 블로킹
    
- 논블로킹(Non-Blocking)
    
    제어권을 넘겨주지 않는다.
    
    ![A함수가 B함수를 부르는 과정 - 논블로킹](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%201.png)
    
    A함수가 B함수를 부르는 과정 - 논블로킹
    

## 🧞 동기 / 비동기

<aside>
💡 반환 값을 기다리느냐?

</aside>

- 동기(Synchronous)
    
    반환 값을 기다린다.
    
- 비동기(Asynchronous)
    
    반환 값을 기다리지 않는다.
    

## 🌝 시나리오

1. 동기 - 블로킹(Synchronous - Blocking)
    
    ![동기 - 블로킹(Synchronous - Blocking)](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%202.png)
    
    동기 - 블로킹(Synchronous - Blocking)
    
    반환 값을 기다리고(**동기**), 제어권을 넘겨주었다(**블로킹**).
    
    > 가장 일반적인 프로그래밍 시나리오
    > 
    - Example
        
        ```jsx
        const syncBlock = () => {
        	console.log('wait for me');
        	console.log('more!');
        	
        	return 'blah'
        }
        
        console.log('before call syncBlock');
        a = syncBlock();
        console.log(`after call syncBlock ${a}`);
        ```
        
        ![Untitled](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%203.png)
        
        > 일반적인 절차지향의 순서대로 함수가 모두 끝날 때까지 제어권을 주고(**블로킹**), 아래의 코드도 나중에 실행된다(**동기**).
        > 
2. 동기 - 논블로킹(Synchronous - Non-Blocking)
    
    ![동기 - 논블로킹(Synchronous - Non-Blocking)](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%204.png)
    
    동기 - 논블로킹(Synchronous - Non-Blocking)
    
    반환 값을 기다리지만(**동기**), 제어권은 주지 않았다(**논블로킹**).
    
    반환 값이 필요하므로 polling방식으로 B함수의 상태를 계속 확인한다.
    
    > Javascript에서는 확인 할 필요 없이 이벤트 루프가 콜스택과 태스크 큐를 통해서 관리하기 때문에 실제로 이런 구현을 한 적은 없었다.
    > 
    - Example
        
        ```jsx
        const syncNonblock = () =>
          new Promise((resolve, reject) => {
            setTimeout(() => {
              flag = true;
              resolve(`Child - done!`);
            }, 50);
          });
        
        let flag = false;
        let response = syncNonblock();
        let checkInterval = setInterval(async () => {
          if (flag) {
            clearInterval(checkInterval);
            console.log('Parent - Finally flag is on!');
            console.log(await response);
          } else {
            console.log('Parent - checking flag!');
          }
        }, 10);
        ```
        
        ![Untitled](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%205.png)
        
    
    > Javascript로는 어거지로 만들수밖에 없었다... setInterval의 콜백 함수가 Global Context가 후에 실행될 코드라고 생각하면 되고, flag가 있어야 제어권을 가지고 있다고 보면 된다.
    > 
    
    > Global Context는 syncNonblock 함수 실행 후에 자신의 코드를 실행하고(**비동기**), 함수의 반환 값을 기다리게 된다(**블로킹**).
    > 
3. 비동기 - 논블로킹(Asynchronous - Non-Blocking)
    
    ![비동기 - 논블로킹(Asynchronous - Non-Blocking)](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%206.png)
    
    비동기 - 논블로킹(Asynchronous - Non-Blocking)
    
    반환 값을 사용하는 콜백 함수를 넘겨주고(**논블로킹**), 제어권은 주지 않는다(**비동기**).
    
    > Javascript의 콜백 함수 동작 형태이다.
    > 
    - Example
        
        ```jsx
        const asyncBlock = async () => {
          console.log(`Child - I'm child!`);
        
          return `cchhiilldd`;
        };
        
        console.log('Parent - before asyncBlock');
        asyncBlock().then((data) => {
          console.log(`Parent - my child's returned data is ${data}`);
        });
        console.log('Parent - after asyncBlock');
        ```
        
        ![Untitled](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%207.png)
        
        > Javascript에서의 일반적인 콜백 함수 패턴이다.
        > 
        
        > Global Context는 제어권을 넘겨주지 않고(**비동기**), 반환 값을 사용하는 콜백 함수를 넘겨준다(**블로킹**).
        > 
4. 비동기 - 블로킹(Asynchronous - Blocking)
    
    ![비동기 - 블로킹(Asynchronous - Blocking)](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%208.png)
    
    비동기 - 블로킹(Asynchronous - Blocking)
    
    - Example
        
        ```jsx
        const syncNonblock = () =>
          new Promise((resolve, reject) => {
            setTimeout(() => {
              resolve(`Child - done!`);
            }, 50);
          });
        
        let flag = false;
        syncNonblock().then((data) => {
          console.log(`Parent - child complete! below is child's message`);
          console.log(data);
          flag = true;
        });
        let checkInterval = setInterval(async () => {
          if (flag) {
            clearInterval(checkInterval);
            console.log('Parent - Finally flag is on!');
            console.log('Parent - my job ...');
          }
        }, 10);
        ```
        
        ![Untitled](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%209.png)
        
        > 이 또한 Javascript로는 어거지로 만들 수밖에 없었다... setInterval의 콜백 함수가 Global Context가 후에 실행될 코드라고 생각하면 되고, flag가 있어야 제어권을 가지고 있다고 보면 된다.
        > 
        
        > Global Context는 제어권을 넘겨주지 않고(**비동기**), 반환 값을 사용하는 콜백 함수를 사용 후 제어권을 넘겨준다(**블로킹**).
        > 
        
        > 생각해보면 블로킹되어있기 때문에, 동기 - 블로킹(Synchronous - Blocking)과 비교해 실행 속도의 이점을 볼 수 없어서 잘 쓰이지 않는다고 한다.
        > 
        

## 🧩 참고

- 블로킹/논블로킹 - 동기/비동기
    
    [블로킹 Vs. 논블로킹, 동기 Vs. 비동기](https://velog.io/@nittre/%EB%B8%94%EB%A1%9C%ED%82%B9-Vs.-%EB%85%BC%EB%B8%94%EB%A1%9C%ED%82%B9-%EB%8F%99%EA%B8%B0-Vs.-%EB%B9%84%EB%8F%99%EA%B8%B0)
    
- Javascript - Event Loop, V8
    
    [이벤트 루프와 태스크 큐 (마이크로 태스크, 매크로 태스크)](https://velog.io/@yejineee/%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84%EC%99%80-%ED%83%9C%EC%8A%A4%ED%81%AC-%ED%81%90-%EB%A7%88%EC%9D%B4%ED%81%AC%EB%A1%9C-%ED%83%9C%EC%8A%A4%ED%81%AC-%EB%A7%A4%ED%81%AC%EB%A1%9C-%ED%83%9C%EC%8A%A4%ED%81%AC-g6f0joxx)
    
    [브라우저에서 이벤트 루프와 V8 엔진의 관계](https://velog.io/@dev-mish-mash/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%97%90%EC%84%9C-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84%EC%99%80-V8-%EC%97%94%EC%A7%84%EC%9D%98-%EA%B4%80%EA%B3%84)