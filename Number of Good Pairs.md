#### Number of Good Pairs
#### Writer: Donggyu Cho
#### Refer: LeetCode

## 문제 설명
nums라는 배열이 주어질때, 다음의 조건을 만족하는 pair(i,j)는 good Pair라고 부릅니다.( nums[i] == nums[j] and i < j )
다음 주어지는 nums에 대한 good pairs를 구하시오.

<b>Example 1</b>
<pre>
<b>Input</b>: [1,2,3,1,1,3]
<b>Output</b>: 4
<b>Explanation</b> (0,3), (0,4), (3,4), (2,5)는 good pair입니다.
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: [1,1,1,1]
<b>Output</b>: 6
<b>Explanation</b> 모든 pair는 good pair입니다.
</pre>

<b>Example 3</b>
<pre>
<b>Input</b>: [1,2,3]
<b>Output</b>: 0
</pre>

<b>Constraints</b>
<pre>
<b>1 <= nums.length <= 1000 </b>
<b>1 <= nums[i] <= 100</b>
</pre>

* * *
### Solution
#### Very Very Naive 방식

- 이중포문을 이용해 i를 고정하고 j로 나머지 인덱스에 접근해가며 하나씩 비교
- nums[i] == nums[j] 일 경우 sum++ 하는 방식으로 접근
- (장점)in-memory방식으로 memory적으로는 O(n)
- (단점)n은 len(nums)이며 시간복잡도는 O(n^2)


#### little bit fine 방식
```go
func numIdenticalPairs(nums []int) int {
    
    val_index := make(map[int][]int)
    
    for _, val := range nums {
        if _, ok := val_index[val]; ok {
            val_index[val] = append ( val_index[val], val )
        } else {
            val_index[val] = make( []int, 0 )
            val_index[val] = append ( val_index[val], val )
        }
    }
    var sum int
    sum = 0
    for _, val := range val_index {
        length := len(val)
        sum += (length*(length-1))/2
    }
    
    return sum
}
```
- nums[i]를 key로하며 []int를 value로 같는 map 데이터구조 사용
- value의 []int에는 key와 동일한 값들의 indices of nums을 저장
- (장점) n은 len(nums)이며 m은 중복을 제거한 nums[i]의 값의 개수라 할때, O(nm)
- (장점) 중복된 값이 많으면 많을수록 직관적인 방법 보다 효율적
- (단점) 추가적인 메모리가 소요되며 m은 중복을 제거한 nums[i]의 값의 개수라 할때, O(m) 만큼의 추가적인 메모리가 필요(for map)
