# Queue
***

**큐에 데이터를 추가하는 작업을 enqueue라고 함**

**큐에 데이터를 꺼내는 작업을 dequeue라고 함**

**데이터를 꺼내는 쪽을 front라고 함**

**데이터를 넣는 쪽을 rear라고 함**

**큐에 쌓여있는 데이터 개수(int)**

***

```python

from typing import Any

class FixedQueue:

    class Empty(Exception): #배열이 비었을 때 예외 처리 클래스
        pass

    class Full(Exception): #배열이 가득 찼을 때 예외 처리 클래스
        pass

    def __init__(self, capacity: int) -> None:
        self.no = 0 # 데이터 개수
        self.rear = 0 #데이터를 넣는 부분
        self.front = 0 #데이터를 꺼내는 부분
        self.capacity = capacity # 리스트 크기 지정 
        self.que = [None] * capacity # 리스트 크기 초기화

    def __len__(self) -> int:
        return self.no #데이터 개수가 배열의 길이

    def is_empty(self) -> bool: #큐가 비었는지 참 거짓 판별
        return self.no <= 0

    def is_full(self) -> bool: #큐가 가득찼는지 참 거짓 판별
        return self.no >= self.capacity

    def enque(self, value: Any) -> None:
        if is_full():
            raise FixedQueue.Full() # 큐가 가득 찼을 때 예외 처리 발생
        self.que[self.rear] = value
        self.rear += 1
        self.no += 1
        if self.rear == self.capacity: #데이터를 넣는 rear 값은 capacity 값을 넘을 수 없음 만약 같다면 rear 값 0 초기화
            self.rear = 0
    
    def deque(self) -> int:
        if is_empty():
            raise FixedQueue.Empty() # 큐가 비었을 때 예외 처리 발생
        x = self.que[self.front]
        self.front += 1
        self.no -= 1
        if self.front == self.capacity: #데이터를 꺼내는 front 값은 capacity 값을 넘을 수 없음 만약 같다면 front 값 0 초기화
            self.front = 0
        return x
    
    def peek(self) -> int:              # 꺼내야 할 데이터 값 검색
        if is_empty():
            raise FixedQueue.Empty      # 큐가 비었을 때 예외 처리 발생
        return self.que[self.front]

    def find(self, value: Any) -> int:  # 큐에서 value를 찾아 idx를 반환하는 함수 없으면 -1 반환
        for i in range(self.no):
            idx = (i + self.front) % self.capacity
            if self.que[idx] == value:
                return idx
        return -1

    def count(self, value: Any) -> int: # 큐에 있는 value 개수 반환
        c = 0
        for i in range(self.no):
            idx = (i + self.front) % self.capacity
            if self.que[idx] == value:
                c += 1
        return c

    def __contain__(self, value: Any) -> bool: # 큐에 value가 있는지 판단 
        return self.count(value)

    def clear(self) -> None:       # 큐의 모든 데이터 비움
        self.no = self.rear = self.front = 0

    def dump(self) -> None:         # 큐에 있는 모든 데이터 앞에서 부터 끝가지 출력
        if is_empty():
            print('값이 비었습니다')
        else:
            for i in range(self.no):
                print(self.que[(i + self.front) % self.capacity], end='')
            print()
  ```
  
