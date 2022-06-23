# 정렬(sorting)
***

**정렬 : 키를 항목값의 대소 관계에 따라 데이터 집합을 일정한 순서로 바꾸어 늘어놓는 작업**
**정렬 알고리즘은 안정적인(stable) 알고리즘과 그렇지 않은 알고리즘으로 나눌 수 있음**
***

#### 시퀀스(sequence)
**시퀀스는 데이터 순서(번호)를 붙여 나열(정렬되있지 않은 것)한 것(순서대로 요소(element)를 가리킬 수 있음**
**시퀀스 특징은 다음과 같음**

* 데이터를 순서대로 하나씩 나열하여 나타낸 데이터 구조
* 특정 위치(~번째 index)의 데이터를 가리킬 수 있음
* 리스트(list), 튜플(tuple), 레인지(range), 문자열(string) 컬렉션이 있음

  


#### 내부 정렬과 외부정렬

**내부 정렬: 정렬할 모든 데이터를 하나의 배열에 저장할 수 있는 경우에 사용하는 알고리즘**
**외부 정렬: 정렬할 데이터가 많아서 하나의 배열에 저장할 수 없는 경우에 사용하는 알고리즘**

### 버블 정렬(bubble sort)

**이웃한 두 원소의 대소 관계를 비교해 필요에 따라 교환을 반복하는 알고리즘**
**원소 수가 n개인 배열에서 n - 1번 비교, 교환을 하는 과정을 패스(pass)라고 함**

```python

from typing import MutableSequence

def bubble_sort(a: MutableSequence) -> None:        #원소를 정렬할 함수 선언 매개변수에는 MutableSequence collection(원소값 변경 가능)이 들어감

    n = len(a)                                      #sequence 길이 선언
    for i in range(n - 1):                          # 배열의 맨 끝에서 맨 앞을 향해 스캔
        for j in range(n -1, i, -1):    
            if a[j - 1] > a[j]:                     
                a[j - 1], a[j] = a[j], a[j - 1]


if __name__=='__main__':
    print("버블 정렬을 수행합니다.")
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] *num

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))
    
    bubble_sort(x)

    print("오름 차순으로 정렬했습니다.")
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
        
  ```
  **버블 정렬은 1칸 이상 떨어져 있는 원소를 교환하는 것이 아닌 서로 이웃한 원소만 교환(안정적)**
  
  
