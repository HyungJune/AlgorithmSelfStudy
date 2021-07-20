### Group Anagrams
#### Writer: Donggyu Cho
#### Refer: LeetCode#49 (Medium)
* * *
### Problem
Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

<b>Example 1</b>
<pre>
<b>Input</b>: strs = ["eat","tea","tan","ate","nat","bat"]
<b>Output</b>: [["bat"],["nat","tan"],["ate","eat","tea"]]
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: strs = [""]
<b>Output</b>: [[""]]
</pre>

<b>Example 3</b>
<pre>
<b>Input</b>: strs = ["a"]
<b>Output</b>: [["a"]]
</pre>


#### Constraints
- 1 <= strs.length <= 104
- 0 <= strs[i].length <= 100
- strs[i] consists of lower-case English letters.

### Solution
```golang
func groupAnagrams(strs []string) [][]string {

	primes := []int{2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 73, 79, 83, 89, 97, 101, 103, 107, 109, 113, 127}
	answer := make(map[int][]int)
	output := make([][]string, 0)

	for i, v := range strs {
		var key int = 1
		// v, _ = strconv.Unquote(v)
		for _, t := range []byte(v) {
			key = key * primes[t-97]
		}
		if _, exist := answer[key]; !exist {
			answer[key] = make([]int, 0)
		}
		answer[key] = append(answer[key], i)
	}
	var i int = 0
	for _, v := range answer {
		output = append(output, make([]string, 0))
		for _, item := range v {
			output[i] = append(output[i], strs[item])

		}
		i = i + 1
	}
	return output
}
```

- Anagram에서 같은 Group에 속하는 element들은 같은 종류의 알파벳으로 이루어지며 순서는 상관이 없음
- 즉, 알파벳 하나하나의 조합이 Unique한 특성을 지닌다 라는 점에서 소수(Prime number)에 대한 생각이 떠오름
- 각 알파벳을 소수와 매핑하기 위해 24개의 소수가 적힌 배열을 이용하여 문제 해결 
