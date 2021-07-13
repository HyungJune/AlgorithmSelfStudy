### Isomorphic Strings
#### Writer: Haram Ryu
#### Refer: LeetCode#205 (Easy)
* * *
### Problem
Given two strings s and t, determine if they are isomorphic.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.



<b>Example 1</b>
<pre>
<b>Input</b>: s = "egg", t = "add"
<b>Output</b>: true
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: s = "foo", t = "bar"
<b>Output</b>: false
</pre>

<b>Example 3</b>
<pre>
<b>Input</b>: s = "paper", t = "title"
<b>Output</b>: true
</pre>

#### Constraints
- 1 <= s.length <= 5 * 104
- t.length == s.length
- s and t consist of any valid ascii character.

### Solution
```golang
func isIsomorphic(s string, t string) bool {
    m := make(map[byte]byte)
    
    for i, _ := range s {
        val, exists := m[s[i]]
        if !exists {
            m[s[i]] = t[i]
        } else if exists && val != t[i] {
            return false
        }
    }
    m = make(map[byte]byte)

    for i, _ := range t {
        val, exists := m[t[i]]
        if !exists {
            m[t[i]] = s[i]
        } else if exists && val != s[i] {
            return false
        }
    }
    return true    
}
```
- map을 활용하여 s 문자열의 알파벳과 같은 인덱스에 있는 t 문자열의 알파벳을 map에 저장
- s 문자열 전체에 대해 한번 훑으면서 이미 저장한 알파벳의 경우에는 해당 인덱스의 t 문자열 알파벳이 저장된 값과 같은지 비교
- 다르면 무조건 false
- 근데 t 문자열의 경우에도 검사해야하는게.. 이렇게 하는게 맞나 싶음
