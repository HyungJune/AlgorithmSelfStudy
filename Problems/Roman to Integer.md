### Roman to Integer
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
- <b>주어진 Roman 숫자에 대해서 이를 정수 숫자로 변경하는 프로그램을 구현해야 합니다. </b>   
- <b>Input 범위는 1에서 3999로 제한됩니다.</b>
* * *
Solution
```go
func romanToInt(s string) int {
	romanMap := map[string]int{
		"I":  1,
		"V":  5,
		"X":  10,
		"L":  50,
		"C":  100,
		"D":  500,
		"M":  1000,
		"IV": 4,
		"IX": 9,
		"XL": 40,
		"XC": 90,
		"CD": 400,
		"CM": 900,
	}
	l := len(s)
	result := 0
	for i := 0; i < l; i++ {
		sub := s[i : i+1]
		if i+1 != l {
			next := s[i+1 : i+2]
			if romanMap[sub] < romanMap[next] {
				result = result + romanMap[s[i:i+2]]
				i = i + 1
				continue
			}
		}

		result = result + romanMap[sub]
	}
	return result
}
```
- 우선 가능한 모든 작은 경우에 수들에 대해서 Map에 Roman 표기법과 이에 대응되는 Value를 저장하고 시작하면 괜찮을 거라고 생각했습니다.
- 첫번째 시도에서는 뒤로 읽었을 때 두 자리씩 자르면 되지 않을까 싶었습니다. 하지만, 이런 접근방법을 사용할 경우 MCDL과 같은 케이스 M + CD + L을 커버하지 못함을 깨닫고 알고리즘을 다시 수정했습니다.
- 두번째 시도는 굉장히 naive한 접근방법을 사용했습니다. 위의 코드와 같이, 맨 앞글자부터 보기 시작하여 다음 글자가 현재 바라보고 있는 글자보다 클 경우 왼쪽에서 오른쪽으로 큰 Symbol 먼저 나오게 된다는 일반적인 조건에 맞지 않으므로 일반적이지 않은 "IV","IX","XL","XC","CD,"CM"이므로, Map에 이에 대응하는 값을 가져오고 index를 한 번 더 증가시키는 방식으로 코드 구현을 완료했습니다.
- LeetCode에서는 Accepted 되었습니다.
