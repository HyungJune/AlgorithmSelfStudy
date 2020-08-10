#### 238. Product of Array Except Self
#### Writter: Donggyu Cho
#### Refer: LeetCode

## 문제설명
nums라는 n개의 integer가 들어있는 배열이 주어졌을 때, output 배열을 구하여라. 
이때, output[i]은 nums[i]를 제외한 모든 nums의 요소를 곱한 값이다.


<b>Example 1</b>
<pre>
<b>Input</b>: [1,2,3,4]
<b>Output</b>: [24,12,8,6]
</pre>

<b>Constraints</b>
<pre>
<b> 배열의 접두사 또는 접미사 (전체 배열 포함) 요소의 곱이 32 비트 정수에 맞는다는 것이 보장된다.</b>
</pre>

<b>Note</b>
<pre>
<b> 나누기 연산이 없도록 구현하며 O(n)을 만족하도록 구현하여라</b>
</pre>

<b>Follow up</b>
<pre>
<b> 메모리를 O(1)에 해결할 수 있는가?</b>
</pre>

* * *
### Solution
```go
func productExceptSelf(nums []int) []int {

	length := len(nums)
	product1 := make([]int, length)
	product1[0] = 1

	product2 := make([]int, length)
	product2[length-1] = 1

	product1 = mulitply(nums, product1, true)
	product2 = mulitply(nums, product2, false)

	output := make( []int, length)
	for i := 0; i< length; i++ {
		output[i] = product1[i] * product2[i]
	}
	return output
}

func mulitply(nums []int, product []int, flag bool) []int {
	if flag {
		for i := 0; i < len(nums)-1; i++ {
			product[i+1] = nums[i] * product[i]
		}
	} else {
		for i := len(nums) - 1; i > 0; i-- {
			product[i-1] = nums[i] * product[i]
		}
	}

	return product
}
```

### 접근법
1. 두개의 배열 선언 및 곱의 값으로 채움(product1, product2)
1.1 product1[0] = 1, product1[i+1] = product[i] * nums[i].
1.2 product2[len(nums)-1] = 1, product2[i-1] = product2[i] * product2[i]
2. Output 배열 생성
2.1 output[i] = product1[i]*product2[i]



