---
###  03. list2 예제 코드 해석 2편! 👀👀

이전까지 insertFirstNode 함수를 해석하여  -1 → 1 → 3 → 4 데이터가 정리되는 것을 확인했습니다. 이제 남은 main 함수 코드를 해석해보도록 하겠습니다. main 함수는 아래와 같습니다.

```c
int main() {
	List list1;
	list1.insertFirstNode(4);
	list1.insertFirstNode(3);
	list1.insertFirstNode(1);
	list1.insertNode(1, 2);
	list1.deleteNode(3);

    list2.insertFirstNode(4);
    list2.insertFirstNode(2);
    list2.insertFirstNode(1);
    
/// 생략
	if (list1 == list2)
		std::cout << "list1 and list2 are equal" << std::endl;
	else
		std::cout << "list1 and list2 are not equal" << std::endl;
	
	return 0;
}
```

<center><img src="/assets/images/posts/linked list2(1).PNG" width="100%" height="100%"></center>

현재 STACK 영역과 HEAP 영역은 위의 그림과 같습니다. 여기서 list1 class가 insertNode 함수를 호출하며 1, 2를 인자로 전달합니다. insertNode 함수 코드를 살펴보겠습니다.

```c
void List::insertNode( int prevData, int data) {
	Node* p = ptr_->next;
	while (p ) {
		if(p->data == prevData)
			break;
		p = p-> next;
	}
	if (p ) {
		Node *tmp = new Node(data, p->next);
		p->next = tmp;
	}
}
```

Node * p 를 선언하고 ptr_->next를 가르키게 합니다. 그리고 p 값이 null이 될 때까지 while 문을 돌게 됩니다. while 문 안에서는 if 로 p가 가르키는 Node의 data 값이 인자값으로 전달된 1 (prevData) 이 맞는지 확인하고 맞으면 break로 반복문을 종료하고, 틀리면 p 값을 p 가 가르키는 Node의 next 값으로 치환합니다. 이렇게 치환되면 p는 다음 Data를 계속 가르키게 됩니다. 우선은 여기까지의 코드를 그림으로 그려보겠습니다.

<center><img src="/assets/images/posts/linked list2(2).PNG" width="100%" height="100%"></center>

이렇게 바로 p값의 데이터 1과 prevData 값 1이 같아서 while 문 반복 없이 break로 빠져나오게 됐습니다. 바로 이어서 if 문 해석을 해보겠습니다.

<center><img src="/assets/images/posts/linked list2(3).PNG" width="100%" height="100%"></center>

Node * 타입의 tmp를 선언하고 HEAP 영역 안에 Node class 공간을 할당받습니다. 그리고 2의 값과 p->next 값을 넣은 Node 가 생성됩니다. 마지막 줄 p->next = tmp; 코드가 실행되면 다음과 같이 변하게 됩니다.

<center><img src="/assets/images/posts/linked list2(4).PNG" width="100%" height="100%"></center>

insertNode 함수가 끝났습니다. data를 나열해보면 -1 → 1 → 2 → 3 → 4 이렇게 순서대로 넣어졌습니다. 이제 list1 class가 deleteNode 함수를 호출합니다. deleteNode 함수는 다음과 같습니다.

```c
void List::deleteNode(int data) {
	Node* p1 = ptr_->next;
	Node* p2 = ptr_;
	
	while(p1 ) {
		if (p1->data == data)
			break;
		
		p1 = p1->next;
		p2 = p2->next;
	}
	
	if (p1 ) {
		p2->next = p1->next;
		delete p1;
	}
}
```

이 함수를 이해하면 다른 함수들도 쉽게 이해하실 수 있을 거라 생각합니다! 전 post에서 설명했듯이 왜 Buffer Node를 만들었는지도 이 함수를 통해 아실 수 있습니다. while 문 안에 if 문 조건까지 확인해보겠습니다.

