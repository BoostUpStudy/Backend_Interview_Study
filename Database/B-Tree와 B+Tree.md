# B-Tree와 B+Tree



# B-Tree

트리 자료구조의 일종으로, 이진 트리를 확장해 하나의 노드가 가질 수 있는 자식 노드의 수가 2이상인 트리 구조이다.

**최상위 노드**를 `root`노드라고 하며, **최하위 노드**들을 `leaf`노드라고 한다. **그 사이 계층의 노드**들은 `internal`노드라고 부른다.

![Untitled](https://user-images.githubusercontent.com/58130501/147547163-dd7f4029-f5dc-4c89-ad59-2563144a1bdf.png)

하나의 노드에 여러 개의 데이터가 있을 수 있다.

데이터의 순서는 이진 탐색 트리와 유사하다.

노드 내 데이터를 최대 M-1개, 최소 [M/2]-1개를 가지는 B-Tree를 **M차 B-Tree**라고 부른다.

자식 노드의 최소 및 최대 수는 특별한 구현에 대해서 결정되어 있다.

노드의 단위는 **page**로, **하드디스크의 저장 단위**에 맞추어져 있어 데이터베이스와 파일시스템에서 잘 쓰인다.



## 규칙

- root 노드는 **2개 이상**의 자식을 가져야 한다.
- M차 B-Tree는 루트 노드를 제외한 나머지 노드는 **최소 M/2개, 최대 M개의 자식 노드**가 있어야 한다.
- **N개의 데이터**가 있는 하나의 노드는 **N+1개의 자식노드**를 갖고 있다.
  
    ⇒ **N개의 데이터**가 있다면 **자식 노드의 포인터는 N+1개**이다.
    
    ![Untitled 1](https://user-images.githubusercontent.com/58130501/147547208-176f996f-19aa-4654-be56-e2af12c47f7c.png)
    

## 탐색

1. 노드 안에서: 순차검색

2. 트리 안에서: 하향식 트리 검색

   

## 삽입

1. 삽입될 위치 검색
2. 삽입
    1. 노드의 공간이 남아있을 때
       
        노드 안에서 오름차순으로 삽입
        
    2. 노드의 공간이 없을 때
        1. 오름차순으로 삽입
        2. 노드안에서 중앙값으로 분할하여 중앙값의 데이터를 부모 노드로 오름차순으로 삽입
        3. i~ii 과정을 `root`노드까지 반복
        
        ex) 최대 2개의 데이터를 가지는 2차 B-Tree
        
        ![Untitled 2](https://user-images.githubusercontent.com/58130501/147547241-c850a65c-eb87-4ad6-96f4-7c45ecc8cc82.png)
        
        1. 4 삽입
           
            ![Untitled 3](https://user-images.githubusercontent.com/58130501/147547275-607bdab5-0d2c-43ca-a1f8-47e9a8e6123c.png)
            
        2. 노드 중앙값 분할
           
            ![Untitled 4](https://user-images.githubusercontent.com/58130501/147547301-03ab31d3-083c-4750-914a-89c96ca31164.png)
            
        3. root노드 중앙값 분할
           
            ![Untitled 5](https://user-images.githubusercontent.com/58130501/147547318-f8bc6afa-8b78-4465-b678-9003036ee6fe.png)
            

## 삭제

1. 삭제할 데이터가 위치한 노드 검색

    1. 삭제할 데이터가 leaf노드에 있는 경우
        1. 현재 노드의 데이터 개수가 최소 개수보다 클 때
           
            삭제
            
        2. 현재 노드의 데이터 개수가 최소 개수일 때
           
            1) 왼쪽 또는 오른쪽 형제노드의 데이터 개수가 최소 개수 이상일때
            
            a) 현재노드를 현재노드와 형제노드 사이의 부모노드 데이터로 교체
            
            b) 형제노드가 왼쪽이라면 최대값을, 오른쪽이라면 최소값을 부모노드 데이터와 교체
            
            2) 부모노드의 데이터는 최소 개수보다 많고, 형제노드 모두 데이터 개수가 최소 개수일 때
            
            a) 현재노드 삭제
            
            b) 부모노드의 데이터 최대값 또는 최소값을 형제노드와 합친다.
            
            3) 부모노드, 형제노드 모두 데이터 개수가 최소 개수일 때
            
            a) 현재노드 삭제
            
            b) 부모노드를 인접한 형제노드와 병합 후 조상노드의 자식으로 위치시킨다.
            
            i) B-Tree의 조건이 맞춰줄 때까지 반복
        
    2. 삭제할 데이터가 leaf노드에 없는 경우
        1. 현재노드와 자식노드의 데이터 개수가 최소 개수보다 클 때
           
            1) 왼쪽 서브트리의 최댓값과 위치를 변경한다.
            
            2) 왼쪽 서브트리의 최댓값과 변경된 데이터를 삭제한다.
            
            3) a. 과정을 한다.
            
        2. 현재노드와 자식노드 모두 데이터 개수가 최소 개수일 경우
           
            1. 데이터를 삭제하고 양쪽 자식노드를 합친다.
            
            2. 부모의 데이터를 인접한 형제노드에 붙이고, 1)에서 합쳤던 노드를 자식노드로 위치시킨다.
            
               
            

