# 배열(array)
***

```c

#include <stdio.h>

// 요소의 타입이 char 요소의 개수가 26개인 배열 alphabets 정의 각각의 요소를 'A'부터 'Z'까지 채우는 코드를 작성하고 출력
int main() {
	char alphabets[26];				//타입 배열명[배열길이] -> 배열을 정의하는 방법
	char a = 'A';
	for (int i = 0; i < sizeof(alphabets); i++) {
		alphabets[i] = a + i;
		printf("%c", alphabets[i]); //ABCDEFGHIJKLMNOPQRSTUVWXYZ 출력
	}
	return 0;
}
```

### 인덱스(index)

**요소(element)의 순번**

```c

#include <stdio.h>


int main() {
	
	int arr[2]; //길이가 2인 int형 배열 
	arr[0] = 1; // 인덱스 0번에 1 
	arr[1] = 2; // 인덱스 1번에 2
	printf("arr[1] : %d", arr[1]); //arr배열 1번 데이터 출력
	return 0;
}
```

### 배열 복사

```c

#include <stdio.h>


int main() {
	
	int arr1[2];
	arr1[0] = 1;
	arr1[1] = 2;

	int arr2[2];
	
	for (int i = 0; i < 2; i++) { //arr1배열의 길이는 2
		arr2[i] = arr1[i]; //배열 복사
		
	}
	printf("arr2[0] : %d\r\n", arr2[0]);
	printf("arr2[1] : %d", arr2[1]);
	return 0;
}
```

**배열은 대입 연산자를 사용하기 어려움**

```c
#include <stdio.h>


int main() {
	
	int arr1[2];
	arr1[0] = 1;
	arr1[1] = 2;

	int arr2[2];
	
	int arr1[2];
	arr1[0] = 1;
	arr1[1] = 2;

	int arr2[2] = arr1; //오류! 실행 안됨
	return 0;
}
```

