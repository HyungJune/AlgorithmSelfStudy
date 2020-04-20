#### Merge Two Sorted Lists
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명

## 솔루션
```
package main

import (
	"fmt"
	"sort"
	"strconv"
	"strings"
)

type ListNode struct {
	Val  int
	Next *ListNode
}

func main() {
	var l1 *ListNode = new(ListNode)
	l1.Val = 1
	l1.Next = &ListNode{}
	l1.Next.Val = 2
	l1.Next.Next = &ListNode{}
	l1.Next.Next.Val = 4

	var l2 *ListNode = new(ListNode)
	l2.Val = 1
	l2.Next = &ListNode{}
	l2.Next.Val = 3
	l2.Next.Next = &ListNode{}
	l2.Next.Next.Val = 4

	var mergedSlice []int
	var mergedSliceString []string
	for l1 != nil {
		fmt.Printf("l1.Val = %d\n", l1.Val)
		mergedSlice = append(mergedSlice, l1.Val)
		mergedSliceString = append(mergedSliceString, strconv.Itoa(l1.Val))
		l1 = l1.Next
	}
	for l2 != nil {
		fmt.Printf("l2 Val = %d\n", l2.Val)
		mergedSlice = append(mergedSlice, l2.Val)
		mergedSliceString = append(mergedSliceString, strconv.Itoa(l2.Val))
		l2 = l2.Next
	}
	sort.Ints(mergedSlice)
	sort.Strings(mergedSliceString)
	//for i := range mergedSlice {
	//	mergedSliceString = append(mergedSliceString, strconv.Itoa(mergedSlice[i]))
	//}
	mergedString := strings.Join(mergedSliceString, "")
	fmt.Printf("Merged string is %s\n", mergedString)
}
```
