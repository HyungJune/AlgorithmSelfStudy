### Regular Expression Matching
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
주어진 입력 스트링 값 s와 패턴 p에 대해서 ```'.'```과```'*'```를 지원하면서 정규표현식이 맞는지 확인하는 알고리즘을 구현해야 합니다.   

```
'.'은 어떤 하나의 문자에 매칭됩니다.
'*'은 길이가 0 또는 그 이상의 연속된 문자들에 매칭됩니다.
```
매칭은 전체 인풋 string을 다뤄야 합니다. (부분적으로만 다루어서는 안됩니다.)

<b>Node</b>
  - ```s```는 비어있을 수 있으며 오직 소문자 형태의 문자(a-z)만을 포함합니다.
  - ```p```는 비어있을 수 있으며 오직 소문자 형태의 문자(a-z)와 ```.```과 ```*```을 포함합니다.

<b>Example 1</b>
<pre>
<b>Input</b>:
s = "aa"
p = "a"
<b>Output</b>: false
<b>Explanation</b>: "a" does not match the entire string "aa".
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>:
s = "aa"
p = "a*"
<b>Output</b>: true
<b>Explanation</b>: '*' means zero or more of the preceding element, 'a'.
Therefore, by repeating 'a' once, it becomes "aa".
</pre>

<b>Example 3</b>
<pre>
<b>Input</b>:
s = "ab"
p = ".*"
<b>Output</b>: true
<b>Explanation</b>: ".*" means "zero or more (*) of any character (.)".
</pre>

<b>Example 4</b>
<pre>
<b>Input</b>:
s = "aab"
p = "c*a*b"
<b>Output</b>: true
<b>Explanation</b>: c can be repeated 0 times, a can be repeated 1 time. Therefore,
it matches "aab".
</pre>

<b>Example 5</b>
<pre>
<b>Input</b>:
s = "mississippi"
p = "mis*is*p*."
<b>Output</b>: false
</pre>
* * *
### Solution
```go
func isMatch(s string, p string) bool {
   if len(s) == 0 && len(p) == 0 {
		return true
	}
	if len(s) != 0 && len(p) == 0 {
		return false
	}
	if len(s) == 0 && len(p) != 0 {
		if p[0] == '.' && len(p) > 1 && p[1] != '*' {
			return false
		} else if len(p) > 1 && p[1] == '*' {
			return isMatch(s, p[2:len(p)])
		} else {
			return false
		}
	}

	if len(p) > 1 && p[1] == '*' {
		if p[0] != s[0] && p[0] != '.' {
			p = p[2:len(p)]
			return isMatch(s, p)
		} else {
			if p[0] == '.' {
				if len(s) == 1 && len(p) == 0 {
					return true
				}
				return isMatch(s[1:len(s)], p) || isMatch(s[1:len(s)], p[2:len(p)]) || isMatch(s, p[2:len(p)])
			}
			//p[0] == s[0]이고 p[0]는 '.'이 아님 즉, a* case
			return isMatch(s, p[0:1]+p[2:len(p)]) || isMatch(s[1:len(s)], p) || isMatch(s, p[2:len(p)])
		}
	}

	if s[0] == p[0] || p[0] == '.' {
		return isMatch(s[1:len(s)], p[1:len(p)])
	}
	return false
}
```
- 제가 푼 solution은 재귀함수를 이용해서 풀었고, 성능적으로는 좋지 않은 결과지만 leetcode test는 통과되었습니다.
- 예외 케이스가 굉장히 많이 발견이 되어 해당 부분을 처리하는가 고생을 했습니다.
- 3번째 if문까지는 s가 0일때와 p가 0일때를 구분하여 처리를 했습니다.
- len(p) > 1이고 p[1] == ```'*'```인 경우에는 두번째 값에 ```*```이 존재하는 경우로 ```.*,a*,b*```등을 모두 포함합니다.
- 각 각의 Case에 대해서 s[0]와 같을 경우와 다를경우를 나누었습니다. 같은 경우에는 뒤의 if이 있으므로 적절한 재귀함수를 통해서 처리를 하였습니다.
- 다를 경우에는 (.이 아닌) ```*```은 길이가 0가 될수 있으므로 패턴에서 ```*``` 부분을 제외하는 경우를 다시 검사합니다. 
- p[0] 값이 .일경우 s의 길이가 1이고 p의 길이가 0일 경우에는 .의 정의상 자명하므로 true 값을 리턴합니다.
- p[0]가 .이면서 s의 길이가 1 이상일 경우 총 3가지의 경우를 검수합니다. 
  - .이므로 s[0]를 대처할 수 있으므로 s의 길이를 줄이고, p[1]이 ```*```이므로 패턴은 그대로 하여 검사
  - p[1]이 ```*```이므로 길이가 1이 될 수 있으므로(. 하나) 이에 대한 검사
  - p[1]이 ```*```이므로 길이가 0이 될 수 있으므로 이에 대한 검사
- 그 이후에는 p[0]가 .이 아닌 경우 입니다.
- 즉 p[0] == s[0]이고 p[0]는 '.'이 아닌 case 입니다.
- 이 경우에도 총 3가지의 경우를 검수 합니다.
  - ```*```을 삭제한 패턴과의 검수
  - 연속된 ```*```의 패턴(길이가 2이상의 문자열)과의 검수 
  - 길이가 0인 경우에 대한 검수
- ```*```과 ```.```의 경우를 모두 검수하고 나서 그 이후에는 단순히 문자 단위의 비교를 진행합니다.
- 모든 경우에도 걸리지 않았을 상황은 문자와 패턴이 서로 다른 경우 이므로 false를 리턴합니다.

- Dynamic programming을 통하여도 구현이 가능해 보이는데 이부분에 대해서는 좀 더 고민이 필요합니다.

