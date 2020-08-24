#### Majority Element
#### Writer: Haram Ryu
#### Refer: LeetCode#169

## 문제 설명
길이 n의 슬라이스가 주어지는데 슬라이스의 엘리먼트 중 하나는 n/2번 이상 반복되고, 이걸, majority element라고 한다. 주어지는 슬라이스에 대해서 majority element를 찾아라.  
empty 슬라이스는 주어지지 않고, 무조건 majority element가 존재.  
***예시1***  

```
Input: [3,2,3]
Output: 3
```
***예시1*** 
```
Input: [2,2,1,1,1,2,2]
Output: 2
```

## 솔루션
```
func majorityElement(nums []int) int {
    m := make(map[int]int)
    for _, num := range nums {
        m[num] += 1   
    }
    for key, value := range m {
        if value > len(nums)/2 {
            return key
        }
    }
    return 0
}
```
- for문으로 한바퀴 돌면서 map에 element의 갯수를 value로 저장
- 다시한번 for문을 돌면서 value가 n/2보다 큰 키값을 리턴
