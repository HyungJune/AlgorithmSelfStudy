
### Dot Product of Two Sparse Vectors
#### Writer: Hyungjune Shin
#### Refer: LeetCode#1570
* * *
### Problem
주어진 두 Sparse Vector에 대해서 dot 연산자를 구현하는 문제입니다.
이때, ``SparseVector`` 클래스를 구현해야합니다.
  - ``SparseVector(nums)``: Vector nums 오브젝트를 초기화하는 함수입니다.
  - ``dotProduct(vec)``: SparseVector의 인스턴스와 ``vec``사이의 dot 연산의 결과를 계산합니다.
  
<b>sparse vector</b>는 대부분 0의 값을 가지는 벡터입니다. sparse vector를 효과적으로 저장해야하며 두 SparseVector사이의 dot 연산을 계산해야합니다.

<b>Example 1:</b>
<pre>
<b>Input:</b> nums1 = [1,0,0,2,3], nums2 = [0,3,0,4,0]
<b>Output:</b> 8
</pre>

<b>Example 2:</b>
<pre>
<b>Input:</b> nums1 = [0,1,0,0,0], nums2 = [0,0,0,0,2]
<b>Output:</b> 0
</pre>

<b>Example 3:</b>
<pre>
<b>Input:</b> nums1 = [0,1,0,0,2,0,0], nums2 = [1,0,0,0,3,0,4]
<b>Output:</b> 6
</pre>

### Constrains: ###
  - ``n == nums1.length == nums2.length``
  - ``1<=n<=10^5``
  - ``0<=nums1[i], nums2[i]<=100``
  
* * *
### Solution
```go
type SparseVector struct {
    value map[int]int
}

func Constructor(nums []int) SparseVector {
    var vector SparseVector
    vector.value = make(map[int]int)
    for i, v := range nums {
        if v != 0 {
            vector.value[i] = v
        }
    }
    return vector
}

// Return the dotProduct of two sparse vectors
func (this *SparseVector) dotProduct(vec SparseVector) int {
    result := 0
    for key, element := range this.value {
        if vec.value[key] != 0 {
            result += (element * vec.value[key])
        }
    }
    return result
}

/**
 * Your SparseVector object will be instantiated and called as such:
 * v1 := Constructor(nums1);
 * v2 := Constructor(nums2);
 * ans := v1.dotProduct(v2);
 */
```

  - 0인 값을 굳이 저장할 필요가 없고, 다만 값에 대응되는 index 값을 저장할 필요가 있으므로 map 구조체를 이용했습니다.
  - Constructor에서는 nums에서 0인 값을 제외한 값들에 대한 index와 값을 vector의 map에 넣고 vector를 리턴합니다.
  - docProduct에서는 this의 value map의 모든 요소를 검토하면서, 혹시 vec의 value map의 key 값이 존재할 경우 dot 연산을 진행하여 결과 값에 더합니다. 이를 반복하여 dot 연산의 결과를 계산합니다.
