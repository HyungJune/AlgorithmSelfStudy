### String to Integer (atoi)
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
스트링 값을 정수 값으로 변환시켜주는 atoi 함수를 구현하는 문제입니다. 이 함수는 처음에 나타나는 공백(white space)문자를 제거합니다. 공백 문자는 처음으로 공백이 아닌 문자가 나올 때까지 제거됩어야 합니다. 공백이 아닌 문자가 나타났을 경우 해당 문자를 기점으로 시작합니다. 양수 혹은 음수 기호를 받을 수 있어야 하며 가능한 많은 자릿 수를 받아서 숫자로 표현되어야 합니다.

해당 함수는 숫자로 표현되어진 문자 다음에 숫자가 아닌 문자도 받을 수 있어야 합니다. 이때 숫자가 아닌 문자들은 무시됩니다. 만약 처음 보이는 공백이 아닌 문자가 숫자 형태가 아닐 경우 혹은 str의 모든 부분들이 공백일 경우에는 0를 결과 값으로 가져야 합니다.

<b>Node</b>

- 스페이스 문자인 ' '만이 유일한 공백문자로써 인식되어야 합니다.
- 구현되는 함수는 오직 32 비트 크기를 가진 정수형만 다뤄져야 합니다: [-2^31,2^31-1]. 만약 범위를 벗어난다면 INT_MIN(-2^31) 또는 INT_MAX(2^31-1)을 결과 값으로 가져야 합니다. 

<b>Example1</b>
<pre>
<b>Input</b>: "42"
<b>Output</b>: 42
</pre>

<b>Example2</b>
<pre>
<b>Input</b>: "   -42"
<b>Output</b>: -42
</pre>

<b>Example3</b>
<pre>
<b>Input</b>: "4193 with words"
<b>Output</b>: 4193
</pre>

<b>Example4</b>
<pre>
<b>Input</b>: "words and 987"
<b>Output</b>: 0
</pre>

<b>Example5</b>
<pre>
<b>Input</b>: "-91283472332"
<b>Output</b>: -2147483648
</pre>

* * *
### Solution
