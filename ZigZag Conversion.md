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
#### Example 1:
```
<b>Input</b>
```
* * *
Solution
```go
func intToRoman(num int) string {
    result := ""
	for num > 0 {
		if num >= 1000 {
            result = result + "M"
			num = num - 1000
		} else if num >= 900 {
			result= result + "CM"
			num = num - 900
		} else if num >= 500 {
            result= result + "D"
			num = num - 500
		} else if num >= 400 {
            result= result + "CD"
			num = num - 400
		} else if num >= 100 {
            result= result + "C"
			num = num - 100
		} else if num >= 90 {
            result= result + "XC"
			num = num - 90
		} else if num >= 50 {
            result= result + "L"
			num = num - 50
		} else if num >= 40 {
            result= result + "XL"
			num = num - 40
		} else if num >= 10 {
            result= result + "X"
			num = num - 10
		} else if num >= 9 {
            result= result + "IX"
			num = num - 9
		} else if num >= 5 {
            result= result + "V"
			num = num - 5
		} else if num >= 4 {
            result= result + "IV"
			num = num - 4
		} else if num >= 1 {
            result= result + "I"
			num = num - 1
		}
	}
	return result
}
```
- LeetCode에서 Medium에 해당하는 문제인데.. 좋은 문제는 아닌 듯 합니다.
- 단순 노가다 if 문으로 작성을 했는데 쉽게 통과가 되었습니다.
- 간략하게 코드화 시키기 위해 배열을 이용하여 반복문을 돌리는 방법도 있지만, 해당 배열에 (Roman, Integer) 쌍을 어딘가에는 저장을 해놔야하는데 이렇게 배열에 작성하는 것과 if문에 작성하는 것에 비용은 비슷해 보입니다. 하지만, 코드는 간략하면 할 수록 좋다고도 생각될 수 있으므로, 이럴 경우에 위의 코드는 좋은 해답은 아닙니다.
