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
```go
func threeSum(nums []int) [][]int {
if len(nums) < 3 {
		return nil
	}
	result := [][]int{}

	sort.Sort(sort.IntSlice(nums))

	var i int = 0
	for {
		if i >= len(nums)-2 {
			break
		}
		var lo int = i + 1
		var hi int = len(nums) - 1
		for {
			if lo >= hi {
				break
			}
			sum := nums[i] + nums[lo] + nums[hi]
			if sum == 0 {
				local := []int{}
				local = append(local, nums[i])
				local = append(local, nums[lo])
				local = append(local, nums[hi])
				result = append(result, local)
				//increase lo
				for {
					if lo <= len(nums)-2 && nums[lo] == nums[lo+1] {
						lo++
					} else {
						lo++
						break
					}
				}
				//decrease hi
				for {
					if hi-1 >= 0 && nums[hi] == nums[hi-1] {
						hi--
					} else {
						hi--
						break
					}
				}
			} else if sum < 0 {
				//increase lo
				for {
					if lo <= len(nums)-2 && nums[lo] == nums[lo+1] {
						lo++
					} else {
						lo++
						break
					}
				}
			} else if sum > 0 {
				//decrease hi
				for {
					if hi-1 >= 0 && nums[hi] == nums[hi-1] {
						hi--
					} else {
						hi--
						break
					}
				}
			}
		}
		//increase i
		for {
			if i <= len(nums)-2 && nums[i] == nums[i+1] {
				i++
			} else {
				i++
				break
			}
		}
	}
	return result
}
```
- nums를 순회하면서(i) low (i+1) / high (nums의 갯수 - 1)를 둬서 비교하는 방식
- 중복을 방지하기 위해서는 nums가 정렬된 상태여야 함. 이때 정렬 알고리즘은 O(n^2)의 복잡성보다 작거나 같기 때문에 전체 알고리즘의 시간 복잡도에는 영향을 주지 않습니다.
- 여기서 고민이였던 부분은 언제 low가 증가되고 high가 감소되야 하는냐인데, nums가 정렬된 상태라면, nums[i] + nums[low] + nums[high] 값이 0보다 작을 경우에는 지금보다 더 큰 값을 더해야하므로 low를 증가시켜야 하며, 0보다 작을 경우에는 지금보다 더 작은 값을 더해야하므로 high를 감소시켜야 합니다.
- sum이 0일 경우에는 low와 high 값을 둘다 증가/감소시켜야 합니다. (한쪽만 증가/감소 시킬 경우 절대로 0을 만족시킬 수 없음)
- i, low, high 값을 증가/감소 시킬때에는 항상 중복여부를 확인하여 중복된 경우는 넘어가게 구현이 되어야 합니다.

