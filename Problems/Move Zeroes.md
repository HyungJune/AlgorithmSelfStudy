#### Move Zeroes  
#### Writer: Haram Ryu
#### Refer: LeetCode#283

## 문제 설명  
주어진 배열에 대해 모든 0 원소를 배열 뒤로 보내어라. 단, 0이 아닌 원소들의 순서를 지키면서.  

***예시***
```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```
## 전제조건
- 배열을 복사하지 않고 해보기
- 동작의 수를 최대한 줄여서 해보기


## 솔루션

```
func moveZeroes(nums []int)  {
    lastidx := 0
    for i, num := range nums {
        if num != 0 {
            nums[lastidx], nums[i] = nums[i], nums[lastidx]
            lastidx++
        }
    }
}
```
- for문으로 검사하는 동안, 0이 아닌 원소가 나왔을 때 모두 맨 앞으로 보내면 0은 뒤로 밀리게 되어 있음
- 그런데 카운터를 하나 둬서 0이 아닌 원소가 몇번째 원소와 바뀌어야하는지를 체크
