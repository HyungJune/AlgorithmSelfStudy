
### Longest Common Prefix
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
주어진 문자열 배열에서 가장 긴 공통의 prefix string을 구하는 함수를 작성해야 합니다.   
만약 존재하지 않는다면, 빈 문자열인 ""를 출력값으로 가져야 합니다.

<b>Example 1</b>
<pre>
<b>Input</b>: ["flower","flow","flight"]
<b>Output</b>: "fl"
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: ["dog","racecar","car"]
<b>Output</b>: ""
<b>Explanation</b>: There is no common prefix among the input strings.
</pre>
* * *
### Solution
```go
func longestCommonPrefix(strs []string) string {
    result := ""
    i := 0
    if len(strs) == 0 {
        return ""
    }
    for {
        isFinished := false
        if len(strs[0]) <= i {
            break;
        }
        local := strs[0][i]
        
        for j:=1;j<len(strs);j++{
            if len(strs[j]) <= i {
                isFinished = true
                break;
            }
            
            if local != strs[j][i] {
                isFinished = true
                break;
            } 
        } 
        
        if isFinished != true {
            result += string(local)
            i++
        } else {
            break;
        }
    }
    
    return result
}
```
- 스트링 배열의 길이가 n이므로, 가장 작은 길이의 문자열을 찾고, 이를 기준으로 문자를 비교하는 방식은 여러개의 loop 문을 발생시킵니다.
- 역으로 생각하여, 무한루프를 돌며 전체 스트링 배열에서 한개의 문자끼리 비교하는 방식으로 구현했습니다.
- 이때, index가 밖으로 벗어나지 않도록 중간 중간에 길이에 대한 확인을 진행했습니다.
