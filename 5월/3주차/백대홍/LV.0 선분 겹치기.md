# LV.0 선분 겹치기(실패)

LV.0 선분 겹치기(실패)

[https://school.programmers.co.kr/learn/courses/30/lessons/120876](https://school.programmers.co.kr/learn/courses/30/lessons/120876)

---

### **문제 설명**

선분 3개가 평행하게 놓여 있습니다. 세 선분의 시작과 끝 좌표가 [[start, end], [start, end], [start, end]] 형태로 들어있는 2차원 배열 `lines`가 매개변수로 주어질 때, 두 개 이상의 선분이 겹치는 부분의 길이를 return 하도록 solution 함수를 완성해보세요.

`lines`가 [[0, 2], [-3, -1], [-2, 1]]일 때 그림으로 나타내면 다음과 같습니다.

![https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/e4122d8b-9ce2-49ce-a360-3d1284babd8a/line_2.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/e4122d8b-9ce2-49ce-a360-3d1284babd8a/line_2.png)

선분이 두 개 이상 겹친 곳은 [-2, -1], [0, 1]로 길이 2만큼 겹쳐있습니다.

---

### 제한사항

- `lines`의 길이 = 3
- `lines`의 원소의 길이 = 2
- 모든 선분은 길이가 1 이상입니다.
- `lines`의 원소는 [a, b] 형태이며, a, b는 각각 선분의 양 끝점 입니다.
    - 100 ≤ a < b ≤ 100

---

### 입출력 예

| lines | result |
| --- | --- |
| [[0, 1], [2, 5], [3, 9]] | 2 |
| [[-1, 1], [1, 3], [3, 9]] | 0 |
| [[0, 5], [3, 9], [1, 10]] | 8 |

---

### 입출력 예 설명

입출력 예 #1

- 두 번째, 세 번째 선분 [2, 5], [3, 9]가 [3, 5] 구간에 겹쳐있으므로 2를 return 합니다.

입출력 예 #2

- 겹친 선분이 없으므로 0을 return 합니다.

입출력 예 #3

- 첫 번째와 두 번째 선분이 [3, 5] 구간에서 겹칩니다.
- 첫 번째와 세 번째 선분 [1, 5] 구간에서 겹칩니다.
- 두 번째와 세 번째 선분 [3, 9] 구간에서 겹칩니다.
- 따라서 [1, 9] 구간에 두 개 이상의 선분이 겹쳐있으므로, 8을 return 합니다.

나의 풀이

```swift
import Foundation

func solution(_ lines: [[Int]]) -> Int {
    var overlappingLength = 0
    
    
    let sortedLines = lines.sorted { $0[0] < $1[0] }
    //시작 좌표 정렬
    
    var previousEnd = sortedLines[0][1]
    // 이전 끝점을 첫번째 끝 좌표로 초기화
    
		//나머지도 반복
    for i in 1..<sortedLines.count {
        let currentStart = sortedLines[i][0]
        let currentEnd = sortedLines[i][1]
        
				//이전꺼랑 비교해서 중복이 있는지 확인
        if currentStart <= previousEnd {
            overlappingLength += min(currentEnd, previousEnd) - currentStart
            previousEnd = max(currentEnd, previousEnd)
        } else {
            previousEnd = currentEnd
        }
    }
    
    return overlappingLength
}
```

테스트 결과

```swift
테스트 1 〉	통과 (0.09ms, 16.1MB)
테스트 2 〉	실패 (0.08ms, 16.5MB)
테스트 3 〉	통과 (0.09ms, 16.5MB)
테스트 4 〉	통과 (0.09ms, 16.3MB)
테스트 5 〉	통과 (0.09ms, 16.5MB)
테스트 6 〉	실패 (0.08ms, 16.2MB)
테스트 7 〉	통과 (0.10ms, 16.5MB)
테스트 8 〉	통과 (0.09ms, 16.6MB)
테스트 9 〉	통과 (0.13ms, 16.5MB)
테스트 10 〉	통과 (0.12ms, 16.3MB)
```

- 테스트 1, 2에서는 문제가 없었는데 3에서는 기댓값이 예상과는 다르게 나온다.
- 문제에 대한 접근이 잘못 되었던것 같아, 이후 다른 스터디원의 코드를 참고해서 업데이트 해야겠다.