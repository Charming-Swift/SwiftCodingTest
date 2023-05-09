# best

배열 요소 두 배 만들기

문제설명
- 정수 배열 numbers가 매개변수로 주어집니다. numbers의 각 원소에 두배한 원소를 가진 배열을 return하도록 solution 함수를 완성해주세요.

---
```
import Foundation

func solution(_ numbers:[Int]) -> [Int] {
    var numbers2:[Int] = []
    for i in 0..<numbers.count{
        numbers2.append(numbers[i]*2)
    }
    return numbers2
}
```
## 다른 사람 풀이
```
func solution(_ numbers: [Int]) -> [Int] { numbers.map { $0 * 2 } }
```

map이라는 메소드를 알게 되었다. 굉장히 유용하게 쓰일 것 같다.
활용도 공유해주시면 감사하겠습니다.
