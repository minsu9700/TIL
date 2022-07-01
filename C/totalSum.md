#  1부터 n까지의 정수 합 구하기
***

```c

#include <stdio.h>
#define _CRT_SECURE_NO_WARNINGS

int main(void) {

	int i, n;
	int sum;
	puts("1부터 n까지의 합을 구합니다.");
	printf("n의 값 : ");
	scanf_s	("%d", &n);
	sum = 0;
	i = 1;
	while (i <= n) {	/*i가 n이하이면 참*/
		sum += i;	
		i++;
	}
	printf("1부터 %d까지의 합은 %d입니다.\n", n, sum);
	return 0;
}
```

**puts()와 printf()의 차이는 puts()는 단순 문자열을 출력하는데 비하면 printf()는 문자열뿐만 아니라 정수, 실수, 문자 출력이 가능하다**

**scanf와 scanf_s의 차이는 scanf는 지정된 버퍼의 크기보다 더 많은 양의 문자를 넣을 수 있지만 scanf_s는 그렇지 못한다(버퍼오퍼플로우 방지)**
***

# n이 7이면 1 + 2 + 3 + 4 + 5 + 6 + 7 = 28로 출력해보기
***

```c
#include <stdio.h>
#define _CRT_SECURE_NO_WARNINGS

int main(void) {

	int i, n, sum;
	puts("1부터 n까지의 합을 구합니다.");
	printf("n의 값 : ");
	scanf_s("%d", &n);
	sum = 0;
	for (i = 1; i <= n; i++) {
		sum += i;
		
		if (i == n)
			printf("%d = %d\n", i, sum);
		else
			printf("%d + ", i);
		
	}
	
	return 0;
}
```

