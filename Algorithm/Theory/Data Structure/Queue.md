# 큐(Queue)?
![2](https://user-images.githubusercontent.com/48504392/75146178-e1bb6e00-573d-11ea-8c2e-c10c87b82ef7.jpg)
- 스택과 다르게 항목이 들어온 순서대로 데이터에 접근할 수 있는 선형 자료구조

# 특징
- 선입선출(FIFO) 구조
- Push를 통해 삽입한 자료는 가장 먼저 들어온 자료부터 Pop 연산으로 출력
- 시간복잡도 : O(1)

# 동작
- push : 큐 뒤쪽에 항목을 삽입
- pop : 큐 앞쪽의 항목을 반환 및 제거
- peek : 큐 앞쪽의 항목 조회
- empty : 큐가 비어 있는지 확인
- size : 큐의 크기를 확인

# 구현 1 - 일반적인 큐
~~~python
class Queue(object):
    def __init__(self):
        self.items = []
        
    def isEmpty(self):
        return not bool(self.items)
    
    def push(self, item):
        self.items.insert(0, item)
        
    def pop(self):
        value = self.items.pop()
        if value is not None:
            return value
        else:
            print("Queue is empty.")
            
    def size(self):
        return len(self.items)
    
    def peek(self):
        if self.items:
            return self.items[-1]
        else:
            print("Queue is empty.")
            
    def __repr__(self):
        return repr(self.items)
    
if __name__ == "__main__":
    queue = Queue()
    print("큐가 비었나요? {0}".format(queue.isEmpty()))
    print("큐에 숫자 0~9를 추가")
    for i in range(10):
        queue.push(i)
    print("큐의 크기: {0}".format(queue.size()))
    print("peek: {0}".format(queue.peek()))
    print("pop: {0}".format(queue.pop()))
    print("peek: {0}".format(queue.peek()))
    print("큐가 비었나요? {0}".format(queue.isEmpty()))
    print(queue)
~~~
~~~python
Out:
큐가 비었나요? True
큐에 숫자 0~9를 추가
큐의 크기: 10
peek: 0
pop: 0
peek: 1
큐가 비었나요? False
[9, 8, 7, 6, 5, 4, 3, 2, 1]
~~~
- 스택에서는 append() 메소드를 통해 삽입하며 큐에서는 insert() 메소드를 통해 값을 삽입  
- insert() 메소드로 인해 모든 요소가 메모리에서 이동될 수 있으므로 비효율적(O(n))
# 구현 2 - 노드의 컨테이너로 구현한 큐
~~~python
class Node(object):
    def __init__(self, value=None, pointer=None):
        self.value = value
        self.pointer = pointer

class Stack(object):
    def __init__(self):
        self.head = None
        self.count = 0
        
    def isEmpty(self):
        return not bool(self.head)
    
    def push(self, item):
        self.head = Node(item, self.head)
        self.count += 1
        
    def pop(self):
        if self.count > 0 and self.head:
            node = self.head
            self.head = node.pointer
            self.count -= 1
            return node.value
        else:
            print("Stack is empty")
            
    def size(self):
        return self.count

    def peek(self):
        if self.count > 0 and self.head:
            return self.head.value
        else:
            print("Stack is empty")
            
    def _printList(self):
        node = self.head
        while node:
            print(node.value, end = " ")
            node = node.pointer
        print()
    
if __name__ == "__main__":
    stack = Stack()
    print("스택이 비었나요? {0}".format(stack.isEmpty()))
    print("스택에 숫자 0~9를 추가")
    for i in range(10):
        stack.push(i)
    print("스택의 크기: {0}".format(stack.size()))
    print("peek: {0}".format(stack.peek()))
    print("pop: {0}".format(stack.pop()))
    print("peek: {0}".format(stack.peek()))
    print("스택이 비었나요? {0}".format(stack.isEmpty()))
    stack._printList()
~~~
~~~python
Out:
큐가 비었나요? True
큐에 숫자 0~9를 추가
큐가 비었나요? False
0 1 2 3 4 5 6 7 8 9 
큐의 크기: 10
peek: 0
pop: 0
peek: 1
1 2 3 4 5 6 7 8 9 
~~~
# 참고
https://gmlwjd9405.github.io/2018/08/03/data-structure-stack.html  
https://www.leafcats.com/125
