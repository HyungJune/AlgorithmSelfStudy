### Max Increase to Keep City Skyline
#### Writer: Donggyu Cho
#### Refer: LeetCode#807

* * *
### Problem
이차원 배열 그리드에 

2차원 배열 그리드에서 각 값 grid[i][j]는 그곳에 위치한 건물의 높이를 나타냅니다. 우리는 건물의 높이를 얼마든지 늘릴 수 있으며 높이 0도 건물로 간주됩니다.
그리드의 네 방향, 즉 위, 아래, 왼쪽 및 오른쪽에서 볼 때 "스카이 라인"은 원래 그리드의 스카이 라인과 동일해야합니다. 도시의 스카이 라인은 멀리서 볼 때 모든 건물에 의해 형성된 직사각형의 바깥 쪽 윤곽입니다. 다음 예를 참조하십시오.

건물 높이를 늘릴 수있는 최대 총합은 얼마입니까?

예를 들면

```
Input: grid = [[3,0,8,4],[2,4,5,7],[9,2,6,3],[0,3,1,0]]
Output: 35
Explanation: 
The grid is:
[ [3, 0, 8, 4], 
  [2, 4, 5, 7],
  [9, 2, 6, 3],
  [0, 3, 1, 0] ]

위 아래에서 바라본 스카이 라인 : [9, 4, 8, 7]
왼쪽 오른쪽에서 바라본 스카이 라인 : [8, 7, 9, 3]

스카이라인의 변화 없이 높일 수 있는 최대 높이는 다음과 같다

gridNew = [ [8, 4, 8, 7],
            [7, 4, 7, 7],
            [9, 4, 8, 7],
            [3, 3, 3, 3] ]
```

 
* * *
### Solution
- 우선 최대 높이에 대한 그리드를 구한다. (maxOfRow, maxOfCol)
- 이후, 2차원배열의 요소를 모두 거쳐가며 스카이라인을 변경하지 않는 최대한의 높이를 구한다.

```
func maxIncreaseKeepingSkyline(grid [][]int) int {
   
    row := len(grid[0])
    col := len(grid)
    
    maxOfRow := make( []int, row )
    maxOfCol := make( []int, col )
    
    for i := 0; i < row; i++ {
        for j := 0; j < col; j++ {
            maxOfRow[i] = Max( maxOfRow[i], grid[i][j] )
            maxOfCol[j] = Max( maxOfCol[j], grid[i][j] )
            
        }
    }
    
    ans := 0
    for i := 0; i < row; i++ {
        for j := 0; j < col; j++ {
            ans += (Min(maxOfRow[i], maxOfCol[j]) - grid[i][j])
        }
    }
    return ans
}

func Max( a, b int ) int {
    if a > b {
        return a
    }
    return b
}

func Min( a, b int ) int {
    if a > b {
        return b
    }
    return a
}
```
