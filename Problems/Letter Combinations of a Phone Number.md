### Letter Combinations of a Phone Number
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.
LINK: https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png

#### Constraints
- 0 <= digits.length <= 4
- digits[i] is a digit in the range ['2', '9'].

### Solution
```java
class Solution {
    public List<String> letterCombinations(String digits) {
		List<String> result = new ArrayList<>();
		if(digits.length() == 0) return result;
		char[] digitsChars = digits.toCharArray();
		char candidate = digitsChars[0];
		if(digits.length() == 1) {
			return singleCharCandidates(candidate);
		}
		List<String> combinations = letterCombinations(digits.substring(1));
		for(String combination : combinations) {
			List<String> singleResult = singleCharCandidates(candidate);
			for(String r : singleResult) {
				result.add(r + combination);
			}
		}

		return result;
    }
    
    private List<String> singleCharCandidates(char candidate) {
		int digit = candidate-48;
		List<String> result = new ArrayList<>();
		if(digit < 7) {
			for (int j = (47 + 2 * (digit - 2)); j < 50 + 2 * (digit - 2); j++) {
				String r = String.format("%c", candidate + j);
				result.add(r);
			}
		} else if (digit == 7) {
			for (int j = 57; j < 61; j++) {
				String r = String.format("%c", candidate + j);
				result.add(r);
			}
		} else if (digit == 8) {
			for (int j = 60; j < 63; j++) {
				String r = String.format("%c", candidate + j);
				result.add(r);
			}
		} else {
			for (int j = 62; j < 66; j++) {
				String r = String.format("%c", candidate + j);
				result.add(r);
			}
		}
		return result;
	}
}
```
- The solution uses the recursive function.
- The function 'singleCharCandidates' returns the candidates which a digit can have.
- After extracting the most significant digit, the function 'letterCombinations' recursively invokes itself with other digits.
- the function 'letterCombinations' calcuates all combinations by attaching the result of 'singleCharCandidates' of the most significant digit infront to the output of the itself's invokation with other digits.  
