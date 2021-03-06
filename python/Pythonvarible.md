# 파이썬 변수
***

**파이썬에는 데이터, 함수, 클래스, 모듈, 패키지 등을 모두 객체(object)로 취급**

**객체는 자료형(data type)을 가지며 메모리를 차지함**

**따라서 파이썬의 변수는 값을 갖지 않는 특징이 있음**
***

### 변수는 객체를 참조하는 객체에 연결된 이름에 불과함
### 모든 객체는 메모리를 차지하고, 자료형뿐만 아니라 식별 번호(identity)를 가짐

**변수는 객체를 참조하는 객체에 연결된 이름에 불과하다? 아래의 그림을 보자**


![변수](https://user-images.githubusercontent.com/42503786/173063207-27327e53-a2de-4768-8fe0-a500d2f22cda.png)

**이 그림은 객체 22를 n으로 참조함 자료형은 int형이며 메모리를 차지하고 있음**
***

### 식별번호 id() 이용하기

```python

n = 22
print(id(22)) # 자료형 22의 id(식별번호) 출력 -> 결과 : 2425313952656
print(id(n)) # n의 식별번호 출력 -> 결과 : 2425313952656

```

**여기서 알 수 있는 것은 파이썬의 대입 연산자는 값을 복사하지 않음 값 22 int형 객체를 참조하는 n이라는 이름 결합**

![아님](https://user-images.githubusercontent.com/42503786/173064157-f7b58c25-a8ad-4e0a-808b-2c93d2aa3d64.png)
***

### 함수 내외부에서 정의한 변수와 객체 식별 번호 출력

```python

n = 1
def make_id():

    x = 1
    print(f'id(x) = {id(x)}') # 값 1을 참조하는 x 식별번호 출력 -> 결과 : 2317573882096

print(f'id(1) = {id(1)}') # 값 1 객체 식별번호 출력 -> 결과 :  2317573882096
print(f'id(n) = {id(n)}') # 값 1를 참조하는 n 식별번호 출력 -> 결과 :  2317573882096

make_id() #make_id() 함수 실행
```

**아래 그림을 통해 쉽게 이해 할 수 있음**

![함수](https://user-images.githubusercontent.com/42503786/173065357-bca382be-1562-473f-be4e-51154d2001ac.png)
