# 재귀(recursion)
***

### 재귀란
+ 어떠한 이벤트에서 자기 자신을 포함하고 다시 자기 자신을 사용하여 정의되는 것

**재귀의 대표적인 예로 factorial이 있으며 아래는 팩토리얼 함수를 간단하게 정의한 코드**

```python

def factorial(n: int) -> int:
  
  if n > 0:
      return n * factorial(n - 1)
  else:
      return 1
```

팩토리얼은 n!이며 만약 n이 5라면 5 x 4 x 3 x 2 x 1 = 120   **( n * (n - 1)! )**

#### 팩토리얼 함수 실행 순서 (n = 3 가정)

1. factorial(3)을 실행하면 factorial() 함수가 호출되고 매개변수 n에 3을 전달받아 3 * factorial(2)의 값 반환 곱셈을 하려면 factorial(2) 값을 구해야 함
2. factorial(2)을 실행하면 factorial() 함수가 호출되고 매개변수 n에 2를 전달받아 2 * factorial(1)의 값 반환 곱셈을 하려면 factorial(1) 값을 구해야 함
3. factorial(1)을 실행하면 factorial() 함수가 호출되고 매개변수 n에 1을 전달받아 1 * factorial(0)의 값 반환 곱셈을 하려면 factorial(0) 값을 구해야 함
4. factorial(0)을 실행하면 factorial() 함수가 호출되고 n이 0보다 크지 않아 1 반환 -> 반환값을 3번으로 보냄
5. 반환된 값 1을 전달받은 factorial() 함수는 1 * factorial(0) -> (1 * 1) 반환 -> 반환값 2번으로 보냄
6. 반환된 값 (1 * 1)을 전달받은 factorial() 함수는 2 * factorial(1) -> (2 * 1) 반환 -> 반환값 1번으로 보냄
7. 반환된 값 (2 * 1)를 전달받은 factorial() 함수는 3 * factorial(2) -> (3 * 2) 반환 -> factorial(3)은 3! 즉 **6**이 됨

**자신과 똑같은 함수를 호출하는 것은 재귀 호출(reursive call)이라고 함**


파이썬에서는 팩토리얼값을 구하는 표준 라이브러리로 **math 모듈에서 factorial()함수 제공**

```python

import math
print(math.factorial(3)) ## 결과 6

```
### 두 정숫값 최대 공약수 구하기

**아래는 두 정숫값의 최대공약수를 구하는 함수코드**

```python

def gcd(x: int, y: int) -> int:
    if y == 0:
        return x
    else:
        return gcd(y, x % y)
        
if __name__=='__main__':

    print('두 정숫값의 최대 공약수를 구합니다')
    x = int(input('첫 번째 정숫값을 입력하세요.: '))
    y = int(input('두 번째 정숫값을 입력하세요.: '))
    
    print(f'두 정숫값의 최대 공약수는 {gcd(x, y)}입니다.')
```
#### gcd()함수 실행 순서

1. x와 y의 정숫값 입력 (x = 24 y = 8) 가정
2. gcd(24, 8) 함수 실행  gcd(8, 0) 실행해야 함 
3. gcd(8, 0) 함수 실행 y가 0이므로 x값 8 반환
4. 두 정숫값의 최대공약수는 **8**

파이썬에서는 최대공약수를 구하는 표준 라이브러리로 **math 모듈에서 gcd()함수 제공**

```python

import math
print(math.gcd(24, 8)) # 8반환 만약 gcd(0,0)이면 0 반환
```

### 재귀 알고리즘 분석 방법

**아래 코드 참고**

```python

def recur(x: int) -> int:
    if n > 0:
        recur(n - 1)
        print(n)
        recur(n - 2)
        
x = int(input("정숫값을 입력하세요.: "))
recur(x)
```

함수 안에서 재귀 호출 2번 실행 

#### 실행 방법(recur(4) 가정)
1. recur(3) 실행
2. n의 값 4 출력
3. recur(2) 실행

#### 함수 하향식(위에서 아래로) 분석

![그래프](https://user-images.githubusercontent.com/42503786/172612239-ce5d36e0-8377-4848-b633-43acb8c28d2c.png)

1. 가장 위쪽에 있는 상자는 recur(4) 실행을 나타냄
2. recur(3)을 실행시 왼쪽 화살표를 따라가면 무엇을 하는지 알 수 있음
3. recur(2)를 실행시 오른쪽 화살표를 따라가면 무엇을 하는지 알 수 있음
4. recur(n -1) 코드에 의해 왼쪽 화살표를 따라 1칸씩 아래쪽 상자로 이동하고 조건이 맞지 않아 다시 원래 호출한 상자로 되돌아오면 상자 안의 값 출력
5. 빈 상자의 경우 아무것도 하지 않고 원래 상자로 되돌아감(조건이 안맞음)