## 특징

모든 노드에 key와 data가 들어있다.

데이터를 정렬된 상태로 보관

상향식 구성

삽입과 삭제시 균형을 유지하기 위한 작업

동일한 높이의 leaf노드 (Balanced)

O(logN) 검색시간 보장



# B+Tree

B-Tree에서 확장된 개념의 트리구조이다. 

leaf노드에만 key와 data를 저장하고, 나머지 노드에는 key만 담겨있다. leaf노드끼리는 linked list로 연결되어 있다.

![Untitled 6](https://user-images.githubusercontent.com/58130501/147547350-c0eee6f8-e884-4768-9e29-4b98037ca34b.png)



## 삽입

- 삽입할 노드의 데이터 개수가 최대값보다 작을 때

데이터 삽입

- 삽입할 노드의 데이터 개수가 최대값일 때
  
    2개로 분할하여 중간값을 부모노드에 추가
    
    - 부모노드의 데이터 개수가 최대값일 때
      
        B-Tree 삽입 과정과 동일
        
        
    

## 삭제

- 삭제할 키가 노드의 첫번째 데이터가 아닐 때

데이터 삭제

- 삭제할 키가 노드의 첫번째 데이터일 때
    - 노드의 데이터 개수가 최소값이 아닐 때
      
        삭제 후 삭제된 key가 있던 노드의 key값을 오른쪽 key로 변경한다.
        
    - 노드의 데이터 개수가 최소값일 때
        - 형제노드의 데이터 개수가 최소값이 아닐 때
          
            삭제 후 인접한 형제노드의 key와 자리를 바꾼 후 부모노드의 key를 알맞게 수정한다.
            
        - 형제노드의 데이터 개수가 최소값일 때
            - 부모노드의 데이터 개수가 최소값이 아닐 때
              
                삭제 후 삭제된 key가 있던 노드의 key 삭제
                
            - 부모노드의 데이터 개수가 최소값일 때
              
                현재노드와 부모노드 삭제 후 조상노드에 형제노드를 연결하고 조상노드에 대해서는 B-Tree와 동일
                
                

## 장점

오직 leaf노드에만 데이터를 담기 때문에 저장공간을 더 확보하고 더 많은 key들을 수용할 수 있다. 하나의 노드에 더 많은 key를 담을 수 있기 때문에 트리의 높이가 더 낮아진다.

leaf노드끼리 서로 연결되어 있기 때문에 범위 검색에 유리하다.

풀 스캔 시, B+Tree는 leaf노드로 한 번의 선형탐색만 하면 되기 때문에 B-Tree보다 빠르다.

→데이터베이스 시스템 인덱스 구성에 매우 효율적이다.



## 단점

B-Tree의 경우 최상의 경우 특정 key의 데이터를 찾기 위해 leaf노드까지 가지 않아도 되지만, B+Tree의 경우 반드시 특정 key에 접근하기 위해서 leaf node까지 가야 한다.



---

- 참고자료
  
    [https://ko.wikipedia.org/wiki/B_트리](https://ko.wikipedia.org/wiki/B_%ED%8A%B8%EB%A6%AC)
    
    [https://velog.io/@emplam27/자료구조-그림으로-알아보는-B-Tree](https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Tree)
    
    [https://velog.io/@emplam27/자료구조-그림으로-알아보는-B-Plus-Tree](https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Plus-Tree)
    
    [https://slenderankle.tistory.com/159](https://slenderankle.tistory.com/159)
    
    [https://rebro.kr/167](https://rebro.kr/167)