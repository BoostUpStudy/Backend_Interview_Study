# Blocking & Non-Blocking - Synchronous & Asynchronous

## ๐ย ์ฉ์ด ์ ๋ฆฌ

- ์ ์ด๊ถ: ์ฝ๋๋ฅผ ์คํํ  ๊ถ๋ฆฌ
    
    > ์ ์ด๊ถ์ ๊ฐ์ง Context๋ ์์ ์ ์คํํ ํ, ๋ถ๋ชจ(์์ ์ ํธ์ถํ) Context๋ก ์ ์ด๊ถ์ ๋๋ ค์ค๋ค.
    > 

## ๐งโโ๏ธย ๋ธ๋กํน / ๋ผ๋ธ๋กํน

<aside>
๐ก ์ ์ด๊ถ์ ์ด๋ป๊ฒ ์ฒ๋ฆฌํ๋๋?

</aside>

- ๋ธ๋กํน(Blocking)
    
    ์ ์ด๊ถ์ ๋๊ฒจ์ค๋ค.
    
    ![Aํจ์๊ฐ Bํจ์๋ฅผ ๋ถ๋ฅด๋ ๊ณผ์  - ๋ธ๋กํน](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled.png)
    
    Aํจ์๊ฐ Bํจ์๋ฅผ ๋ถ๋ฅด๋ ๊ณผ์  - ๋ธ๋กํน
    
- ๋ผ๋ธ๋กํน(Non-Blocking)
    
    ์ ์ด๊ถ์ ๋๊ฒจ์ฃผ์ง ์๋๋ค.
    
    ![Aํจ์๊ฐ Bํจ์๋ฅผ ๋ถ๋ฅด๋ ๊ณผ์  - ๋ผ๋ธ๋กํน](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%201.png)
    
    Aํจ์๊ฐ Bํจ์๋ฅผ ๋ถ๋ฅด๋ ๊ณผ์  - ๋ผ๋ธ๋กํน
    

## ๐งย ๋๊ธฐ / ๋น๋๊ธฐ

<aside>
๐ก ๋ฐํ ๊ฐ์ ๊ธฐ๋ค๋ฆฌ๋๋?

</aside>

- ๋๊ธฐ(Synchronous)
    
    ๋ฐํ ๊ฐ์ ๊ธฐ๋ค๋ฆฐ๋ค.
    
- ๋น๋๊ธฐ(Asynchronous)
    
    ๋ฐํ ๊ฐ์ ๊ธฐ๋ค๋ฆฌ์ง ์๋๋ค.
    

## ๐ย ์๋๋ฆฌ์ค

1. ๋๊ธฐ - ๋ธ๋กํน(Synchronous - Blocking)
    
    ![๋๊ธฐ - ๋ธ๋กํน(Synchronous - Blocking)](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%202.png)
    
    ๋๊ธฐ - ๋ธ๋กํน(Synchronous - Blocking)
    
    ๋ฐํ ๊ฐ์ ๊ธฐ๋ค๋ฆฌ๊ณ (**๋๊ธฐ**), ์ ์ด๊ถ์ ๋๊ฒจ์ฃผ์๋ค(**๋ธ๋กํน**).
    
    > ๊ฐ์ฅ ์ผ๋ฐ์ ์ธ ํ๋ก๊ทธ๋๋ฐ ์๋๋ฆฌ์ค
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
        
        > ์ผ๋ฐ์ ์ธ ์ ์ฐจ์งํฅ์ ์์๋๋ก ํจ์๊ฐ ๋ชจ๋ ๋๋  ๋๊น์ง ์ ์ด๊ถ์ ์ฃผ๊ณ (**๋ธ๋กํน**), ์๋์ ์ฝ๋๋ ๋์ค์ ์คํ๋๋ค(**๋๊ธฐ**).
        > 
2. ๋๊ธฐ - ๋ผ๋ธ๋กํน(Synchronous - Non-Blocking)
    
    ![๋๊ธฐ - ๋ผ๋ธ๋กํน(Synchronous - Non-Blocking)](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%204.png)
    
    ๋๊ธฐ - ๋ผ๋ธ๋กํน(Synchronous - Non-Blocking)
    
    ๋ฐํ ๊ฐ์ ๊ธฐ๋ค๋ฆฌ์ง๋ง(**๋๊ธฐ**), ์ ์ด๊ถ์ ์ฃผ์ง ์์๋ค(**๋ผ๋ธ๋กํน**).
    
    ๋ฐํ ๊ฐ์ด ํ์ํ๋ฏ๋ก polling๋ฐฉ์์ผ๋ก Bํจ์์ ์ํ๋ฅผ ๊ณ์ ํ์ธํ๋ค.
    
    > Javascript์์๋ ํ์ธ ํ  ํ์ ์์ด ์ด๋ฒคํธ ๋ฃจํ๊ฐ ์ฝ์คํ๊ณผ ํ์คํฌ ํ๋ฅผ ํตํด์ ๊ด๋ฆฌํ๊ธฐ ๋๋ฌธ์ ์ค์ ๋ก ์ด๋ฐ ๊ตฌํ์ ํ ์ ์ ์์๋ค.
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
        
    
    > Javascript๋ก๋ ์ด๊ฑฐ์ง๋ก ๋ง๋ค์๋ฐ์ ์์๋ค... setInterval์ ์ฝ๋ฐฑ ํจ์๊ฐ Global Context๊ฐ ํ์ ์คํ๋  ์ฝ๋๋ผ๊ณ  ์๊ฐํ๋ฉด ๋๊ณ , flag๊ฐ ์์ด์ผ ์ ์ด๊ถ์ ๊ฐ์ง๊ณ  ์๋ค๊ณ  ๋ณด๋ฉด ๋๋ค.
    > 
    
    > Global Context๋ syncNonblock ํจ์ ์คํ ํ์ ์์ ์ ์ฝ๋๋ฅผ ์คํํ๊ณ (**๋น๋๊ธฐ**), ํจ์์ ๋ฐํ ๊ฐ์ ๊ธฐ๋ค๋ฆฌ๊ฒ ๋๋ค(**๋ธ๋กํน**).
    > 
