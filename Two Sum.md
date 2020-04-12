#### Two Sum  
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명  
주어진 정수의 배열 중에서 두개를 골라서 더했을때 정해진 타겟이 되는 경우의 배열의 인덱스를 리턴해야함  

## 예시와 조건
- 배열이 nums = [2, 7, 11, 15]로 주어지고, 타겟은 9로 주어졌을 때, nums[0] + nums[1] = 2 + 7 = 9 이기 때문에 리턴은 [0, 1]이 되어야 함
- 단, 같은 인덱스의 숫자를 두 번 더하는 경우는 없음

## 솔루션

```
func twoSum(nums []int, target int) []int {
    for i := 0; i < len(nums); i++ {
        for j := i + 1; j < len(nums); j++ {
            if nums[i] + nums[j] == target {
                return []int{i, j}
            }
        }    
    }
    return []int{}
}
```
- go언어 사용
- for 반복문 두개를 이용해서 앞에서부터 순서대로 다 더해서 target과 일치하는 경우의 인덱스 i, j를 찾아내는 가장 간단한 방법
- 이렇게 for문을 두번쓰면 시간이 배열의 길이의 제곱이 된다고 함
- LeetCode 통과 완료

## LeetCode 솔루션 참고 내용
- 해쉬맵을 이용하고, 정수의 보수를 찾는 방식을 사용하면 더 빠르다고 함
- 해쉬맵에서 검색하는게 for 반복문 한번 돌리는것보다 빠르다고 볼 수 있는 듯
```
func twoSum(nums []int, target int) []int {
    var idxmap map[int]int
    idxmap = make(map[int]int)
    for i := 0; i < len(nums); i++ {
        complement := target - nums[i]
        val, exists := idxmap[complement]
        if exists {
            return []int{i, val}
        }
        idxmap[nums[i]] = i
    }
    return []int{}
}
```
