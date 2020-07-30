#### 650. 2 Keys Keyboard
#### Writter: Donggyu Cho
#### Refer: LeetCode

## 문제설명
초기에 'A' 문자 하나가 주어진다. 해당 A를 이용하여 할 수 있는 동작은 아래 두개이다.
1. Copy All: 현재 notepad에 있는 모든 문자열을 복사한다
2. Paste: 마지막으로 복사한 문자열을 붙여넣기한다.

n이란 숫자가 주어질때, notepad에 n개의 'A'문자열을 위의 동작을 통해 만들 경우 가장 적은 동작 개수를 구하여라


<b>Example 1</b>
<pre>
<b>Input</b>: 3
<b>Output</b>: 3
<b>Explanation</b>: 
초기 문자는 'A'. 
첫번째 동작으로 Copy All 수행
두번째 동작으로 Paste 실행.('AA')
세번째 동작으로 Paste 실행.('AAA')
</pre>

<b>Constraints</b>
<pre>
<b> n의 범위는 [1,1000]이다. </b>
</pre>

* * *
### Solution
```go
package main

import (
	"fmt"
	"math/big"
)

type node struct {
	value int
}

type stack struct {
	count int
	nodes []*node
}

func (s *stack) Push(n *node) {
	s.nodes = append(s.nodes[:s.count], n)
	s.count++
}

func (s *stack) Pop() *node {
	if s.count == 0 {
		return nil
	}
	s.count--
	return s.nodes[s.count]
}

func NewStack() *stack {
	return &stack{}
}

func main() {
	n := 30
	fmt.Println(minSteps(n))
}

func minSteps(n int) int {
	stack := NewStack()
	sum := 0

	factorization(n, stack)

	for stack.count != 0 {
		sum += stack.Pop().value
	}

	return sum
}

func factorization(n int, s *stack) {
	if n == 1 {
		return
	}
	factor := find_factor(n)
	if factor == -1 {
		panic("Error")
	}
	s.Push(&node{value: factor})
	factorization(n/factor, s)

	return
}

func find_factor(n int) int {
	if n%2 == 0 {
		return 2
	}
	if isPrime(n) {
		return n
	}

	for i := 3; i*i <= n; i = i + 2 {
		if n%i == 0 {
			return i
		}
	}
	return -1
}

func isPrime(n int) bool {
	return big.NewInt(int64(n)).ProbablyPrime(0)
}
```

### 접근법
1. 입력 n에 대해 인수분해 실행
1.1 입력 값 n이 소수인지 확인
1.1.1 ProbablyPrime()이라는 메소드가 있는데 이는 내부적으로 MillerRabin 알고리즘으로 구현되어 있다.
1.2 만약 소수가 아니면 반복문을 실행
1.2.1 2부터 루트 n보다 작은 수까지 반복문을 돌며 인수를 찾아 낸다.
1.2.2 인수를 찾을때 마다 queue에 넣음
2. queue의 값들을 pop하며 sum에 더함
3. sum값 출력
