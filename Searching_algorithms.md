탐색 알고리즘
=============
백준을 풀면서 사용해보았던 순서대로 작성합니다.

이진 탐색 알고리즘(Binary Search Algorithm)
-------------------------------------------
> 시간 복잡도 : $O(logN)$
> 
> 탐색하려는 배열이 오름차순으로 정렬되어 있어야한다.

탐색 과정은 다음과 같다.

1. 배열을 가운데를 기준으로 두 부분으로 나눈 후, 가운데 값과 찾는 값을 비교한다.
2. 찾는 값과 가운데 값이 다를 경우, 찾는 값과 대소 비교 후 어느 부분에서 값을 찾을지 결정한다.
3. 2번까지 내용을 값을 찾을때까지 반복한다.
사용 예시는 다음과 같다. <[백준 14425번](https://www.acmicpc.net/problem/14425) | [내 풀이](https://www.acmicpc.net/source/60915913)>
```c++
bool binary_search(std::vector<std::string>& v, std::string& str, int first, int last) {
    int mid = (first + last) / 2; 
    while(first <= last) {
        if (v[mid] == str) 
            return true; // 배열의 중간값이 찾는 값일 경우.
        else if (v[mid] > str) { // 배열의 중간값이 찾는 값이 아니고, 그 값이 찾는 값보다 작을 경우.
            last = mid - 1;
            mid = (first + last) / 2; // 배열의 시작 값은 그대로 하고, 마지막 값을 mid - 1로 변경 후 다시 시행. 
        } else { // 배열의 중간값이 찾는 값이 아니고, 그 값이 찾는 값보다 클 경우.
            first = mid + 1;
            mid = (first + last) / 2; // 배열의 시작 값을 mid + 1로 하고, 마지막 값은 그대로 둔 후 다시 시행.
        }
    }
    return false;
}
```

깊이 우선 탐색(Depth First Search)
----------------------------------
