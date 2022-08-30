---
layout: default
title: algorithm data structure 종류
parent: algorithm
nav_order: 405200
---

### Linked List
```java
class Node
{
public:
    Node* next;
    int data;
};

LinkedList::LinkedList(){
this->length = 0;
this->head = NULL;
}

int length;
Node* head;
void LinkedList::add(int data){
Node* node = new Node();
node->data = data;
node->next = this->head;
this->head = node;
this->length++;
}
void LinkedList::print(){
Node* head = this->head;
int i = 1;
while(head){
std::cout << i << "": "" << head->data << std::endl;
head = head->next;
i++;
}
}
```


### Vector
* 시작에 타입을 정해놓은 연속된 데이터 구조
```java
// 대괄호 연산자
template <class T>
T& LinkedList<T>::operator[](const int &i) {
    return get(i);
}
```


### Hashtable
null이 입력이 안되는 key value 구조	동기화 지원


### Hashmap
null이 입력이 되는 key value 구조	동기화 지원 하지 않음


### 스택
lifo	마지막이 처음으로 나옴


### 큐
fifo	처음이 처음으로 나옴


### Map
javascript의 key value 자료구조
자바에서는 list와 같이 인터페이스, hash라고도 불림


### hashmap
linkedhashmap등이 있음


### Set
javascript의 값의 집합


### linked list
동적으로 길이를 지정할수 있는 연속된 자료구조


### array
배열 크기가 고정된 길이가 있는 데이터 구조

자바에서 arraylist의 경우 vector에 자동 동기화기능이 삭제된 형태
스레드 처리에는 vector보다 synchronizedlist, map 사용


### B-Tree, B+-Tree
균형 탐색 트리
B-의경우 자식 여러 개 모른 리프가 부모와 같은거리
b+의겨우 마지막에 삽입되도록 리프끼리 링크"


### AVL-TREE, Red-Black Tree
AVL 회전을 통해 높이 유지
좌 회전할경우 좌 자식을 부모로
좌 자식의 오른 자식을 부모의 좌자식으로

블랙 레드 트리
루트는 블랙이다.
모든 리프(NIL)는 블랙이다.
노드가 레드이면 그 노드의 자식은 반드시 블랙이다.
로트 노드에서 임의의 리프 노드에 이르는 경로에서 만나는 블랙 노드의 수는 모두 같다.

회전하고 색상을 바꿔가며 처리


### 어레이와 리스트 정렬할때 정렬 방식에 따라 차이
어레이는 랜덤 억세스가 가능하고 리스트는 리니어하게 접근해들어가야 하기 때문에 차이 발생
