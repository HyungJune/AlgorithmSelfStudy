### ZigZag Conversion
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
"PAYPALISHIRING"를 기준으로 주어진 행의 수에 따라서 zigzag 패턴으로 쓰여진 문자열은 다음과 같습니다.
(좀 더 명확한 표현을 위해 그림으로 본다면 다음과 같습니다.)
```
P   A   H   N
A P L S I I G
Y   I   R
```
이를 line by line 으로 읽으면 "PAHNAPLSIIGYIR"이 됩니다.

문자열과 행의 수를 받아서 위와 같은 변환을 시켜주는 함수를 구하는게 문제입니다.
```
string convert(string s, int numRows);
```
<b>Example 1</b>
<pre>
<b>Input</b>: s = "PAYPALISHIRING", numRows = 3
<b>Output</b>: "PAHNAPLSIIGYIR"
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: s = "PAYPALISHIRING", numRows = 4
<b>Output</b>: "PINALSIGYAHRPI"
<b>Explanation:</b>

P     I    N
A   L S  I G
Y A   H R
P     I
</pre>
* * *
### Solution
문제의 설명이 굉장히 부족하지만, 패턴이 표현된 부분을 본다면 글자가 순서대로 행을 따라 갔다가 역순으로 다시 올라오는 패턴으로 zigzag 모양을 띄고 있습니다.
제가 풀었던 방식은 다음과 같습니다.
```go
func convert(s string, numRows int) string {
	var zigzagMap [][]int
	zigzagMap = make([][]int, numRows)

	for i := 0; i < len(s); {
		for j := 0; j < numRows; j++ {
			if i >= len(s) {
				break
			}
			zigzagMap[j] = append(zigzagMap[j], i)
			i++
		}
		for j := numRows - 2; j > 0; j-- {
			if i >= len(s) {
				break
			}
			zigzagMap[j] = append(zigzagMap[j], i)
			i++
		}
	}
	var r string
	r = ""
	for i := 0; i < numRows; i++ {
		for j := 0; j < len(zigzagMap[i]); j++ {
			r += string(s[zigzagMap[i][j]])
		}
	}
	return r
    
}
```
- numRows개의 Slice를 통하여 순차적으로 index를 넣습니다. ZigZag 모양이다보니, 순차적으로 index를 넣은 후 역순으로 다시 넣어주어야 합니다.
- 넣은 index를 기반으로 각 각의 Slice를 그대로 스트링으로 묶습니다.
