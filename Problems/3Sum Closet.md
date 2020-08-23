### 3Sum Closet
#### Writer: Hyungjune Shin
#### Refer: LeetCode#16
* * *
### Problem
```nums```라는 n개의 정수로 이루어진 행렬과 target이 주어졌을 때 nums의 원소 3개를 합한 값이 target과 가장 가까웠을 때
nums의 원소 3개의 합을 구하는 문제입니다.

<b>Example 1:</b>
<pre>
<b>Input:</b> nums = [-1,2,1,-4], target = 1
<b>Output:</b> 2
<b>Explanation:</b> target에 가장 가까운 조합은 (-1+2+1 = 2)이므로 결과는 2입니다.
</pre>

<b>Constrains:</b>
- ```3<=nums.length<=10^3```
- ```-10^3<=nums[i]<=10^3```
- ```-10^4<=target<=10^4```

* * *
### Solution
#### Two Point 방식
```go
func threeSumClosest(nums []int, target int) int {
  sort.Sort(sort.IntSlice(nums))
  i := 0
  result := 10000
  smallestGap := abs(result - target)
  FirstLoop:
  for {
    if i == len(nums) {
      break
    }
    low := i + 1
    high := len(nums) - 1
    for {
      if low >= high {
        break
      }
      if nums[i]+nums[low]+nums[high] == target {
        result = nums[i] + nums[low] + nums[high]
        smallestGap = 0
        break FirstLoop
      } else if nums[i]+nums[low]+nums[high] < target {
        gap := abs(target - (nums[i] + nums[low] + nums[high]))
        if gap < smallestGap {
          smallestGap = gap
          result = nums[i] + nums[low] + nums[high]
        }
        for {
          if low+1 < high && nums[low] == nums[low+1] {
            low++
          } else {
            low++
            break
          }
        }
      } else {
        gap := abs(target - (nums[i] + nums[low] + nums[high]))
        if gap < smallestGap {
          smallestGap = gap
          result = nums[i] + nums[low] + nums[high]
        }
        for {
          if low < high-1 && nums[high] == nums[high-1] {
            high--
          } else {
            high--
            break
          }
        }
      }
    }
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

func abs(x int) int {
  if x < 0 {
    return -x
  }
  return x
}
```
- nums를 순회하면서(i) low (i+1) / high (nums의 갯수 - 1)를 둬서 비교하는 방식 (예전 3Sum 문제와 동일하게 접근)
- 중복을 방지하기 위해서는 nums가 정렬된 상태여야 함. 이때 정렬 알고리즘은 O(n^2)의 복잡성보다 작거나 같기 때문에 전체 알고리즘의 시간 복잡도에는 영향을 주지 않습니다.
- 여기서 고민이였던 부분은 언제 low가 증가되고 high가 감소되야 하는냐인데, nums가 정렬된 상태라면, nums[i] + nums[low] + nums[high] 값이 target보다 작을 경우에는 지금보다 더 큰 값을 더해야하므로 low를 증가시켜야 하며, target보다 작을 경우에는 지금보다 더 작은 값을 더해야하므로 high를 감소시켜야 합니다.
- 세 원소를 더한 값이이 target과 같은 경우에는 low와 high 값을 둘다 증가/감소시켜야 합니다. (이 Case에 걸리면 답은 무조건 이때의 세 원소의 합입니다.)
- i, low, high 값을 증가/감소 시킬때에는 항상 중복여부를 확인하여 중복된 경우는 넘어가게 구현이 되어야 합니다.

