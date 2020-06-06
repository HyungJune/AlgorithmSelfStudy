#### Climbing Stairs
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
n개의 층계를 가진 계단을 오르는데, 한번에 1칸 또는 2칸씩 올라간다고 했을 때, 계단을 오를 수 있는 경우의 수를 구한다.

***예시***
```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```
```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

## 솔루션1(재귀적인 방법)
- 첫번째 걸음을 1걸음 가거나 2걸음 갈 수 있다.
    - 1걸음 가면 남은 계단이 n-1개이므로, 그 상황에서 경우의 수는 n-1개의 층계를 오르는 경우의 수와 같다.
    - 2걸음을 가고 난 후의 경우의 수는 n-2개의 층계를 오르는 경우의 수와 같다.
    - 즉, n개의 계단을 오르는 경우의 수는 n-1개 계단을 오르는 경우의 수 + n-2개의 계단을 오르는 경우의 수와 같다.
```
func climbStairs(n int) int {
    if n == 1 {
        return 1
    } else if n == 2 {
        return 2
    } else if n == 3 {
        return 3
    } else if n == 4 {
        return 5
    } else if n == 5 {
        return 8
    } else if n == 6 {
        return 13
    }
    return climbStairs(n-1) + climbStairs(n-2)
}
```
- 재귀적으로 함수를 동작시키면 시간이 오래걸려서, 첫 몇가지 경우를 미리 입력해줘야 LeetCode에서 accept이 됐다.
- 위의 코드의 경우에도 시간이 3초나 걸린다고 나옴..
## 솔루션2(피보나치 수열)
- f(n)=f(n-1)+f(n-2) 이고, f(1)=1, f(2)=2인 이 경우는 피보나치 수열의 일부라고 볼 수 있다.
```
func climbStairs(n int) int {
    
    return FibonacciLoop(n)
}

func FibonacciLoop(n int) int {
    f := make([]int, n+1, n+2)
    if n < 2 {
        f = f[0:2]
    }
    f[0] = 1
    f[1] = 2
    for i := 2; i <= n; i++ {
        f[i] = f[i-1] + f[i-2]
    }
    return f[n-1]
}
```
- 피보나치 수열을 계산하는 함수를 만들어서, 초기값이 1, 2일 때 n번째 항을 구함.
