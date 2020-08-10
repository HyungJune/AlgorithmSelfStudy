#### Queue Reconstruction by Height
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
사람들의 리스트가 있고, 사람들은 두개의 정수의 순서쌍(h, k)로 표현되는데
h는 그 사람의 키이고, k는 그 사람보다 앞에서 서 있는 사람 중에 키가 더 크거나 같은 사람의 수이다.
Input은 순서가 흐트러진 상태로 들어오는데 이걸 제대로 줄세우는 알고리즘을 작성해야한다.
***예시***  
다음 바이너리 트리는 대칭
```
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```

## 솔루션
```
	sort.Slice(input, func(i, j int) bool {
		return input[i][0] > input[j][0]
	})

	sort.Slice(input, func(i, j int) bool {
		return input[i][1] < input[j][1]
	})
	fmt.Println(input)

	var result [][]int
	var cnt int = 0
	for _, slice := range input {
		fmt.Println(slice)
		if len(result) == 0 {
			result = append(result, slice)
			continue
		}
		for j, scope := range result {
			if scope[0] >= slice[0] {
				cnt++
			}

			if slice[1] == 0 {
				tmp := make([][]int, len(result))
				copy(tmp, result)
				result[0] = slice
				result = append(result[:1], tmp...)
				cnt = 0
				break
			} else if slice[1] == cnt {
				if j == len(result)-1 {
					result = append(result, slice)
					cnt = 0
					break
				} else {
					fmt.Println("else in")
					tmp := make([][]int, len(result[j+1:]))
					copy(tmp, result[j+1:])
					fmt.Println(result[j+1:])
					fmt.Println(tmp)
					result = append(result[:j+1], slice)
					fmt.Println(result)
					result = append(result, tmp...)
					cnt = 0
					break
				}
			}
			fmt.Println(result)
		} 
```
