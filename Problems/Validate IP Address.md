### Validate IP Address 
#### Writer: Hyungjune Shin
#### Refer: LeetCode#468
* * *
### Problem
input string이 IPv4 형식인지, IPv6 형식인지 확인하는 함수를 구현해야합니다.

<b>IPv4</b> 주소체계는 dot-decimal 표기법으로 표현되며, 0-255의 범위를 가지는 4개의 10진수 숫자와 각 각의 숫자를 구별하는 dot(".")으로 구성됩니다. 예를 들면, 172.16.254.1은 IPv4 주소체계를 가집니다. 추가로 0으로 시작되는 10진수 숫자가 존재할 경우에는 IPv4 주소체계에 맞지 않게됩니다. 예를 들면 172.16.254.01은 IPv4 주소체계가 아닙니다.

<b>IPv6</b> 주소체계는 16bit를 표현하는 4자리의 16진수 수로 구성된 8개의 부위를 가집니다. 각 부위는 colons(":")으로 구별됩니다. 예를 들면 2001:0db8:85a3:0000:0000:8a2e:0370:7334는 IPv6 주소체계입니다. 또한, 앞자리에 0으로 시작되는 부분은 생략가능하며 대소문자 구별이 없습니다. 예를 들면 2001:db8:85a3:0:0:8A2E:0370:7334는 IPv6 주소체계입니다.

하지만, 0 값을 가진 부위를 ::으로 비어 있는 공간으로 만들 수는 없습니다. 예를 들면 2001:0db8:85a3::8A2E:0370:7334는 IPv6 주소가 아닙니다.
또한 추가적인 0을 앞에 붙였을 경우에도 IPv6 주소가 아닙니다. 예를 들면 02001:0db8:85a3:0000:0000:8a2e:0370:7334는 IPv6 주소가 아닙니다.

<b>Example1</b>
<pre>
<b>Input</b>: IP = "172.16.254.1"
<b>OutPut</b>: "IPv4"
</pre>

<b>Example2</b>
<pre>
<b>Input</b>: IP = "2001:0db8:85a3:0:0:8A2E:0370:7334"
<b>OutPut</b>: "IPv6"
</pre>

<b>Example3</b>
<pre>
<b>Input</b>: IP = "256.256.256.256"
<b>OutPut</b>: "Neither"
</pre>

* * *
### Solution
```go
func validIPAddress(IP string) string {
    if strings.Count(IP, ".") == 3 {
        return validIPv4Address(IP)
    }
    
    if strings.Count(IP, ":") == 7 {
        return validIPv6Address(IP)
    }
    
    return "Neither"
}

func validIPv4Address(IP string) string {
    var digitCheck = regexp.MustCompile(`^[0-9]+$`)
    nums := strings.Split(IP, ".")
    for _, num := range nums {
        if len(num) > 3 || len(num) == 0 {
            return "Neither"
        }
        
        if len(num) != 1 && num[0] == '0' {
            return "Neither"
        }
        
        if digitCheck.MatchString(num) == false {
            return "Neither"
        }
        
        if e, _ := strconv.Atoi(num); e>255 {
            return "Neither"
        }
    }
    
    return "IPv4"
}

func validIPv6Address(IP string) string {
    nums := strings.Split(IP, ":")
    var hexCheck = regexp.MustCompile(`^[0-9A-Fa-f]+$`)
    for _, num := range nums {
        if len(num) == 0 || len(num) > 4 {
            return "Neither"
        }
        
        if hexCheck.MatchString(num) == false {
            return "Neither"
        }
    }
    
    return "IPv6"
}
```
- strings.Count 함수를 이용하여 "."의 갯수 혹은 ":" 갯수를 확인합니다. 이후 IPv4와 IPv6에 해당하는 함수를 부르게 됩니다.
- 두 함수의 로직은 비슷하며, 특이한 부분은 regexp를 통해서 확인하는 부분이 조금 다르다는 점입니다.
- IPv4 같은 경우 각 digit의 범위를 추가로 확인해야 합니다. 또한 leading zero가 존재하는지 확인해야 합니다.


