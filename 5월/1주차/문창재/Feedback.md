# feedback

## 분수의 덧셈
문제 설명

- 첫 번째 분수의 분자와 분모를 뜻하는 numer1, denom1, 두 번째 분수의 분자와 분모를 뜻하는 numer2, denom2가 매개변수로 주어집니다. 두 분수를 더한 값을 기약 분수로 나타냈을 때 분자와 분모를 순서대로 담은 배열을 return 하도록 solution 함수를 완성해보세요.
---

```
import Foundation

func solution(_ numer1:Int, _ denom1:Int, _ numer2:Int, _ denom2:Int) -> [Int] {
    var numer3, denom3:Int // 두 분수 덧셈의 결과
    var num3:[Int] = [] // 결과 분자의 약수
    var de3:[Int] = [] // 결과 분모의 약수
    var same:[Int] = [] // 공약수
    var lastIndex:Int // 최대공약수
    numer3 = (numer1 * denom2) + (numer2 * denom1)
    denom3 = denom2 * denom1
    for i in 1...numer3 {
        if numer3 % i == 0{
            num3.append(i)
        }
    }
    for i in 1...denom3 {
        if denom3 % i == 0{
            de3.append(i)
        }
    }
    for i in num3{
        if de3.contains(i){
            same.append(i)
        }
    }
    lastIndex = same.count - 1
    return [(numer3/same[lastIndex]),(denom3/same[lastIndex])]
}
```
## 다른 사람의 풀이

```
import Foundation

func solution(_ denum1:Int, _ num1:Int, _ denum2:Int, _ num2:Int) -> [Int] {
    let boonja = denum1 * num2 + denum2 * num1
    let boonmo = num1 * num2
    let gcd = (1...min(boonja, boonmo)).filter { boonja % $0 == 0 && boonmo % $0 == 0 }.max()!
    return [boonja/gcd, boonmo/gcd]
}

```
1부터 분자 분모 중 더 작은 수까지 배열 생성 후 .filter 메소드를 사용해 조건에 맞는 요소만으로 이루어진 배열 재생성, .max()로 최대공약수


## 더 나은 방법?
 
n의 제곱근까지만 나누어 떨어지는지 확인하여 약수를 찾는 코드입니다.

```
import Foundation

func findDivisors(of n: Int) -> [Int] {
    var divisors = [Int]()
    let sqrtN = Int(sqrt(Double(n)))
    
    for i in 1...sqrtN {
        if n % i == 0 {
            divisors.append(i)
            if i != n/i {
                divisors.append(n/i)
            }
        }
    }
    
    return divisors.sorted()
}
```

위의 코드에서는 sqrtN에 n의 제곱근을 저장합니다. 그리고 1부터 sqrtN까지 반복하면서 n이 현재의 수로 나누어 떨어지는지 확인합니다. 만약 나누어 떨어진다면 현재의 수와 n을 현재의 수로 나눈 몫을 약수 리스트에 추가합니다. 마지막으로 약수 리스트를 정렬하여 반환합니다. 이 코드는 O(sqrt(n))의 시간 복잡도를 가지므로, n이 매우 큰 경우에도 효율적으로 약수를 찾을 수 있습니다.

- 잘 이해가 안되는 부분,, 효율적인 코드란 어떤 코드인가
