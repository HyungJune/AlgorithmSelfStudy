#### 1282. Group the People Given the Group Size They Belong To
#### Writter: Donggyu Cho
#### Refer: LeetCode

## 문제설명
n명의 사람이 존재하고 그들 각각이 0부터 n-1까지의 ID를 갖고 있으며 그들은 정확히 하나의 그룹에 속하며 두개 이상의 그룹에 속하지 않는다. 
이러한 상황속에서 GroupSize라는 배열이 주어지며 배열의 각 index는 한명의 people을 뜻하며 value는 그 people이 속한 그룹에 속한 people들의 명수를 뜻한다.
주어진 GroupSize라는 배열을 이용하여 각 그룹의 people들의 배열을 표현해보시오. 만약 다양한 솔루션이 존재하는 경우 그 중 하나의 솔루션만 제시하여도 인정된다.

<b>Example 1</b>
<pre>
<b>Input</b>: groupSizes = [3,3,3,3,3,1,3]
<b>Output</b>: [[5],[0,1,2],[3,4,6]]
<b>Explanation</b> 한가지 가능한 솔루션은 [[2,1,6],[5],[0,4,3]]. 다른 한가지 솔루션은 [[5],[0,6,2],[4,3,1]].
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: groupSizes = [2,1,3,3,3,2]
<b>Output</b>: [[1],[0,5],[2,3,4]]
</pre>

<b>Constraints</b>
<pre>
<b> groupSizes.length == n </b>
<b> 1 <= n <= 500</b>
<b> 1 <= groupSizes[i] <= n </b>
</pre>

* * *
### Solution
#### Very Very Naive 방식
```go
func groupThePeople(groupSizes []int) [][]int {
    var people map[int][]int
    var returnArr [][]int
        
    returnArr = make( [][]int, 1)
    returnArr[0] = make( []int, 0 )
    people = make(map[int][]int)
    
    for i, val := range groupSizes {
        if _, ok := people[val]; !ok {
            people[val] = make([]int, 0)
        }
        
        people[val] = append(people[val], i)
        
        if len(people[val]) == val {
            returnArr = append( returnArr, people[val] )
            people[val] = make([]int,0)
        }
    }
    return returnArr[1:]
}
```
- people이란 map의 key는 한 그룹안에 속한 사람의 수(group의 size)이고 value는 그 그룹에 속한 people들의 ID
- returnArr의 Value들은 각각의 그룹을 뜻하며, Value인 int slice 내부에는 해당 그룹에 속한 people들의 ID가 저장됨
- 이렇게 두개의 자료구조를 사용한 이유는 Map 만으로는 한 group의 size가 다른 group의 size와 같을 경우 연속하여 저장할 수가 없었기 때문
- 한 그룹이 가득 찼을 경우 people 맵의 value 값을 returnArr에 넣어주고 새로운 slice로 다시 채워나감
- 시간복잡도는 People의 수를 n이라 하였을때, O(n)
- 처음 생각한 방식은 sizeOfGroup이 같은 people들을 따로 모아서 map에 넣어두고 다시 map 전부를 읽으며 Output을 내는 방식으로 시작하였으며 이 경우 returnArr이란 배열 필요x
- 이 경우 map의 Key의 개수를 m이라 하였을때, 시간복잡도 O(nm)이 된다
- 이를 O(n)으로 만들기 위해 returnArr이란 배열을 추가적으로 사용

