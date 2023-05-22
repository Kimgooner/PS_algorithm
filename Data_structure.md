자료 구조
=========
백준을 풀면서 사용해보았던 순서대로 작성합니다.

스택(Stack)
-----------
> ![stack_img](https://github.com/Kimgooner/PS_algorithm/assets/82828857/f559edfd-3a29-43d7-9c70-6a74690c0bc8)
>
> 예시 이미지, 스택의 push 함수와 pop 함수는 다음과 같은 기능을 한다.

LIFO(Last In First Out)특성을 가지는 자료 구조로, 메모리에 새로 들어오는 데이터는 메모리의 말단에 위치한다.

일반적으로, 다음과 같은 5가지 메소드와 함께 사용한다.

**push(data)** // 스택에 데이터를 저장한다. 저장되는 위치는 스택의 맨 윗 부분이다.

**top()** // 스택의 맨 윗 부분에 위치한 데이터에 접근한다.

**pop()** // 스택의 맨 윗 부분에 위치한 데이터를 빼낸다.

**size()** // 스택에 저장되어있는 데이터의 개수를 반환한다.

**empty()** // 스택이 비어있는지 확인한다.

다음은 class로 스택을 정의한 것이다. <[백준 10828번](https://www.acmicpc.net/problem/10828) | [내 풀이](https://www.acmicpc.net/source/61147713)> // 문제에선 STL vector를 사용해서 스택을 구현했다.

```cpp
class Stack {
private:
    int stack[10000];
    int last; // 스택의 현재 탑 메모리의 위치를 가리키는 포인터. <[백준 10828번](https://www.acmicpc.net/problem/10828) | [내 풀이](https://www.acmicpc.net/source/61147713)>
public:
    void init() {
        last = -1; // 스택초기화.
    }
    void push(int x) {
        stack[++last] = x; // 스택의 탑 메모리에 데이터 삽입.
    }
    bool empty() {
        return (last < 0); // 스택이 비어있는지 확인. 
    }
    int pop() {
        if(empty()) {
            return -1; // 런타임 에러 방지.
        }
        return stack[last--]; // 스택의 탑 메모리 데이터를 빼냄.
    }
    int size() {
        return last + 1; // 스택의 현재 크기 출력.
    }
    int top() {
        if(empty()) {
            return -1; // 런타임 에러 방지.
        }
        return stack[last]; // 스택의 현재 탑 메모리의 데이터를 출력.
    }
};
```

