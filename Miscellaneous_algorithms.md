기타 알고리즘
=============
백준을 풀면서 사용해보았던 순서대로 작성합니다.

유클리드 호제법(Euclidean Algorithm)
------------------------------------
> 시간 복잡도 : $O(logN)$
>
> 2개의 자연수 a, b에 대해서 a를 b로 나눈 나머지를 r이라 하면(단, a>b), a와 b의 최대공약수는 b와 r의 최대공약수와 같다.

최대 공약수를 찾는 알고리즘이다. 찾는 과정은 다음과 같다.

1. 자연수 a와 b를 입력 받은 후(단, a > b), a % b 의 값을 r에 저장한다. 
2. r값이 0이 아닐경우, b와 r값으로 1번 과정을 재시행한다.
3. 2번까지의 과정을 r값이 0이 될때까지 반복한다.
4. r값이 0일 때의 b 값을 출력한다.

사용 예시는 다음과 같다. <[백준 13241번](https://www.acmicpc.net/problem/13241) | [내 풀이](https://www.acmicpc.net/source/60954825)>
```cpp
int Euclidean(long long int a, long long int b){ // 재귀함수를 사용.
    long long int r = a % b; // a % b의 값을 r에 저장.
    if(r == 0) {
        return b; // r의 값이 0일 경우 b의 값을 결과로 출력 (=최대 공약수가 b)
    }
    return Euclidean(b, r); // r의 값이 0이 아닐 경우, b와 r을 이용해서 다시 한번 시행.
}
```

에라토스테네스의 체
-------------------
> 시간 복잡도 : $O(Nlog(logN))$

소수를 찾는 알고리즘이다. 찾는 과정은 다음과 같다.
1. 찾으려고 하는 범위의 수들이 적힌 배열을 만든다.
2.  idx가 2 <= idx <= sqrt(배열의 최댓값) 이라고 할때, 배열의 수 % idx == 0인 값들을 모두 지운다.
3.  배열의 남은 값들이 소수이다.

사용 예시는 다음과 같다. <[백준 1929번](https://www.acmicpc.net/problem/1929) | [내 풀이](https://www.acmicpc.net/source/61024318)>
```cpp
#include <iostream>
#include <vector>
#include <cmath>

int main() {
    int first, last;
    std::cin >> first >> last;
    std::vector<int> num_list;

    for(int i = first; i <= last; i++){
        if(i != 1)
            num_list.push_back(i); // 원하는 수들의 배열을 생성.
    }

    int idx = 2;
    while(idx <= sqrt(last)){
        for(int& v : num_list){
            if((v % idx == 0 && v != idx) && v != 0)
                v = 0;
        }
        idx++; // 2부터 sqrt(배열의 최댓값)까지의 값으로 배열의 수를 나눠 나머지가 0인 경우 모두 제거(= 소수가 아닌 수를 제거함.)
    }

    for(int v : num_list){
        if (v != 0)
            std::cout << v << "\n"; // 결과 출력.
    }
}
```