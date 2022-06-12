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

    def peek(self) -> Any: # 스택 들여다보기(꼭대기 값)
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
***

### 스택 프로그램 만들기
***

``` python
from enum import Enum
from fixedstack import FixedStack

Menu = Enum('Menu', ['푸시', '팝', '피크', '검색', '덤프', '종료'])

def select_menu():
    s = [f'({m.value}){m.name}'for m in Menu] #  enum 타입은 이름(name) 과 값(value) 속성을 가지고 있음
    while True:
        print(*s, sep=' ', end='') # *s -> 컨테이너 데이터 unpacking
        n = int(input(': '))
        if 1 <= n <= len(s):
            return Menu(n)

s = FixedStack(64)
while True:
    print(f'현재 데이터 개수: {len(s)} / {s.capacity}')
    menu = select_menu()

    if menu == Menu.푸시:
        x = int(input('데이터를 입력하세요: '))
        try:
            s.push(x)
        except FixedStack.Full:
            print('스택이 가득 차 있습니다.')

    elif menu == Menu.팝:
        try:
            s.pop()
        except FixedStack.Empty:
            print('스택이 비어 있습니다.')

    elif menu == Menu.피크:
        try:
            x = s.peek()
            print(f'피크한 데이터는 {x}입니다.')
        except FixedStack.Empty:
            print('스택이 비어 있습니다.')

    elif menu == Menu.검색:
        x = int(input('검색할 값을 입력하세요: '))
        if x in s:
            print(f'{s.count(x)}개 포함되고 맨 앞의 위치는 {s.find(x)}입니다.')
        else:
            print('검색 값을 찾을 수 없습니다.')

    elif menu == Menu.덤프:
        s.dump()
    
    else:
        break
```

**데이터 5개 푸시하기**

<img width="494" alt="푸시5" src="https://user-images.githubusercontent.com/42503786/173225106-4cdd930b-b529-47b4-b1e4-0e4acccc79ff.png">

**데이터 1개 팝하기**


<img width="314" alt="팝" src="https://user-images.githubusercontent.com/42503786/173225125-9c16e843-a3dd-433a-8787-585e269ba4dc.png">

**데이터 피크하기**

<img width="308" alt="피크" src="https://user-images.githubusercontent.com/42503786/173225150-5dc498ee-bf61-4225-962f-cd6230dec17c.png">

**데이터 검색하기**

<img width="319" alt="검색" src="https://user-images.githubusercontent.com/42503786/173225165-ee7a8b33-57e1-4e1d-a3db-595d14caf2ca.png">

**데이터 덤프하기**

<img width="322" alt="덤프" src="https://user-images.githubusercontent.com/42503786/173225172-57713cdb-56d4-4649-a3ad-93ed0894f225.png">

**종료하기**

<img width="304" alt="종료" src="https://user-images.githubusercontent.com/42503786/173225181-fced08f3-efe9-41af-9b58-5cbe2806cd6a.png">
