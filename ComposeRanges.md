### Integer to Roman
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
중복되지 않은 요소들을 포함한 정렬된 integer 배열에 대해서 해당 배열이 담고 있는 숫자 범위에 대한 요약을 출력하는 알고리즘을 구현하는 문제입니다.   
예)
```
nums = [-1, 0, 1, 2, 6, 7, 9]에 대해서
composeRanges(nums) = ["-1->2", "6->7", "9"]
```
* * *
### Solution
#### my solution
```go
func composeRanges(nums []int) []string {
	start := 0
	result := []string{}
	for i := 0; i < len(nums); i++ {
		if i+1 < len(nums) && nums[i]+1 == nums[i+1] {
			continue
		}

		if start == i {
			result = append(result, strconv.Itoa(nums[i]))
			start = i + 1
			continue
		}
		rangeResult := strconv.Itoa(nums[start]) + "->" + strconv.Itoa(nums[i])
		result = append(result, rangeResult)
		start = i + 1
	}
	return result
}
```
- loop을 한번 돌면서 range의 시작점을 range가 끝나는 조건에 맞춰 변경해주는 방안으로 접근했습니다.
- inner for 문을 사용하지 않고, continue를 활용했습니다.

#### solution
```go
func composeRangesSolution(nums []int) []string {
	result := []string{}
	for i := 0; i < len(nums); i++ {
		start := nums[i]
		for {
			if i+1 < len(nums) && nums[i]+1 == nums[i+1] {
				i++
			} else {
				break
			}
		}
		end := nums[i]
		var currentRange string
		if start != end {
			currentRange = strconv.Itoa(start) + "->" + strconv.Itoa(end)
		} else {
			currentRange = strconv.Itoa(start)
		}
		result = append(result, currentRange)
	}
	return result
}
```
- 실제 솔루션은 C++ 코드이지만, go 언어로 변경해보았습니다.
- 여기서는 inner for문 (실제로는 while문 한줄)를 이용하여 내부적으로 루프 변수 i를 조건에 맞춰 증가시켜주는 기법을 사용합니다.
- continue 문을 이용하지 않으면서, 굉장히 직관적으로 코딩이 되어 있습니다.
