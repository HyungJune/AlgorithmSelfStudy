#### Single Number 
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명  
nil이 아닌 정수의 배열이 입력값으로 들어오고, 그안의 하나의 원소만 빼고 모든 원소가 두번씩 반복됨. 반복되지 않는 하나의 원소를 찾는 문제.

## 예시와 조건
```
Input: [2, 2, 1]
Output: 1
```
```
Input: [4, 1, 2, 1, 2]
Output: 4
```
- 시간복잡도는 O(n), 공간복잡도는 O(1)로 할 수 있겠니

## 솔루션
- 입력값 nums를 range문으로 순회하면서 검사
- 해쉬맵에 nums의 값을 키값으로, 반복되는 횟수를 밸류값으로 저장
- 해쉬맵에서 밸류가 1인 키값을 찾아서 리턴
```
func singleNumber(nums []int) int {
	tmpmap := make(map[int]int)
	for _, num := range nums {
		if val, exists := tmpmap[num]; exists {
			tmpmap[num] = val + 1
		} else {
			tmpmap[num] = 1
		}
	}

	var result int
	for key, val := range tmpmap {
		if val == 1 {
			result = key
		}
	}
	return result
}
```

## 제출결과
- 통과는 됐는데 시간복잡도는 O(n)이지만 공간복잡도도 O(n)

## LeetCode 솔루션 참고 내용
- 수학적 연산으로도 해결 가능
- 2*(a+b+c)-(a+a+b+b+c)=c
```
func singleNumber(nums []int) int {
	tmpmap := make(map[int]int)
	dupval := 0
	notdupval := 0
	for _, num := range nums {
		if _, exists := tmpmap[num]; !exists {
			tmpmap[num] = 0
			dupval += num
		}
		notdupval += num
	}
	return 2*dupval - notdupval
}
```
- XOR 연산을 하면 공간복잡도도 O(1)로 줄일수 있다고함
```
func singleNumber(nums []int) int {
	var result int
	for _, num := range nums {
		result ^= num
	}
	return result
}
```
