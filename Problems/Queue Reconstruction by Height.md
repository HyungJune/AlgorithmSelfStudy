#### Queue Reconstruction by Height
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
사람들의 리스트가 있고, 사람들은 두개의 정수의 순서쌍(h, k)로 표현되는데
h는 그 사람의 키이고, k는 그 사람보다 앞에서 서 있는 사람 중에 키가 더 크거나 같은 사람의 수이다.
Input은 순서가 정렬되지 않은 상태인데 이걸 규칙에 맞게 정렬해야 한다.  
***예시***  

```
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```

## 솔루션
```
func reconstructQueue(people [][]int) [][]int {

	sort.Slice(people, func(i, j int) bool {
		return people[i][0] < people[j][0] || (people[i][0] == people[j][0] && people[i][1] < people[j][1])
	})

	result := make([][]int, len(people))
	for i := range result {
		result[i] = []int{-1, -1}
	}

	for _, person := range people {
		index := person[1]
		for j, scope := range result {

			if scope[0] == -1 && index == 0 {
				result[j] = person
				break
			} else if scope[0] == -1 || scope[0] == person[0] {
				index--
			}

		}
	}
	return result
}
``
- sorting이 중요함
    - h의 오름차순으로 정렬하고, 같은 h에 대해서는 k의 오름차순으로 정렬
- result는 input(=people) 과 같은 크기로 모든 엘리먼트를 {-1, -1}로 채움
- people를 for문으로 한바퀴 돌면서 검사를 진행
    - 해당 회차의 요소(=person)의 k를 index로 하여 result 슬라이스의 앞에서부터 검사하면서 scope[0]이 -1이거나 person[0]과 같은 경우에는 index--
    - 반대로 생각하면 result 슬라이스에서 이미 채워진 부분은 person[0]보다 작은 값들이므로 index--가 되지 않아야함(오름차순으로 정렬됐으니까)
