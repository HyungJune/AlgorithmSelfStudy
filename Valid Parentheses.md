#### Valid Parentheses 
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
괄호를 나타내는 기호 '(', ')', '{', '}', '[', ']'로만 이루어진 String 타입의 입력값이 들어올 것이다. 이 입력값을 다음 규칙에 따라서 판별하여 Boolean을 반환하라.  
***규칙***  
    1. 열린 괄호는 같은 종류의 괄호로 닫혀야 한다.  
    2. 괄호는 열린 순서의 역순으로 닫혀야한다. (먼저 열린 괄호는 나중에 닫히고, 나중에 열린 괄호가 먼저 닫히고)  
    3. empty string은 유효한 것으로  
***예시1:***  
```
Input: "()"
Output: true
```
***예시2:***
```
Input: "()[]{}"
Output: true"
소괄호가 열렸다가 닫히고, 대괄호가 열렸다가 닫히고, 중괄호가 열렸다가 닫혔으므로 유효하다
```
***예시3:***
```
Input: "(]"
Output: false
소괄호가 열렸는데 같은 종류의 괄호로 닫히지 않아서 무효
```
***예시4:***
```
Input: "([)]"
Output: false
소괄호가 먼저 열렸으니까 나중에 닫혀야하는데 소괄호가 먼저 닫혔으므로 무효
```
***예시5:***
```
Input: {[]}"
Output: true
제대로 중괄호랑 대괄호가 먼저열렸다가 같은 종류로 나중에 닫히니까 유효
```

## 솔루션
```
func isValid(s string) bool {
    if s == "" {
        return true
    } else if len(s)%2 != 0 {
        return false
    }
    
    slice := strings.Split(s, "")
    
    bracketMap := map[string]string{
        ")" : "(",
        "]" : "[",
        "}" : "{",
    }
    
    	lastString := ""
	for i, _ := range slice {
		if slice[i] == "(" || slice[i] == "[" || slice[i] == "{" {
			lastString += slice[i]
			lastString += "_"
		} else if slice[i] == ")" || slice[i] == "]" || slice[i] == "}" {
			val, _ := bracketMap[slice[i]]
			lastString = strings.TrimRight(lastString, "_")
			lastString = strings.TrimRight(lastString, val)
		} else {
			break
		}
	}

    if len(lastString) == 0 {
        return true
    } else {
        return false
    }
}
```
- Empty string이면 true, input string의 길이가 홀수이면 false를 바로 반환
- 일단 input string을 슬라이스하여 배열로 만들고, 그 배열의 길이만큼 반복문을 돌리면서 검사
- Input string을 왼쪽부터 한글자씩 읽는다
    - "(", "[", "{" 세가지 여는 괄호이면, lastString에 누적한다
    - 읽은 글자가 ")", "]", "}" 닫는 괄호이면, 그 짝인 여는 괄호를 TrimRight로 lastString의 맨 오른쪽에서 제거
        - 이를 위해서 ")" : "(", "]" : "[", "}" : "{" 형태로 "닫는 괄호" : "여는 괄호" 를 key : value로 맵핑
- 검사가 끝난 후 마지막에 lastString이 empty string이면 true, 아니면 false를 반환  

## LeetCode의 솔루션 참고 내용
- 이런 작업을 하는데 적합한 것이 stack이었군
```
type StackItem struct {
	item interface{}
	next *StackItem
}

type Stack struct {
	sp    *StackItem // Stack에서 가장 위에 있는 아이템을 저정합니다.
	depth uint64     // Stack에 아이템이 몇개 있는지를 저장합니다.
}

func New() *Stack {
	var stack *Stack = new(Stack)

	stack.depth = 0
	return stack
}

func (stack *Stack) Push(item interface{}) {
	stack.sp = &StackItem{item: item, next: stack.sp}
	stack.depth++
}

func (stack *Stack) Pop() interface{} {
	if stack.depth > 0 {
		item := stack.sp.item
		stack.sp = stack.sp.next
		stack.depth--
		return item
	}

	return nil
}

func (stack *Stack) Peek() interface{} {
	if stack.depth > 0 {
		return stack.sp.item
	}

	return nil
}

func isValid(s string) bool {
    if s == "" {
        return true
    } else if len(s)%2 != 0 {
        return false
    }
    
    slice := strings.Split(s, "")
    
    bracketMap := map[string]string{
        ")" : "(",
        "]" : "[",
        "}" : "{",
    }
    
    var bracketStack *Stack = New()
    
    for i, _ := range slice {
        if slice[i] == "(" || slice[i] == "{" || slice[i] == "[" {
            bracketStack.Push(slice[i])
        } else if slice[i] == ")" || slice[i] == "}" || slice[i] == "]" {
            val, _ := bracketMap[slice[i]]
            if bracketStack.Peek() == val {
                bracketStack.Pop()
            }
        } else {
            break;
        }
    }
    
    if bracketStack.depth == 0 {
        return true
    } else {
        return false
    }
}
```
