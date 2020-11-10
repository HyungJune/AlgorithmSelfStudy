### Total Hamming Distance
#### Writer: Donggyu Cho
#### Refer: LeetCode#477

* * *
### Problem
The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Now your job is to find the total Hamming distance between all pairs of the given numbers.

Example
```
Input: 4, 14, 2

Output: 6

Explanation: In binary representation, the 4 is 0100, 14 is 1110, and 2 is 0010 (just
showing the four bits relevant in this case). So the answer will be:
HammingDistance(4, 14) + HammingDistance(4, 2) + HammingDistance(14, 2) = 2 + 2 + 2 = 6.
```

 
* * *
### Solution
- 각 숫자들을 32bit로써 보며, LSB부터 MSB까지 한 bit씩 보며 1인 갯수를 구한다
- 각 비트때 마다 1인 갯수를 이용해 1인 조합(Combination)을 구한다 (numberOfOne * (len(inputNums) - numberOfOne)
- 각 비트마다의 조합의 값들을 더하여 출력


```
func totalHammingDistance(nums []int) int {
    var sum int
    var totalSum int
    totalSum = 0
    for i := 0; i < 32; i++ {
        sum = 0
        for _, val := range nums {
            if ((val >> i) & 1) == 1 {
                sum++
            }
        }
        totalSum += sum * (len(nums) - sum)
    }
    return totalSum
}
```
