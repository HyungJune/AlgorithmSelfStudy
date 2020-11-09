
### Shuffle the Array
#### Writer: Hyungjune Shin
#### Refer: LeetCode#1470
* * *
### Problem
Given the array nums consisting of 2n elements in the form [x1,x2,...,xn,y1,y2,...,yn].

Return the array in the form [x1,y1,x2,y2,...,xn,yn].

<b>Example 1</b>
<pre>
<b>Input:</b> nums = [2,5,1,3,4,7], n = 3
<b>Output:</b> [2,3,5,4,1,7] 
<b>Explanation:</b> Since x1=2, x2=5, x3=1, y1=3, y2=4, y3=7 then the answer is [2,3,5,4,1,7].
</pre>

<b>Example 2</b>
<pre>
<b>Input:</b> nums = [1,2,3,4,4,3,2,1], n = 4
<b>Output:</b> [1,4,2,3,3,2,4,1]
</pre>
* * *
### Solution
```go
func shuffle(nums []int, n int) []int {
    var result []int
    for i := 0;i<n;i++ {
        result = append(result, nums[i])
        result = append(result, nums[n+i])
    }
    
    return result
}
```
- 간단하게 n을 기점으로 삼아 y의 시작점을 찾으면 됩니다.
- result 슬라이스에 x와 y를 번갈아가면서 넣어서 x,y를 구성합니다.
