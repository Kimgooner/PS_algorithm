자료 구조
=========
백준을 풀면서 사용해보았던 순서대로 작성합니다.

스택(Stack)
-----------
> <시간 복잡도>
> 
> Insertion = $O(1)$
> 
> Deletion = $O(1)$
> 
> Search = $O(N)$

> ![stack_img](https://github.com/Kimgooner/PS_algorithm/assets/82828857/f559edfd-3a29-43d7-9c70-6a74690c0bc8)
>
> 스택의 push 함수와 pop 함수는 다음과 같은 기능을 한다.

LIFO(Last In First Out)특성을 가지는 자료 구조로, 메모리에 새로 들어오는 데이터는 메모리의 말단에 위치한다.

스택에서 내보내는 데이터 역시 메모리의 말단을 거친다.

다음은 배열을 이용하여 스택을 구현한 것이다. <[백준 10828번](https://www.acmicpc.net/problem/10828) | [내 풀이](https://www.acmicpc.net/source/61147713)>

```cpp
//#include <stack> c++에는 STL 라이브러리로 stack template를 제공한다.
class Stack {
private:
    int stack[10000];
    int last; // 스택의 현재 탑 메모리의 위치를 가리키는 포인터.
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

큐(Queue)
---------
> <시간 복잡도>
> 
> Insertion = $O(1)$
> 
> Deletion = $O(1)$
> 
> Search = $O(N)$

> ![queue_img](https://github.com/Kimgooner/PS_algorithm/assets/82828857/fe2f210a-6d1d-4679-83cb-bfcfe1b24ac5)
>
> 큐의 push 함수는 rear 위치에 데이터를 추가하고, pop 함수는 front 위치에 데이터를 제거한다.

FIFO(First In First Out)특성을 가지는 자료 구조로, 메모리에 새로 들어오는 데이터는 메모리의 말단(rear)에 위치한다.

하지만, 스택과 달리 내보내는 데이터의 위치는 제일 앞(front)에 위치한다.

다음은 연결 리스트를 이용하여 큐 구현한 것이다. <[백준 18258번](https://www.acmicpc.net/problem/18258) | [내 풀이](https://www.acmicpc.net/source/61192878)>

```cpp
// #include <queue> c++에는 STL 라이브러리로 queue template를 제공한다.
struct Node {
    int data;
    Node* next;
};

struct Queue {
    Node *front, *back;
    int len = 0;

    Queue(){ // 기본 생성자
        front = back = nullptr;
    }

    int size(){ // queue의 현재 크기 출력
        return len;
    }

    int isEmpty(){ // queue가 비어있는지(len = 0) 확인
        if(len == 0) return 1;
        else return 0;
    }

    int front_data(){
        if(isEmpty())
            return -1;
        return front->data;
    }

    int back_data(){
        if(isEmpty())
            return -1;
        return back->data;
    }

    void push(int data){ // =enqueue, 데이터를 큐의 rear에 저장한다.
        Node* new_data = new struct Node;
        new_data->data = data;
        new_data->next = nullptr;
        if(isEmpty()){
            front = back = new_data;
        }
        else{
            back->next = new_data;
            back = back->next;
        }
        len++;
    }

    int pop(){ // =dequeue, front에 위치하는 데이터를 내보낸다.
        if(isEmpty())
            return -1;
        Node* pop_data = front;
        int ret = pop_data->data;
        front = pop_data->next;
        delete pop_data;
        len--;
        return ret;
    }
};
```

덱(Deque, Double-Ended Queue)
-----------------------------
> <시간 복잡도>
>
> Insertion = $O(1)$ // front, rear 둘다 만족
> 
> Deletion = $O(1)$ // front, rear 둘다 만족
> 
> Search = $O(N)$

> img
>
> blah blah

내용.

다음은 연결 리스트를 이용하여 덱을 구현한 것이다.

```cpp
// #include <deque> c++에는 STL 라이브러리로 deque template를 제공한다.
struct Node {
    int data;
    Node *next;
    Node *prev;
};

struct Deque {
    Node *front, *rear;
    int len = 0;

    Deque(){
        front = rear = nullptr;
    }

    int size(){
        return len;
    }

    bool isEmpty(){
        return len == 0;
    }

    int front_data() {
        return front->data;
    }

    int rear_data() {
        return rear->data;
    }

    void front_push(int data){
        Node *new_data = new struct Node;
        new_data->data = data;
        new_data->next = nullptr;
        if(isEmpty())
            front = rear = new_data;
        else{
            new_data->next = front;
            front->prev = new_data;
            front = new_data;
        }
        len++;
    }

    void rear_push(int data){
        Node *new_data = new struct Node;
        new_data->data = data;
        new_data->next = nullptr;
        if(isEmpty())
            front = rear = new_data;
        else{
            rear->next = new_data;
            new_data->prev = rear;
            rear = new_data;
        }
        len++;
    }

    int front_pop(){
        Node *del_Node = front;
        if(isEmpty())
            return -1;
        else{
            int ret = front->data;
            front = front->next;
            delete del_Node;
            return ret;
        }
    }

    int rear_pop(){
        Node *del_Node = rear;
        if(isEmpty())
            return -1;
        else{
            int ret = rear->data;
            rear = rear->prev;
            delete del_Node;
            return ret;
        }
    }
};
```
