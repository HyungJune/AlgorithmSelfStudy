#### Running Sum of 1d Array
#### Writter: Donggyu Cho
#### Refer: LeetCode

## 문제설명
nums라는 배열이 주어질때, runningSum이라는 배열은 다음과 같의 정의합니다. runningSum[i]=sum(nums[0]...nums[i]). 
다음 주어지는 nums에 대한 runningSum을 구하시오.

<b>Example 1</b>
<pre>
<b>Input</b>: [1,2,3,4]
<b>Output</b>: [1,3,6,10]
<b>Explanation</b> Running sum은 다음과 같습니다.[1, 1+2, 1+2+3, 1+2+3+4].
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: [1,1,1,1,1]
<b>Output</b>: [1,2,3,4,5]
<b>Explanation</b> Running sum은 다음과 같습니다.[1, 1+1, 1+1+1, 1+1+1+1, 1+1+1+1+1].
</pre>

<b>Example 3</b>
<pre>
<b>Input</b>: [3,1,2,10,1]
<b>Output</b>: [3,4,6,16,17]
</pre>

<b>Constraints</b>
<pre>
<b>1 <= nums.length <= 1000 </b>
<b>-10^6 <= nums[i] <= 10^6</b>
</pre>

* * *
### Solution
#### Very Very Naive 방식
```go
func runningSum(nums []int) []int {
    var tmp []int
    tmp = make( []int, len(nums) )
    
    for i, _ := range nums {
        for j := 0; j <= i; j++ {
            tmp[i] += nums[j]
        }
    }
    return tmp
}
```
- 이전의 모든 인덱스를 접근해 값을 더하는 방식
- 시간복잡도는 O(n^2) 입니다.

#### little bit fine 방식
```go
func runningSum(nums []int) []int {
    var tmp []int
    tmp = make( []int, len(nums) )
    
    for i, _ := range nums {
        if i > 0 {
            tmp[i] = tmp[i-1] + nums[i]
        } else {
            tmp[i] = nums[i]
        }
    }
    return tmp
}
```
- nums[0]의 값은 그대로 tmp[0]에 넣음
- runningSums[i] = nums[i-1] + nums[i] (단, i>0) 인 방식으로 해결 
- 시간복잡도는 O(n)
