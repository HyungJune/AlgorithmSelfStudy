```
func totalHammingDistance(nums []int) int {
    sort.Ints(nums)

	dp := make(map[pair]int)

	for i := 0; i < len(nums)-1; i++ {
		for j := i + 1; j < len(nums); j++ {
			dp[pair{nums[i], nums[j], i,j}] = HammingDistance(nums[i], nums[j])
		}
	}

	sum := 0

	for _, val := range dp {
		fmt.Println(val)
		sum += val
	}

	return sum
    
}

type pair struct {
	a int
	b int
    c int
    d int
}

func HammingDistance(a, b int) int {
	a ^= b
	var i int
	for i = 0; a != 0; i++ {
		a &= (a - 1)
	}
	return i
}
```
