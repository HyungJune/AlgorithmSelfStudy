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
* * *
Solution
