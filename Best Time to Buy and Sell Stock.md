### Best Time to Buy and Sell Stock
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
i번째 요소가 i날의 주어진 주식의 가격을 가리키는 배열이 있다고 할 경우, 최대 수익을 계산하는 알고리즘을 만드는 문제입니다.
이때, 최대 한번의 거래만 허용됩니다. (즉, 주식 하나를 사고 해당 주식을 팖)

#### Note
구매한 날 전에는 주식을 판매할 수 없습니다.

<b>Example 1</b>
<pre>
<b>Input</b>: [7,1,5,3,6,4]
<b>Output</b>: 5
<b>Explanation</b> 2번째 날에 사고 (price = 1), 5번째 날에 팔면 됩니다. (price = 6), profit = 6 - 1 = 5. 수익을 얻으려면 판매 금액은 항상 구매 가격보다 커야합니다.
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: [7,6,4,3,1]
<b>Output</b>: 0
<b>Explanation</b>: 이 경우 거래는 이루어지지 않으며, max profit은 0입니다.
</pre>
* * *
### Solution
#### Brute-Force 방식
```go
func maxProfit(prices []int) int {
    max := 0
    buy := 0
    for {
        if buy >= len(prices) - 1 {
            break
        }
        for sell:= buy+1;sell<len(prices);sell++ {
            profit := prices[sell] - prices[buy]
            if profit > max {
             max = profit
           }       
        }
        buy++
    }
    return max
}
```
- 모든 경우의 수를 다 찾는 방식입니다.
- 최대 수익을 계산합니다.
- 시간복잡도는 O(n^2) 입니다.

#### One Pass 방식
```go
func maxProfit(prices []int) int {
    const UintSize = 32 << (^uint(0) >> 32 & 1)
    const (
        MaxInt = 1 << (UintSize -1) - 1
        MinInt = -MaxInt - 1
        MaxUint = 1 << UintSize - 1
    )
    
    minprice := MaxInt
    maxprofit := 0
    for i := 0 ;i<len(prices);i++{
        if prices[i] < minprice {
            minprice = prices[i]
        } else if prices[i] - minprice > maxprofit {
            maxprofit = prices[i] - minprice
        }
    }
    return maxprofit
}
```
- 초기 최소 금액을 Integer의 최대값으로 설정합니다.
- 현재 가장 최소인 금액을 가지고 현재 가격이 최소가 보다 작다면 최소가격을 갱신합니다.
- 만약 현재 금액이 최소가격보다 클 경우 profit을 계산하며 maxprofit을 결정합니다.
- 시간복잡도는 O(n)입니다.


