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
```go
func myAtoi(str string) int {
    intLen := 0
    var result int = 0
    isMinus := false
    isFirstZero := false
    isPlus := false
    for i:=0;i<len(str);i++{
        if isFirstZero && (str[i:i+1] == " " || str[i:i+1] == "-") {
            return 0
        }
        if isPlus && str[i:i+1] == "+" && result == 0{
            return 0
        }
        if isMinus && str[i:i+1] == "-" && result == 0{
            return 0
        }
        if (isPlus || isMinus || intLen != 0) && str[i:i+1] == " " {
            break;
        }
        if str[i:i+1] == " " {
            continue
        }
        if (i+1 < len(str)) && (str[i:i+2] =="+-" || str[i:i+2] =="-+") {
            return 0
        }
        if str[i:i+1] == "-" && intLen == 0 {
            isMinus = true
            continue
        }
        if str[i:i+1] == "+" && intLen == 0 {
            isPlus = true
            continue
        }

        var integer int
        switch str[i:i+1] {
        case "0":
            integer = 0
            break;
        case "1":
            integer = 1
            break;
        case "2":
            integer = 2
            break;
        case "3":
            integer = 3
            break;
        case "4":
            integer = 4
            break;
        case "5":
            integer = 5
            break;
        case "6":
            integer = 6
            break;
        case "7":
            integer = 7
            break;
        case "8":
            integer = 8
            break;
        case "9":
            integer = 9
            break;
        default:
            integer = -1    
        }
        if integer == -1 && intLen == 0 {
            return 0
        }
        if integer == -1 && intLen != 0 {
            break;
        }
        if integer == 0 && intLen == 0 {
            isFirstZero = true
            continue;
        }
        
        if result > 214748365 {
            return 2147483647
        }
        if result >= 214748364 && integer > 7 {
            return 2147483647   
        }
        
        if result <= -214748365 {
            return -2147483648
        }
        if result <= -214748364 && integer > 8 {
            return -2147483648
        }
        
        if isMinus {
            result = result * 10 + (-1) * integer
            
        } else { 
            result = result * 10 + integer
        }
        
        intLen++
    }
    return result
}
```
- str의 길이만큼 루프를 돌면서 str 문자 하나하나를 보고, 공백이면 continue로 넘기고, 처음으로 만난 문자인지를 확인하기 위해 integer의 길이를 따로 저장해두어서 예외처리를 했습니다.
- 우선 숫자인 문자일 경우에는 Switch문을 통하여 0~9를 숫자로 만들고 음수 혹은 양수인지에 따라 
```go
...
  if isMinus {
            result = result * 10 + (-1) * integer
            
        } else { 
            result = result * 10 + integer
        }
...
```

위의 공식을 통하여 결과 값을 만들었습니다.
- 나머지 부분들은 자잘한 예외적인 상황들을 처리하기 위한 구문들로 이루어져 있습니다. 
