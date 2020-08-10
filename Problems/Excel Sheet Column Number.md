### Excel Sheet Column Number
#### Writer: Hyungjune Shin
#### Refer: LeetCode#171
* * *
### Problem
엑셀 시트지에서 주어진 Column의 이름이 주어졌을 때 이에 대응되는 Column의 숫자를 출력하는 프로그램을 작성하는 문제입니다. 
예를 들면

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
```

<b>Example1</b>
<pre>
<b>Input:</b> "A"
<b>Output:</b> 1
</pre>

<b>Example2</b>
<pre>
<b>Input:</b> "AB"
<b>Output:</b> 28
</pre>

<b>Example3</b>
<pre>
<b>Input:</b> "ZY"
<b>Output:</b> 701
</pre>

<b> Constraints: </b>
 - 1<=s.length<=7
 - s는 오직 영문 대문자로만 구성되어져만 있습니다.
 - s는 "A"와 "FXSHRXW" 사이 값만을 가지고 있습니다.
* * *
### Solution
```go
func titleToNumber(s string) int {
    alpaMap := map[byte]int{
        'A': 1,
        'B': 2,
        'C': 3,
        'D': 4,
        'E': 5,
        'F': 6,
        'G': 7,
        'H': 8,
        'I': 9,
        'J': 10,
        'K': 11,
        'L': 12,
        'M': 13,
        'N': 14,
        'O': 15,
        'P': 16,
        'Q': 17,
        'R': 18,
        'S': 19,
        'T': 20,
        'U': 21,
        'V': 22,
        'W': 23,
        'X': 24,
        'Y': 25,
        'Z': 26,
    }
    
    result := 0
    for i := 0;i<len(s);i++{
        result = result * 26 + alpaMap[s[i]]   
    }
    
    return result
}
```
- 문제는 26진수에 대한 문제입니다.
- A부터 Z까지의 map을 구성하고 26진수를 10진수로 변환하는 방식으로 풀면 됩니다.
