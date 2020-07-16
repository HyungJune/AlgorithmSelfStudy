#### Longest Substring Without Repeating Characters
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
주어진 문자열로 만들 수 있는 substring 중에서 가장 긴 substring의 길이를 구하라.  
***예시***
```
Input: "abcabcbb"
Output: 3
이유: "abc"든 "bca"든 "cab"든. 길이는 3.
```
```
Input: "bbbbb"
Output: 1
이유: "b"
```
```
Input: "pwwkew"
Output: 3
이유: "wke"
```
```
Input: "dvdf"
Output: 3
이유: "vdf"
```

## 솔루션
```
func lengthOfLongestSubstring(s string) int {
    if len(s) == 1 {
        return 1
    }
	size := 0
	s2Slice := strings.Split(s, "")
	var examination []string

	for i := 0; i < len(s)-1; i++ {
		examination = append(examination, s2Slice[i])
		if flag, index := Contains(examination, s2Slice[i+1]); !flag {
			if i+1 == len(s)-1 {
				examination = append(examination, s2Slice[i+1])
				size = Max(size, len(examination))
			}
		} else {
			size = Max(size, len(examination))
			examination = examination[index+1:]
		}
	}
	return size
}

func Contains(slice []string, val string) (bool, int) {
	for i, item := range slice {
		if item == val {
			return true, i
		}
	}
	return false, 0
}

func Max(x, y int) int {
	if x >= y {
		return x
	} else {
		return y
	}
}
```
- Input 문자열을 앞에서부터 한글자 떼어서 누적시키고, 다음 글자가 들어있는지를 검사
    - 1) 들어있지 않으면(false), 다른 액션을 취하지 않고 다음 글자를 누적
    - 2) 틀어있으면 (true), 누적된 문자열 중에서 처음~그 글자가 있는 인덱스까지를 제거하고 나머지만 남긴다
        - 제거하기 전에 누적된 문자열 길이를 저장하는데, 이전의 문자열 길이와 현재 문자열 길이 중 큰 값을 남김
    - 만약 마지막 한글자가 남았으면(그리고 false)인 경우이면 마저 누적하고, 사이즈를 구함
    - 한글자인 입력값에 대해서는 바로 1을 반환(for문에 들어가지 못하므로)
