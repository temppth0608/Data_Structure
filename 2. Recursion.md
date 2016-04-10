```
최종 작성자 : 박태현
최초 작성일 : 2016년 4월 10일
마지막 수정 : 2016년 4월 10일, 박태현
```

# Recursion(재귀)
## Factorial 함수 구현
```C
int Factorial(int num) {
	if (num == 1)
		return 1;
	else
		return num * Factorial(num - 1);
}
```

## Fibonacci Sequence
```C
int Fibo(int num) {
	if (num == 1)
		return 0;
	else if (num == 2)
		return 1;
	else
		return Fibo(num - 1) + Fibo(num - 2)
}
```

## Binary Search(재귀로 구현)
```C
int BSearchRecur(int ar[], int len, int first, int last, int target) {
	int mid;
	if (first > last)
		return -1;
	mid = (first + last) / 2;
	if (ar[mid] == target)
		return mid;
	else if (ar[mid] > target)
		BSearchRecur(ar, len, first, mid - 1, target);
	else BSearchRecur(ar, len, mid + 1, last, target);
}
```

## 하노이의 타워
```C
void HanoiTowerMove(int num, char from, char by, char to) {
	if (num == 1) {
		printf("원반 1을 %c에서 %c로 이동 \n", from, to)
	} else {
		HanoiTowerMove(num - 1, from, to, by);
		printf("원반 %d를 %c에서 %c로 이동 \n", num, from, to)
		HanoiTowerMove(num - 1, by, from, to);
	}
}
```
