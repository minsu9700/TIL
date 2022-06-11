# 스택 클래스 정의하고 속성 집어 넣기
***
### 스택(stack)

1. 데이터를 임시 저장하는 기본 자료구조
2. **LIFO(Last In First Out)** 방식
3. 스택에서 데이터를 집어 넣는 작업을 **push** 라 함
4. 스택에서 데이터를 꺼내는 작업을 **pop** 이라 함
5. 푸시하고 팝하는 윗부분을 **꼭대기(top)** 이라 함
6. 아랫부분을 **바닥(bottom)**이라 함

***

### 스택 고정 크기 클래스 구현

```python

from typing import Any

class FixedStack:

    class Empty(Exception): #스택이 비어있을 때 예외처리 클래스
        pass
    
    class Full(Exception): #스택이 가득 차 있을 때 예외처리 클래스
        pass

    def __init__(self, capacity: int) -> None: # 클래스를 생성할 때 초기화
        self.stk = [None] * capacity # 스택 변수와 크기 정의
        self.capacity = capacity #
        self.ptr = 0 #포인터 지정

    def __len__(self) -> int:
        return self.ptr #스택에 쌓여있는 데이터 개수 반환

    def is_empty(self) -> bool:
        return self.ptr <= 0 # ptr이 0보다 작거나 같을 때 스택이 비워져있다는 것을 알 수 있음

    def is_full(self) -> bool:
        return self.ptr >= self.capacity # ptr이 capacity 보다 크거나 같을 때 스택이 가득 찬 것을 알 수 있음

    def push(self, value: Any) -> None:
        if self.is_full():
            raise FixedStack.Full #스택이 가득 차 있을 때 예외처리 클래스 호출
        
        self.stk[self.ptr] = value  #스택에 데이터 집어넣기
        self.ptr += 1               # 포인터 1증가

    def pop(self) -> Any:
        if self.is_empty():
            raise FixedStack.Empty #스택이 비워있을 때 예외처리 클래스 호출` 

        self.ptr -= 1 # 현재 포인터 위치에서 1 빼주기 그래야 스택 꼭대기 값 반환 가능
        return self.stk[self.ptr]    # 스택 꼭대기 값 반환

    def peek(self, value: Any) -> Any: # 스택 들여다보기(꼭대기 값)
        if self.is_empty():
            raise FixedStack.Empty #스택이 비워있을 때 예외처리 클래스 호출

        return self.stk[self.ptr - 1] #스택 꼭대기 값 반환

    def find(self, value: Any) -> Any: #데이터 인덱스 값 찾기
        if self.is_empty():
            raise FixedStack.Empty #스택이 비워있을 때 예외처리 클래스 호출
        
        for i in range(self.ptr -1, -1, -1):
            if self.stk[i] == value: #스택 index에 있는 데이터가 일치하면 그 위치 index 반환
                return i
            return -1

    def count(self, value: Any) -> int: # 데이터 개수 세기
        c = 0 #개수 초기화
        for i in range(self.ptr):
            if self.stk[i] == value:
                c += 1
        return c

    def __contains__(self, value: Any) -> bool: #데이터 포함되어 있는지 확인유무
        return self.count(value) > 0

    def dump(self) -> None: # 스택에 있는 데이터 출력
        if self.is_empty():
            raise FixedStack.Empty
        else:
            print(self.stk[:self.ptr]) 

    def clear(self) -> None: #스택 초기화
        self.ptr = 0
```
