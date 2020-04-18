### Regular Expression Matching
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
주어진 입력 스트링 값 s와 패턴 p에 대해서 ```'.'```과```'*'```를 지원하면서 정규표현식이 맞는지 확인하는 알고리즘을 구현해야 합니다.   

```
'.'은 어떤 하나의 문자에 매칭됩니다.
'*'은 길이가 0 또는 그 이상의 연속된 문자들에 매칭됩니다.
```
매칭은 전체 인풋 string을 다뤄야 합니다. (부분적으로만 다루어서는 안됩니다.)

<b>Node</b>
  - ```s```는 비어있을 수 있으며 오직 소문자 형태의 문자(a-z)만을 포함합니다.
  - ```p```는 비어있을 수 있으며 오직 소문자 형태의 문자(a-z)와 ```.```과 ```*```을 포함합니다.

<b>Example 1</b>
<pre>
<b>Input</b>:
s = "aa"
p = "a"
<b>Output</b>: false
<b>Explanation</b>: "a" does not match the entire string "aa".
</pre>
