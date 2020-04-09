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
