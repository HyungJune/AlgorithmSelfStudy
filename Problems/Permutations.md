#### Permutations  
#### Writer: Haram Ryu
#### Refer: LeetCode#46

## 문제 설명  
주어진 배열에 대해 가능한 모든 permutation을 배열의 배열로 출력  

***예시***
```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```


## 솔루션

```
var ans [][]int

func permute(a []int) [][]int {
	ans = make([][]int, 0)
	perm(a, 0)
	return ans
}

func perm(a []int, i int) {
	if i == len(a) {
		ans = append(ans, append(make([]int, 0), a...))
		return
	}
	for j := i; j < len(a); j++ {
		a[i], a[j] = a[j], a[i]
		perm(a, i+1)
		a[i], a[j] = a[j], a[i]
	}
}

```
- 기본적인 로직은, 모든 원소들의 위치를 서로 바꾸는 것.
    - 이것을 구현하기 위한 두가지 행정은
        - 첫째, 두개의 원소를 서로 교환한다.
	- 둘째, 교환된 상태에서 스코프를 옮겨서 재귀 함수를 연속적으로 실행하며 입력된 슬라이스의 끝에 스코프가 도달할때까지 재귀함수 실행