<center><img src="/assets/images/posts/linked list2(5).PNG" width="100%" height="100%"></center>

if의 조건식이 (1 == 3), false 이므로 다음으로 건너뛰어서 코드를 진행합니다.

<center><img src="/assets/images/posts/linked list2(6).PNG" width="100%" height="100%"></center>

한번 더 반복해서 if 조건을 확인해보니 (2 == 3) , false 이므로 한번 더 코드를 진행합니다.

<center><img src="/assets/images/posts/linked list2(7).PNG" width="100%" height="100%"></center>

<center><img src="/assets/images/posts/linked list2(4).PNG" width="100%" height="100%"></center>

insertNode 함수가 끝났습니다. data를 나열해보면 -1 → 1 → 2 → 3 → 4 이렇게 순서대로 넣어졌습니다. 이제 list1 class가 deleteNode 함수를 호출합니다. deleteNode 함수는 다음과 같습니다.

```c
void List::deleteNode(int data) {
	Node* p1 = ptr_->next;
	Node* p2 = ptr_;
	
	while(p1 ) {
		if (p1->data == data)
			break;
		
		p1 = p1->next;
		p2 = p2->next;
	}
	
	if (p1 ) {
		p2->next = p1->next;
		delete p1;
	}
}
```

이 함수를 이해하면 다른 함수들도 쉽게 이해하실 수 있을 거라 생각합니다! 전 post에서 설명했듯이 왜 Buffer Node를 만들었는지도 이 함수를 통해 아실 수 있습니다. while 문 안에 if 문 조건까지 확인해보겠습니다.

<center><img src="/assets/images/posts/linked list2(5).PNG" width="100%" height="100%"></center>

if의 조건식이 (1 == 3), false 이므로 다음으로 건너뛰어서 코드를 진행합니다.

<center><img src="/assets/images/posts/linked list2(6).PNG" width="100%" height="100%"></center>

한번 더 반복해서 if 조건을 확인해보면 (3 == 3) , 드디어 True 이므로 break 함수로 반복문을 빠져나옵니다.

<center><img src="/assets/images/posts/linked list2(7).PNG" width="100%" height="100%"></center>

마지막 if (p1 ) 은 p1이 가르키는 값이 Null이 아니기 때문에 조건이 만족하여 실행문을 실행합니다. 코드를 실행한 후의 그림은 이렇습니다.

<center><img src="/assets/images/posts/linked list2(8).PNG" width="100%" height="100%"></center>

이렇게 해서 deleteNode 함수의 실행까지 살펴보았습니다. dummy Node가 왜 필요한지 감이 오셨나요? Linked List의 장점이 바로 data들 사이에 data를 삽입하거나 삭제할 때 자료구조의 변경이 필요없다는 것이었는데요. 우리가 지금까지 살펴보니 연결된 pointer 값만 변경해주면 순서가 쉽게 변경되는 것을 확인했습니다. 하지만 그 의미는 pointer를 잘 관리하지 못하면 끊긴 data들에는 접근할 수 없어진다는 것입니다.

그렇기 때문에 중간에 데이터를 삭제하기 위해서는 그 전에 삭제할 데이터를 가르키고 있는 pointer를 알아야 할 필요가 있었습니다. 그래서 Node * 를 2개 만들어서 한단계 차이로 계속 쫓아가는 듯한 그림을 만들어야 했던 것입니다. data를 삭제한 후에 끊긴 pointer를 연결해서 다음 Node를 가리키게 만드는 것이죠.

결국 list1 의 ptr_이 가르키는 Node의 data들은 -1 → 1 → 2 → 4 가 되었습니다. 이제 남은 코드들을 한번에 살펴보겠습니다.

```c
list2.insertFirstNode(4);
list2.insertFirstNode(2);
list2.insertFirstNode(1);
/// 생략
if (list1 == list2)		//	list1.operator==(list2) or operator==(list1, list2)
    std::cout << "list1 and list2 are equal" << std::endl;
else
    std::cout << "list1 and list2 are not equal" << std::endl;

return 0;
```

