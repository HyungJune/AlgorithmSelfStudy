### 3Sum
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
```nums```라는 n개의 정수로 이루어진 행렬이 주어졌을 때 a+b+c=0을 만족하는 모든 a,b,c 쌍들을 찾는 함수를 구현해야합니다.

#### Note
3개의 쌍은 순서와 상관없이 다른 쌍들과 중복되어서는 안됩니다.
(예를 들면, (0,1,-1)과 (1,0,-1)은 중복입니다.)

<b>Example</b>
<pre>
Given array nums = [-1,0,1,2,-1,-4],

A solution set is:
[
  [-1,0,1],
  [-1,-1,2],
]
</pre>
* * *
### Solution
#### Brute-Force 방식
```go
func threeSum(nums []int) [][]int {
  result := [][]int{}

	checkDuplicate := func(r []int, s []int) bool {
		sort.Sort(sort.IntSlice(r))
		sort.Sort(sort.IntSlice(s))
		for i := 0; i < len(r); i++ {
			if r[i] != s[i] {
				return false
			}
		}
		return true
	}
    for i:=0;i<len(nums);i++ {
        for j:=i+1;j<len(nums);j++{
            for k:=j+1;k<len(nums);k++{
                if i == k || j == k {
                    continue
                }
                if nums[i] + nums[j] + nums[k] == 0 {
                    local := []int{}
                    local = append(local, nums[i])
                    local = append(local, nums[j])
                    local = append(local, nums[k])
                    
                    for _, r := range result {
                        if checkDuplicate(r, local) == true {
                            goto LABEL        
                        }
                    } 
                    
                    result = append(result, local)
                    
                }
                LABEL:
            }
        }
    }
    
    return result
}
```
- 모든 경우의 수를 다 찾는 방식입니다.
- 중간 중간에 중복인 Case를 검열하는 방식입니다.
- Time Limit Exceeded가 발생하는 해결법입니다.

#### Two Point 방식
- 현재 구현 중, 중복된 Case에 대한 처리가 복잡..

#### Hash Set 
