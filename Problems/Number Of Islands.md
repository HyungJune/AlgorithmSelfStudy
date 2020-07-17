### Number of Islands
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
2차원 grid가 주어졌을 때, 섬의 갯수를 구하는 문제입니다. 2차원 grid에서 '1'은 땅을 의미하며 '0'은 물을 의미합니다.
섬은 물에 의해 둘러 싸여진 영역이며 수평 혹은 수직으로 인접한 땅으로 구성되어집니다. 
grid의 모든 모서리는 물로 이루어졌다고 가정합니다.

<b>Example 1</b>
<pre>
<b>Input:</b> grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
<b>Output:</b> 1
</pre>

<b>Example 2</b>
<pre>
<b>Input:</b> grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
<b>Output:</b> 3
</pre>
* * *
### Solution
#### 내가 생각해본 방식 (DFS 방식인듯)
```go
func numIslands(grid [][]byte) int {
	i := 0
	j := 0
	lands := 0
	for {
		lands += isLands(grid, i, j)
		i, j = findNotChecked(grid)
		if i == -1 && j == -1 {
			break
		}
	}
	return lands
}

func isLands(grid [][]byte, i int, j int) int {
	if i < 0 || j < 0 || i >= len(grid) || j >= len(grid[0]) {
		return 0
	}
	if grid[i][j] == '1' {
		grid[i][j] = 'A'
		_ = isLands(grid, i, j+1)
		_ = isLands(grid, i, j-1)
		_ = isLands(grid, i+1, j)
		_ = isLands(grid, i-1, j)
	} else if grid[i][j] == '0' {
		grid[i][j] = 'A'
		return 0
	}
	return 1
}

func findNotChecked(grid [][]byte) (int, int) {
	for i, gridI := range grid {
		for j, value := range gridI {
			if value != 'A' {
				return i, j
			}
		}
	}
	return -1, -1
}
```
- 모든 타일을 'A'로 체크하면서 4가지 방향을 Check합니다.
- 현재 i,j가 땅일 경우 ('1'), 위, 아래, 왼쪽, 오른쪽 4가지 방향에 대해서 재귀적으로 땅인지 확인합니다.
- 만약 땅이 아닐 경우 'A'로 체크하고 0을 리턴하고 함수를 끝냅니다.
- 4가지 방향에 대해서 타일을 'A'로 확인이 다 되었다면 1을 리턴합니다.
- findNotChecked 함수를 통해 타일 중 'A'가 아직 표시안된 부위를 찾아내고, 해당 부위를 기점으로 다시 isLands 함수를 돌립니다.
- 모든 grid가 'A'로 표기가 되면 결과 값을 리턴하고 종료합니다.

#### 3가지 Solution 존재
#### DFS
#### BFS
#### Union Find
