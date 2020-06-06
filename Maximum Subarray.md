#### Data Structure: Binary Search Tree
#### Writer: Haram Ryu
#### Refer: AppliedGo.net

## 문제 설명
정수로 이루어진 배열이 주어진다. 그 배열에서 만들 수 있는 부분배열의 수를 모두 더했을 때 가능한 가장 큰 합을 구한다.

***예시***
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

## 솔루션

```
func maxSubArray(nums []int) int {
    return maxSubarraySum(nums, 0, len(nums)-1)
}

func max2(a, b int) int {
	if a > b {
		return a
	} else {
		return b
	}
}

func max3(a, b, c int) int {
	return max2(max2(a, b), c)
}

func maxSubarraySum(array []int, start, end int) int {

	if start == end {
		return array[start]
	}
	m := (start + end) / 2
	return max3(maxSubarraySum(array, start, m), maxSubarraySum(array, m+1, end), maxCrossingSum(array, start, m, end))
}

func maxCrossingSum(array []int, start, mid, end int) int {
	leftMax := math.MinInt32
	temp := 0
	for i := mid; i >= start; i-- {
		temp = temp + array[i]
		if temp > leftMax {
			leftMax = temp
		}
	}

	rightMax := math.MinInt32
	temp = 0
	for i := mid + 1; i <= end; i++ {
		temp = temp + array[i]
		if temp > rightMax {
			rightMax = temp
		}
	}
    
	return max3(leftMax, rightMax, leftMax+rightMax)
}
```
- Divide and conquer
    - 반으로 쪼개서, 왼쪽 반과 오른쪽 반, 그리고 그 왼쪽과 오른쪽에 무조건 걸쳐있는 부분배열 중에 가장 합이 큰 것을 찾는다.
- maxSubarraySum에서는 입력 문자열에 대해서 다시 반을 쪼개서 왼쪽 반 부분배열, 오른쪽 반 부분배열에 대해서 maxSubarraySum을 재귀적으로 적용하여 최대값을 찾고, 왼쪽 반과 오른쪽 반에 걸쳐있는 부분배열중에 합이 최대인 경우도 찾아서 셋중에 최대값을 구한다.
    - maxCrossingSum에서 왼쪽 반과 오른쪽 반에 걸쳐있는 부분배열의 합 중에 최대값을 찾는다.
    - 이렇게 하면 모든 경우를 다 검사할 수 있다!!
