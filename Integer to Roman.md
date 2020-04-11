### Integer to Roman
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
Roman 숫자는 7개의 다른 Symbol들로 구성됩니다. (I, V, X, L, C, D, M)   
각 각의 Symbol과 Value는 다음과 같습니다.    
<pre>
<b>Symbol    Value</b>
I         1
V         5
X         10
L         50
C         100
D         500
M         1000
</pre>

예를 들면
- II는 2 (I + I)
- XII는 X + I + I = 12
- XXVII는 XX + V + II = 27

일반적으로, Roman 숫자는 왼쪽에서 오른쪽으로 큰 Symbol 먼저 나오게 됩니다.   
다만, 4는 Roman 숫자로 IIII가 아닙니다. 대신 IV로 표기됩니다.   
V전에 I가 올 경우에는 V에서 I를 빼게 됩니다.   
같은 방식으로 숫자 9는 IX로 표기됩니다.   
이와 같은 방식의 6가지 표기법들은 다음과 같습니다.   
```
- I는 4와 9를 표기하기 위해 V(5)와 X(10) 전에 나타날 수 있습니다.
- X는 40과 90을 표기하기 위해 L(50)과 C(100) 전에 나타날 수 있습니다.
- C는 400과 900을 표기하기 위해 D(500)과 M(1000) 전에 나타날 수 있습니다.
```
- <b>주어진 Integer에 대해서 이를 Roman 표기법으로 변경하는 프로그램을 구현해야 합니다. </b>   
- <b>Input 범위는 1에서 3999로 제한됩니다.</b>
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
