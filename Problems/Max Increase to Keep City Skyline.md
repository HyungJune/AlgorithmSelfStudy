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
