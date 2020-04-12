#### Palindrome Number
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
단어를 똑바로 읽었을 때와 거꾸로 읽었을 때가 같은 경우를 palindrome이라고 한다. 주어진 정수가 palindrome인 경우 true, 아닌 경우 false를 반환해야 함

## 예시와 조건
- 121은 거꾸로 읽어도 121이므로 true
- -121은 거꾸로 읽으면 121-이므로 false
    - 나중에 알았지만 정수 중 음수는 모두 false라고 할 수 있다고 함
- 10은 거꾸로 읽으면 01이므로 false

## 솔루션
```
func isPalindrome(x int) bool {
    s := strconv.Itoa(x)
    slice := strings.Split(s, "")
    var replace []string
    replace = make([]string, len(slice))
    for i := 0; i < len(slice); i++ {
        replace[i] = slice[len(slice) - 1 - i]
    }
    r := strings.Join(replace, "")
    if s == r {
        return true
    } else {
        return false
    }
}
```
- go 언어 사용
- 이 역시 단순하게 string으로 변환하여, split 함수를 사용하여 한글자씩 자른 후, 거꾸로 이어붙여서 처음의 문자열과 비교하는 방식을 사용
- accept은 되었으나, 문자열로 바꾸지 않고 비교할 수 있는지를 LeetCode에서 제시

## LeetCode 솔루션 참고내용
```
func isPalindrome(x int) bool {
    if x < 0 || ( x % 10 == 0 && x != 0 ) {
        return false
    }
    
    revert := 0
    for x > revert {
        revert = revert*10 + x%10
        x /= 10
    }
    
    return x == revert || x == revert/10
}
```
- 정수가 0보다 작거나, 10의 배수인 경우는 false
- 정수를 거꾸로 읽은 반을 자르는 방법으로 원래의 정수 x를 10으로 나눈 나머지를 각각 1의 자리, 10의 자리로 사용하는 방법을 사용
- 그렇게 나온 revert 정수를 원래의 정수와 비교, 원래의 정수 x의 길이가 홀수인 경우에는 revert가 한자리 더 길게되는데 이때 맨 마지막 자리를 버린 값이 원래의 정수 x와 같으면 true
