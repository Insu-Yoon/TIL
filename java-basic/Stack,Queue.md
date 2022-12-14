# 자료구조 소개

자료구조란 데이터들의 묶음을 저장하고 사용하는 방법을 정의한 것이다. 수많은 데이터들을 필요에 따라 정리하고 활용할 때, 효율적인 방법이 있으면 당연히 좋을 것이다. 직접 자신이 원하는 처리방식을 구현하여 사용할 수도 있겠지만, 이미 수많은 개발자들이 그러한 효율적인 방법들을 연구해왔고 그 결과물들이 앞으로 배우게 될 자료구조이다. 자료구조는 특정한 상황에 놓인 문제를 해결하는데 특화되어 있으므로, 적합한 자료구조를 선택할 수 있게 된다면 빠르고 정확하게 문제를 해결할 수 있다.

보편적으로 자주 사용되는 자료구조는 Stack, Queue, Tree, Graph이며, 오늘은 Stack과 Queue에 정리해보자.

---

## Stack

-   LIFO(Last In First Out)의 구조를 갖는 자료구조이다. 가장 먼저 들어간 데이터가 가장 나중에 나오게 된다. 프링글스를 생각하면 이해하기 쉽다.
-   한번에 하나의 데이터만 처리할 수 있다.
-   데이터를 입력하든, 출력하든 한 방향으로 이루어진다.
-   웹 브라우저의 앞으로 가기, 뒤로 가기 또한 Stack을 활용해 구현된 기능이다.


### Stack의 메서드

| 반환 타입   | 메서드 | 기능 |
|---------| --- | --- |
| < T >   | push(T t) | 데이터를 Stack에 추가하고, 추가한 값을 반환한다 |
| < T >   | peek() | Stack의 마지막 요소를 반환하며, Stack에 변화를 주지 않는다. |
| < T >   | pop() | Stack의 마지막 요소를 반환하며, Stack에서 해당 요소를 제거한다. |
| boolean | empty() | Stack이 비었는지 여부를 리턴한다. |
| int     | search(Object o) | Stack에서 o를 검색하여 해당 값이 있으면 인덱스를 반환한다.   <br/>(여러 개면 마지막 인덱스 반환) |

search()메서드의 경우, 첫 인덱스가 1이며 해당 인덱스는 가장 마지막에 입력된 데이터를 가르킨다.   
java에서 Stack 클래스는 Vector의 하위클래스이며, Vector는 List를 implement하므로 Collection의 메서드를 사용할 수 있다.

```java 
Stack<String> stack = new Stack<>(); // String형 Stack의 선언

stack.push("가"); //stack에 data 추가
stack.push("나");
stack.push("다");
stack.push("라");
// "가" "나" "다" "라" - 현재 데이터 순서. 가-나-다-라 순으로 입력되었다.
String peek = stack.peek(); // peek에 "라" 할당(peek이므로 stack은 변화없음)
String pop = stack.pop(); // pop에 "라" 할당(stack에서 "라" 삭제됨)
if(!stack.empty()) {
    stack.search("가"); // 4를 반환함
    stack.search("다"); // 2를 반환함
    stack.search("사"); // stack에 "사"는 없으므로 -1을 반환함
}
```
---

## Queue

-   FIFO(First In First Out)의 구조를 갖는 자료구조이다. 가장 먼저 들어간 데이터가 가장 먼저 나오게 된다.
-   Stack과 마찬가지로 한번에 하나의 데이터만 처리할 수 있다.
-   데이터의 입력, 출력의 뱡항이 다르다.
-   LinkedList를 활용해 구현한다.
-   롤을 해본 사람이라면 '큐를 잡는다' 라는 말을 들어본 적이 있을 것이다. 그 큐가 이 큐다.


### Queue의 메서드

| 반환 타입   | 메서드 | 기능 |
|---------| --- | --- |
| boolean | add(T t) | 데이터를 Queue에 추가하고, 성공 여부를 반환한다. |
| boolean | offer(T t) | 데이터를 Queue에 추가하고, 성공 여부를 반환한다. |
| < T >   | peek() | Queue의 선두 요소를 반환하며, Queue에 변화를 주지 않는다. |
| < T >   | poll() | Queue의 선두 요소를 반환하며, Queue에서 해당 요소를 제거한다.  |
| < T >   | remove() | Queue의 선두 요소를 반환하며, Queue에서 해당 요소를 제거한다. |

add와 offer 그리고 poll과 remove은 같은 동작을 하지만, 차이점이 존재한다.

-   offer는 add와 비교했을 때 IllegalStateException이 발생하지 않는다.  
    IllegalStateException는 Queue가 가득 찼을 때 offer를 시도하면 발생하는 런타임 오류다.      
    (주로 LinkedList로 구현해서 이런 경우가 발생할 일이 많을지는 모르겠다)
-   poll은 Queue가 비어있을 때 null을 반환하지만, remove는
    NoSuchElementException이 발생한다.

java에서 Queue는 인터페이스로 구현되어 있으며, Collection을 상속받으므로 Collection의 메서드를 사용할 수 있다.
```java
Queue<Integer> queue = new LinkedList<>(); //Integer형 Queue의 선언
queue.add(1); //queue에 데이터 추가
queue.add(2);
queue.add(3);
queue.add(4);
//1 2 3 4 - 현재 데이터 순서. 1 2 3 4 순으로 입력되었다.
int peek = queue.peek(); // peek에 1 할당. peek이므로 queue는 변화없음
int poll = queue.poll(); // poll에 1 할당. poll이므로 queue에서 1 삭제
int remove = queue.remove(); // remove에 2 할당. queue에서 2 삭제
queue.poll();
queue.poll();
//이제 queue는 빈 상태
queue.poll(); // null을 반환
queue.remove(); // NoSuchElementException 발생

```