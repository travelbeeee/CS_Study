## Quick Sort

### 소개 

불안정 정렬

분할 정복 방법

평균적으로 O(NlogN)의 빠른 수행 속도  

### 과정

1. 정렬할 리스트에서 임의의 원소를 골라 pivot으로 설정한다. 
2. pivot을 기준으로 왼쪽에는 pivot보다 작은 원소들, 오른쪽에는 pivot보다 큰 원소들이 오도록 교환한다. 
3. pivot을 기준으로 분할된 왼쪽/오른쪽 리스트에 대해 리스트의 크기가 0이 될 때까지 재귀적으로 반복한다. 

** pivot을 어떤것으로 정하느냐에 따라 성능이 많이 좌우된다. 중간값을 pivot으로 정하는 것이 좋다. 

### 수도 코드

```pseudocode
QuickSort (Arr, left, right) {
	if left < right:
		pivot_idx = Partion(Arr, left, right)
		QuickSort(Arr, left, pivot_idx - 1)
		QuickSort(Arr, pivot_idx + 1, right)
}

Partion (Arr, left, right){
	low = left + 1
	high = right
	pivot = Arr[left] // 제일 왼쪽원소를 pivot으로 설정

	while (low < high):
		while (Arr[low] < pivot): low++
		while (Arr[high] > pivot): high--
		if (low <= high): SWAP(Arr[low], Arr[high])
	SWAP(pivot, A[high])
	return high // pivot 위치 반환 
}
```

![image-20211015180414268](../Bada/images/QuickSort_1.png)

