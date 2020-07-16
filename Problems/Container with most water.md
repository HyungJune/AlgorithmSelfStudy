### Container with most water
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
각 각의 (i, A_i) 좌표를 가르키는 n개의 양수(A_1,A_2,...,A_n)가 주어졌을 때, n개의 수직 선들을 (i,A_i)와 (i,0)를 잇는 i 라인으로 그려질 수 있습니다. 이때 x 좌표와 같이하여 상자를 만들 때 가능한 담을 수 있는 가장 많은 양의 물은 얼마인지 구하는 프로그램을 작성해야 합니다.

<img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg" width="90%"></img>

<b>Example</b>
<pre>
<b>Input</b>: [1,8,6,2,5,4,8,3,7]
<b>Output</b>: 49
</pre>


### Solution
#### Brute-Force 방식
```go
func maxArea(height []int) int {
  max := 0
    for i:=0;i<len(height);i++{
        for j:=i+1;j<len(height);j++{
            var h int
            if height[i] > height[j] {
                h = height[j]
            } else {
                h = height[i]
            }
            w := j-i
            area := h * w
            if area > max {
                max = area
            }
        }
    }
    
    return max
}
```
- 전수조사 방식으로, 가능한 모든 물의 양을 구하고 max를 리턴합니다.

#### Two Point를 이용한  방식
```go
func maxArea(height []int) int {
    left := 0
    right := len(height) -1
    max := 0
    for left < right {
        h := int(math.Min(float64(height[left]), float64(height[right])))
        max = int(math.Max(float64(max),float64(h*(right-left))))
        if height[left] > height[right] {
            right--
        } else {
            left++
        }
        
    }
    return max
}
```
- left와 right 두 point를 이용하여 구현한 방법입니다.
- 두 point에 대한 area를 구한 뒤, 작은 높이를 가진 point를 움직이면서 max area를 찾는 방식입니다.
- 한번의 loop 문을 통하여 계산되기에 위의 brute-force 방식보다 효과적입니다.
