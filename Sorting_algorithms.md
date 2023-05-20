정렬 알고리즘
=============
백준을 풀면서 사용해보았던 순서대로 작성합니다.

카운팅 정렬(Counting Sort)
--------------------------
> 시간 복잡도 : $O(n+k)$ // k는 데이터의 최댓값이다.

숫자의 개수를 세어 정렬하는 방식으로, 과정은 다음과 같다.

1. 정렬하려는 수들 중에서 가장 큰 수를 찾는다. 이를 기반으로 하는 카운팅 배열의 크기를 결정한다.
2. 카운팅 배열을 생성하고, 각 수마다 출현 횟수를 세어 저장한다.
3. 카운팅 배열을 토대로 누적 카운팅 배열을 생성한다. 이는 각 인덱스보다 작거나 같은 값의 출현 횟수들의 누적합과 같다.
4. 원래 수의 배열을 순회하면서, 해당하는 누적 카운팅 배열의 값을 하나씩 줄여가며 정렬된 새로운 배열을 만든다.

사용 예시는 다음과 같다. <[백준 10989번](https://www.acmicpc.net/problem/10989)> | [내 풀이](https://www.acmicpc.net/source/60879093)
```cpp
#include <iostream>

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(nullptr);

    int N;
    std::cin >> N;
    int data[10001] = {0}; // 

    int input;
    for(int i = 0; i < N; i++){
        std::cin >> input;
        data[input]++;
    }

    for(int i = 1; i < 10001; i++){
        if(data[i] != 0){
            for(int j = 0; j < data[i]; j++){
                std::cout << i << "\n";
            }
        }
    }
}
```
