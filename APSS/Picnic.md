### Picnic
#### Writer: Hyungjune Shin
#### Refer: APSS
* * *
### Problem
한 학교에서 소풍을 가는데, 두 명씩 짝을 지어 행동하게 하려고 합니다. 다만 서로 친구가 아닌 학생들끼리 짝을 지어주면 서로 다투기 때문에, 항상 서로 친구인 학생들끼리만 짝을 지어야 합니다.   
각 학생들의 쌍에 대해 서로 친구인지 여부가 주어질 경우 학생들을 짝 지을 수 있는 방법의 수를 계산하는 프로그램 작성하는 문제입니다.

- 짝이되는 학생들끼리 다르더라도 다른 방법으로 봅니다. 예를 들면 다음의 두가지 방법은 서로 다른 방법입니다.
  - (0, 1) (2, 3) (4, 5)
  - (0, 1) (2, 5) (3, 4)
- 입력
  - 입력의 첫 줄에는 테스트 케이스의 수 C(C<=50)가 주어집니다. 
  - 각 테스트 케이스의 첫 줄에는 학생의 수 n (2<=n<=10)과 친구 쌍의 수 m (0<=m<=n(n-1)/2)가 주어집니다. 
  - 번호는 모두 0부터 n-1 사이의 정수이며 같은 쌍은 입력에 두 번 주어지지 않습니다. 
  - 학생들의 수는 짝수입니다.
- 출력
  - 각 테스트 케이스마다 한 줄에 모든 학생을 친구끼리만 짝지어 줄 수 있는 방법의 수를 출력해야 합니다.
- 예제 입력
```
3
2 1
0 1
4 6
0 1 1 2 2 3 3 0 0 2 1 3
6 10
0 1 0 2 1 2 1 3 1 4 2 3 2 4 3 4 3 5 4 5
```
- 예제 출력
```
1
3
4
```
### Solution
우선 문제를 입력 받아야 하므로 입력 방식에 대해서 구현을 해야합니다.
```go
type Problem struct {
	numOfStudents int
	numOfFriends  int
	relationShip  []int
}
```
우선 저는 Problem이라는 객체를 만들어서 여러가지의 케이스를 받을 수 있도록 구성했습니다.
```go
func main() {
	var numOfQuestionString string
	fmt.Scanln(&numOfQuestionString)
	numOfQuestion, _ := strconv.Atoi(numOfQuestionString)
	questions := []Problem{}
	for i := 0; i < numOfQuestion; i++ {
		var numOfStudents int
		var numOfFriends int
		scanner := bufio.NewScanner(os.Stdin)
		if scanner.Scan() {
			line := scanner.Text()
			lineSlice := strings.Split(line, " ")
			numOfStudents, _ = strconv.Atoi(lineSlice[0])
			numOfFriends, _ = strconv.Atoi(lineSlice[1])
		}

		p := Problem{}
		p.numOfFriends = numOfFriends
		p.numOfStudents = numOfStudents

		var relationShip []int
		if scanner.Scan() {
			line := scanner.Text()
			lineSlice := strings.Split(line, " ")
			for j := 0; j < len(lineSlice); j++ {
				n, _ := strconv.Atoi(lineSlice[j])
				relationShip = append(relationShip, n)
			}
		}
		p.relationShip = relationShip
		questions = append(questions, p)
	}

	for i := 0; i < numOfQuestion; i++ {
		fmt.Println(answer(questions[i]))
	}
}
```
main 문에서는 questions라는 이름의 Problem 형 슬라이스를 만들어서 문제를 받을 수 있도록 했습니다.
아래의 answer 함수가 이번 문제의 해답을 알려주는 역할을 합니다.

```go
func answer(problem Problem) int {
	var taken [10]bool

	var areFriends [10][10]bool

	for i := 0; i < len(problem.relationShip); i += 2 {
		areFriends[problem.relationShip[i]][problem.relationShip[i+1]] = true
	}

	//countPairings
	return countPairing(taken, problem.numOfStudents, areFriends)
}
```
taken이라는 변수는 짝이 지어진 학생들을 true로 표시하기 위한 변수입니다.
areFriends 변수는 i와 j 학생이 서로 친구관계인지를 표시해주는 변수입니다.
문제의 값을 활용하여 두 변수로 재구성했습니다.


책에서 제공하는 solution을 go언어로 재구성했을 경우 다음과 같습니다.
```go
func countPairing(taken [10]bool, n int, areFriends [10][10]bool) int {
	firstFree := -1
	for i := 0; i < n; i++ {
		if !taken[i] {
			firstFree = i
			break
		}
	}

	if firstFree == -1 {
		return 1
	}

	ret := 0

	for pairWith := firstFree + 1; pairWith < n; pairWith++ {
		if !taken[pairWith] && areFriends[firstFree][pairWith] {
			taken[firstFree], taken[pairWith] = true, true
			ret += countPairing(taken, n, areFriends)
			taken[firstFree], taken[pairWith] = false, false
		}
	}
	return ret
}
```
중복을 피하기 위해 index가 가장 작은 애를 먼저 짝을 지어주는 방식으로 동작합니다. 
firstFree 변수는 현재 taken 변수 상태에서 아직 짝이 없는 애들 중 가장 작은 값(학생)을 가집니다.
firstFree와 짝을 지을 pairWith를 찾습니다. 이때 areFriends 변수를 활용하며, 재귀함수를 통하여 가능한 모든 수를 검색합니다.

---
해당 풀이로 풀었을 경우 책에서 제공하는 특수한 경우일 때 다른 해답이 나옵니다.
```
1
4 6
0 1 1 2 2 3 3 0 0 2 1 3
```
위의 Case일 경우 예제 출력 값으로는 3이나와야 하는데, 실제 프로그램에서는 2가 나옵니다.
다른 Case일 경우는 정상 출력이 됩니다.