list2 class 는 이전 블로그의 insertFirstNode 함수의 설명처럼 -1 → 1 → 2 → 4 가 될 것이라고 알 수 있습니다. 그렇다면 list1 과 list2 는 같다고 볼 수 있을까요? 맞다고 할 수도 있고 아니라고 할 수도 있습니다. 왜냐하면 우리는 기본 자료형에 대한 논리 연산은 배웠지만 우리가 생성한 class의 논리 연산이 적용될 수 있는지는 배우지 않았기 때문입니다.

list1 == list2 두 개의 class 값을 비교하려면 어떤 값을 비교해서 맞다 틀리다를 판단할 수 있을까요? 제가 위에서 설명한 바와 같이 list 안에 ptr_ 값이 가르키는 연결된 Node들의 Data들의 값의 순서가 동일하면 True 일 것이고, 틀리면 False가 될 것입니다. 이러한 ==연산은 **우리가 정의한 논리 연산**이므로 함수로 만들어 주어야 비로소 방금 말했던 논리의 연산이 가능해집니다. 마지막 남은 함수 operator== 함수에 대해서 살펴보겠습니다. 함수는 다음과 같습니다.

```c
bool List::operator==(const List& rhs) const {
	Node *p = this->ptr_->next;
	Node *p2 = rhs.ptr_->next;

	while (p ) {
		if (p->data != p2->data)
			break;
		p = p->next;
		p2 = p2->next;
	}

	return (p == NULL);
}
```

list1 이 list2 를 const List& 타입 rhs 변수로 인자를 전달하는 operator== 함수를 호출했습니다. 이전에 논리 연산이 어떻게 이루어질지 설명드렸었는데요. 과연 코드에서는 어떻게 작성되어 있을지 해석해보겠습니다.

<center><img src="/assets/images/posts/linked list2(9).PNG" width="100%" height="100%"></center>

Node * 타입의 p와 p2를 만들어 각각 this와 rhs를 가르키고 한 단계씩 넘어가면서 data값들을 비교할 수 있는 그림이 되었습니다. while 문 안에서는 조건문(if)을 통해 맞지 않으면 break를 걸어 반복문을 빠져나가게 하고, 맞으면 다음 data들을 비교하는 알고리즘을 만들었습니다.  return 값은 p == NULL 이 되었느냐라고 물었기 때문에 p가 NULL이면 True를 반환할 것이고, p가 NULL이 아니면 False를 반환하게 될 것입니다. 마지막 문장을 이해하기 어려우실 수도 있을 것 같아 그림으로 한번 더 설명드리겠습니다.

<center><img src="/assets/images/posts/linked list2(10).PNG" width="100%" height="100%"></center>

현재 예제의 경우 이렇게 끝까지 1, 2, 4로 값이 같기 때문에 p와 p2는 Null을 가르키게 됩니다. 그럼 while 문의 조건식이 p가 null이 되기 때문에 빠져나오게 되고 return 값으로 True가 반환되게 됩니다.

이렇게 list2 예제 코드에 대해 설명드렸습니다. 요청받는 내용은 삽입과 삭제, 순회?여서 생성자와 그 외에 다른 함수들은 생략했었습니다. 만약 생략된 내용에 대해 더 궁금하시거나 이해가 안되시면 그에 대해 또 댓글 남겨주세요! 여기까지 설명이 틀린 부분이나 부족한 부분이 있다면 꼭 아래 댓글로 요청해주세요!

생각보다 늦게 올라간 것 같아 혹 공부 못하셨을까봐 죄송합니다. 기초부터 설명하려고 하다보니 양이 더 많아진 것 같습니다. 노력한만큼 더 이해가 쉬우셨으면 좋겠습니다. 힘들어도 열심히 올려드리겠습니다! 더더 질문해주세요~ 감사합니다. 😄