3. ๋น๋๊ธฐ - ๋ผ๋ธ๋กํน(Asynchronous - Non-Blocking)
    
    ![๋น๋๊ธฐ - ๋ผ๋ธ๋กํน(Asynchronous - Non-Blocking)](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%206.png)
    
    ๋น๋๊ธฐ - ๋ผ๋ธ๋กํน(Asynchronous - Non-Blocking)
    
    ๋ฐํ ๊ฐ์ ์ฌ์ฉํ๋ ์ฝ๋ฐฑ ํจ์๋ฅผ ๋๊ฒจ์ฃผ๊ณ (**๋ผ๋ธ๋กํน**), ์ ์ด๊ถ์ ์ฃผ์ง ์๋๋ค(**๋น๋๊ธฐ**).
    
    > Javascript์ ์ฝ๋ฐฑ ํจ์ ๋์ ํํ์ด๋ค.
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
        
        > Javascript์์์ ์ผ๋ฐ์ ์ธ ์ฝ๋ฐฑ ํจ์ ํจํด์ด๋ค.
        > 
        
        > Global Context๋ ์ ์ด๊ถ์ ๋๊ฒจ์ฃผ์ง ์๊ณ (**๋น๋๊ธฐ**), ๋ฐํ ๊ฐ์ ์ฌ์ฉํ๋ ์ฝ๋ฐฑ ํจ์๋ฅผ ๋๊ฒจ์ค๋ค(**๋ธ๋กํน**).
        > 
4. ๋น๋๊ธฐ - ๋ธ๋กํน(Asynchronous - Blocking)
    
    ![๋น๋๊ธฐ - ๋ธ๋กํน(Asynchronous - Blocking)](Blocking%20&%20Non-Blocking%20-%20Synchronous%20&%20Asynchrono%209f3213ff70fc47edaf8749c28974a713/Untitled%208.png)
    
    ๋น๋๊ธฐ - ๋ธ๋กํน(Asynchronous - Blocking)
    
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
        
        > ์ด ๋ํ Javascript๋ก๋ ์ด๊ฑฐ์ง๋ก ๋ง๋ค ์๋ฐ์ ์์๋ค... setInterval์ ์ฝ๋ฐฑ ํจ์๊ฐ Global Context๊ฐ ํ์ ์คํ๋  ์ฝ๋๋ผ๊ณ  ์๊ฐํ๋ฉด ๋๊ณ , flag๊ฐ ์์ด์ผ ์ ์ด๊ถ์ ๊ฐ์ง๊ณ  ์๋ค๊ณ  ๋ณด๋ฉด ๋๋ค.
        > 
        
        > Global Context๋ ์ ์ด๊ถ์ ๋๊ฒจ์ฃผ์ง ์๊ณ (**๋น๋๊ธฐ**), ๋ฐํ ๊ฐ์ ์ฌ์ฉํ๋ ์ฝ๋ฐฑ ํจ์๋ฅผ ์ฌ์ฉ ํ ์ ์ด๊ถ์ ๋๊ฒจ์ค๋ค(**๋ธ๋กํน**).
        > 
        
        > ์๊ฐํด๋ณด๋ฉด ๋ธ๋กํน๋์ด์๊ธฐ ๋๋ฌธ์, ๋๊ธฐ - ๋ธ๋กํน(Synchronous - Blocking)๊ณผ ๋น๊ตํด ์คํ ์๋์ ์ด์ ์ ๋ณผ ์ ์์ด์ ์ ์ฐ์ด์ง ์๋๋ค๊ณ  ํ๋ค.
        > 
        

## ๐งฉย ์ฐธ๊ณ 

- ๋ธ๋กํน/๋ผ๋ธ๋กํน - ๋๊ธฐ/๋น๋๊ธฐ
    
    [๋ธ๋กํน Vs. ๋ผ๋ธ๋กํน, ๋๊ธฐ Vs. ๋น๋๊ธฐ](https://velog.io/@nittre/%EB%B8%94%EB%A1%9C%ED%82%B9-Vs.-%EB%85%BC%EB%B8%94%EB%A1%9C%ED%82%B9-%EB%8F%99%EA%B8%B0-Vs.-%EB%B9%84%EB%8F%99%EA%B8%B0)
    
- Javascript - Event Loop, V8
    
    [์ด๋ฒคํธ ๋ฃจํ์ ํ์คํฌ ํ (๋ง์ดํฌ๋ก ํ์คํฌ, ๋งคํฌ๋ก ํ์คํฌ)](https://velog.io/@yejineee/%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84%EC%99%80-%ED%83%9C%EC%8A%A4%ED%81%AC-%ED%81%90-%EB%A7%88%EC%9D%B4%ED%81%AC%EB%A1%9C-%ED%83%9C%EC%8A%A4%ED%81%AC-%EB%A7%A4%ED%81%AC%EB%A1%9C-%ED%83%9C%EC%8A%A4%ED%81%AC-g6f0joxx)
    
    [๋ธ๋ผ์ฐ์ ์์ ์ด๋ฒคํธ ๋ฃจํ์ V8 ์์ง์ ๊ด๊ณ](https://velog.io/@dev-mish-mash/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%97%90%EC%84%9C-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84%EC%99%80-V8-%EC%97%94%EC%A7%84%EC%9D%98-%EA%B4%80%EA%B3%84)