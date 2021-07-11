### Count of Smaller Numbers After Self
#### Writer: Hyungjune Shin
#### Refer: LeetCode (Hard)
* * *
### Problem
You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

<b>Example 1</b>
<pre>
<b>Input</b>: nums = [5,2,6,1]
<b>Output</b>: [2,1,1,0]
<b>Explanation</b> 
To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: nums = [-1]
<b>Output</b>: [0]
</pre>

<b>Example 3</b>
<pre>
<b>Input</b>: nums = [-1,-1]
<b>Output</b>: [0,0]
</pre>

#### Constraints
- 1 <= nums.length <= 10^5
- -10^4 <= nums[i] <= 10^4

### Solution
#### Using recursion
```java
class Solution {
    public List<Integer> countSmaller(int[] nums) {
      if(nums.length == 1) {
        List<Integer> result = new ArrayList<>();
        result.add(0);
        return result;
      }

      int compare = nums[0];
      int count = 0;
      for(int i=1; i<nums.length; i++){
        if(compare > nums[i]) count++;
      }
      List<Integer> result = new ArrayList<>();
      result.add(count);
      result.addAll(
        countSmaller(Arrays.copyOfRange(nums, 1, nums.length))
      );
      return result;
    }
}
```
- Extract a number in the index 0. We call it as the comparing number.
- compare it with other numbers in the nums array
- When comparing the numbers, the count increase if the other numbers are bigger than the comparing number.
- When adding the count to the result array, the 'countSmaller' function recursively runs it-self with the nums array except the comparing num.
- The warst timecomplexity is O(n^2) -> O(n) (The comparing for loop) * O(n) (The number of recursive invokations)
#### Using slice windows
```java
class Solution {
    public List<Integer> countSmaller(int[] nums) {
        int[] result = new int[nums.length];
		for(int i = 0; i < result.length; i++ ) {
			result[i] = 0;
		}
		for(int windowSize = 2;windowSize<=nums.length;windowSize++){
			for(int windowIndex = 0; windowIndex-1 + windowSize < nums.length; windowIndex++) {
				if(nums[windowIndex] > nums[windowIndex+windowSize-1]) result[windowIndex]++;
			}
		}

		List<Integer> resultList = new ArrayList<>();
		for(int i = 0;i< result.length;i++) {
			resultList.add(result[i]);
		}

		return resultList;
    }
}
```
- The windowSize is 2 ~ nums.length
- We compare first element and last element in the window.
- In the code, the index of the first element is windowIndex and the last element is (windowIndex+windowSize-1)
- It is the same with when we compare all elements in the nums array by using double loops
- It has the O(n^2) timecomplexity

#### Using Merged Array (Merge Sort)
```java
class Solution {
    public List<Integer> countSmaller(int[] nums) {
        if(nums == null || nums.length == 0) {
            return List.of();
        }
        int n = nums.length;
        Element[] elements = new Element[n];
        for(int i = 0; i < n ;i++) {
            elements[i] = new Element(i, nums[i]);
        }
        
        int[] result = new int[n];
        countSmallerByMerge(elements, 0, n-1, result);
        return Arrays.stream(result).boxed().collect(Collectors.toList());
    }
    
    public void countSmallerByMerge(Element[] elements, int start, int end, int[] result) {
        if(start >= end) return;
        int mid = (start + end) / 2;
        countSmallerByMerge(elements, start, mid, result);
        countSmallerByMerge(elements, mid+1, end, result);
        
        int left = start;
        int right = mid+1;
        
        int count = 0;
        List<Element> mergedList = new LinkedList<>();
        
        while(left < mid + 1 && right <= end) {
            if(elements[left].value > elements[right].value) {
                count++;
                mergedList.add(elements[right]);
                right++;
            } else {
                result[elements[left].index] += count;
                mergedList.add(elements[left]);
                left++;
            }
        }
        
        while(left < mid + 1) {
            result[elements[left].index] += count;
            mergedList.add(elements[left]);
            left++;
        }
        
        while(right <= end) {
            mergedList.add(elements[right]);
            right++;
        }
        
        int pos = start;
        for(Element element : mergedList) {
            elements[pos] = element;
            ++pos;
        }
    }
    private class Element {
        int index;
        int value;
        public Element(int index, int value) {
            this.index = index;
            this.value = value;
        }
    }
}
```
- While the nums array is sorted, the function count smallers. 
- Since the nums array is sorted, original index should be saved. Therefore, Element class is defined.
- The nums array is replaced with the Element array.
- The recursive function calls 'countSmallerByMerge(elements, start, mid, result)' and 'countSmallerByMerge(elements, mid+1, end, result)' are invoked untile start >= mid and mid+1 >= end respectively.
- By the recursive function calls, the elements array is seperated to multiple small partial arrays.
- The minimum size of the elements partial array for going inside of 'while(left < mid + 1 && right <= end)' is 2
- The variable 'left' is the first index of the partial array.
- The variable 'right' is the mid index of the partial array.
- When the value of the element[left] is bigger than the element[right], 'count' variable and 'right' variable increase and element[right] is sorted by using mergedList.
- When the value of the element[left] is smaller than the element[right],  the count variable is added to the result with the index of the elements[left], the left variable increase, and the element[left] is sorted by using mergedList.
- If we sort the elements ascending order, we can expect that if first element in the left part is bigger than all in the right part, then we do not need to compare other elements in the left part with in the right part.

- while loop: 
```java
while(left < mid + 1) {
    result[elements[left].index] += count;
    mergedList.add(elements[left]);
    left++;
}
```
- It means that since all elements in the right part are smaller than the left, comparing other elements in the left part with all elements in the right part does not needed in the ascending ordered array. Therefore, add the count to the other left element's value
