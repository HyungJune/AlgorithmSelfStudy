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
}을 

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
- 최적화가 덜된 부분들이 존재, Discussion을 참고해보니 'A'로 표기하지 않고 '0'으로 표기했으면 좀 더 간단하게 구성이 되었을 것..

#### 3가지 Solution 존재
#### DFS
```go
func numIslands(grid [][]byte) int {
    if grid == nil || len(grid) == 0 {
        return 0
    }   
    
    nr := len(grid)
    nc := len(grid[0])
    result := 0
    for r := 0;r<nr;r++ {
        for c:=0;c<nc;c++{
            if grid[r][c] == '1' {
                result++
                dfs(grid,r,c)
            }
        }
    }
    return result
}

func dfs(grid [][]byte, r int, c int){
    nr := len(grid)
    nc := len(grid[0])
    
    if r < 0 || c < 0 || r >= nr || c >= nc || grid[r][c] == '0' {
        return
    }
    
    grid[r][c] = '0'
    dfs(grid, r-1, c)
    dfs(grid, r+1, c)
    dfs(grid, r, c-1)
    dfs(grid, r, c +1)
}
```
- 앞의 방식과 같습니다.
- 다만 '0'으로 지정함으로써 함수의 길이도 줄어들었으며 좀 더 효율적으로 구성되어져 있습니다.
#### BFS
```go
func numIslands(grid [][]byte) int {
    if grid == nil || len(grid) == 0 {
        return 0
    }   
    
    nr := len(grid)
    nc := len(grid[0])
    result := 0
    for r := 0;r<nr;r++{
        for c:=0;c<nc;c++{
            if grid[r][c] == '1' {
                result++
                grid[r][c] = '0'
                var neighbors []int
                neighbors = append(neighbors, r*nc+c)
                for len(neighbors) != 0 {
                    id := remove(&neighbors)
                    row := id / nc
                    col := id % nc
                    if row-1 >= 0 && grid[row-1][col] == '1' {
                        neighbors = append(neighbors, (row-1) * nc + col)
                        grid[row-1][col] = '0'
                    }
                    if (row+1) < nr && grid[row+1][col] == '1' {
                        neighbors = append(neighbors, (row+1) * nc + col)
                        grid[row+1][col] = '0'
                    }
                    if (col-1) >= 0 && grid[row][col-1] == '1' {
                        neighbors = append(neighbors, row * nc + (col-1))
                        grid[row][col-1] = '0'
                    }
                    if (col+1) < nc && grid[row][col+1] == '1' {
                        neighbors = append(neighbors, row * nc + (col+1))
                        grid[row][col+1] = '0'
                    }
                }
                }
            }
        }
    
    return result
}

func remove(s *[]int) int {
	val := (*s)[0]
	*s = (*s)[1:len(*s)]
	return val
}
```
- 일반적으로 Queue를 사용하는데, Slice로 이를 대체했습니다. (Go에서는 따로 Queue 자료구조를 제공하지는 않습니다.)
- Remove 함수에서는 Queue에서 Pop 함수와 같은 결과를 만들어주고 있습니다.
- BFS에서는 인접한 노드들의 정보를 Queue에 저장하고, Queue에 저장된 순서대로 검사를 진행합니다. (인접한 노드들을 먼저 탐색)
#### Union Find
