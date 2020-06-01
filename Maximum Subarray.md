```
package main

import (
	"fmt"
)

func main() {

	var nums []int
	nums = []int{1, 2}

	nums = preprocessing(nums)
	fmt.Println("nums: ", nums)

	max := 0
	temp := 0
	i, j := 0, 0
	for {
		if i == j {
			if nums[i] > max {
				max = nums[2*i]
			}
			i++
			if j == len(nums)/2 {
				break
			}
		}
		temp = summation(nums[2*j : 2*i+1])
		if temp > max {
			max = temp
		}
		i++
		if i == len(nums)/2+1 {
			j++
			i = j
		}
	}
	fmt.Println("max: ", max)
}

func preprocessing(s []int) []int {
	if len(s) <= 1 {
		return s
	}
	for s[0] < 0 {
		s = s[1:]
	}
	for s[len(s)-1] < 0 {
		s = s[:len(s)-1]
	}
	for i := 0; i < len(s)-2; i++ {
		if (s[i] >= 0 && s[i+1] >= 0) || (s[i] < 0 && s[i+1] < 0) {
			s[i] = s[i] + s[i+1]
			if i < len(s)-2 {
				s = append(s[:i+1], s[i+2:]...)
			} else {
				s = s[:i+1]
			}
		}
	}
	return s
}

func summation(s []int) int {
	sum := 0
	for _, value := range s {
		sum = sum + value
	}
	return sum
}
```
