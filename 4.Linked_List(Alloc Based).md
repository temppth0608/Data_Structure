```
최종 작성자 : 박태현
최초 작성일 : 2016년 4월 11일
마지막 수정 : 2016년 4월 11일, 박태현
```

# 연결리스트 - 2

## Linked란 무엇인가?
**배열은 메모리의 특성이 정적이어서(길이의 변경이 불가능해서) 메모리의 길이를 변경하는 것이 불가능 함**<br>

*이러한 정적인 배열의 문제를 해결하기위해 '동적인 메모리의 구성' 으로 해결할 수 있다.*

```C
/*
ADT를 고려하지 않은 Linked List 구현
*/
#include <stdio.h>
#include <stdlib.h>

typedef struct _node {
    int data;
    struct _node* next;
}Node;

int main(int argc, const char * argv[]) {
    
    Node* head = NULL;	//리스트의 머리를 가리키는 포인터 변수
    Node* tail = NULL;	//리스트의 꼬리를 가리키는 포인터 변수
    Node* cur = NULL;	//저장된 데이터의 조회에 사용되는 포인터 변수
    
    Node* newNode = NULL;
    
    int readData;
    
    /*
     입력
    */
    
    while(1) {
        printf("자연수를 입력 하세요 : ");
        scanf("%d", &readData);
        
        if(readData < 1) {
            break;
        } else {
            newNode = (Node*)malloc(sizeof(Node));
            newNode -> data = readData;
            newNode -> next = NULL;
            if (head == NULL) {
                head = newNode;
            } else {
                tail -> next = newNode;
            }
            tail = newNode;
        }
    }
    
    /* 
     출력
    */
    
    if (head == NULL) {
        printf("데이터가 없습니다.\n");
    } else {
        cur = head;
        printf("%d\n", cur -> data);
        
        while((cur -> next) != NULL) {
            cur = cur -> next;
            printf("%d\n", cur -> data);
        }
    }
    
    /*
     메모리 해제 과정
    */
    
    if (head == NULL) {
        printf("데이터가 없습니다.");
        return 0;
    } else {
        Node* delNode = head;
        Node* delNextNode = head -> next;
        
        printf("%d를 삭제합니다.\n", head -> data);
        free(delNode);
        
        while(delNextNode != NULL) {
            delNode = delNextNode;
            delNextNode = delNextNode -> next;
            printf("%d를 삭제합니다. \n", delNode -> data);
            free(delNode);
        }
    }
    
    return 0;
}
```

**Node - 연결이 가능한 개채**

새노드를 리스트의 머리와 꼬리중 어디에 저장 하는 것이 효율적인가?

1. 머리에 추가할 경우
	* 장점 - 포인터 변수 tail이 불필요하다.
	* 단점 - 저장된 순서를 유지하지 않는다.
2. 꼬리에 추가할 경우
	* 장점 - 저장된 순서가 유지된다.
	* 단점 - 포인터 변수 tail이 필요하다.
	
*포인터 변수 tail을 유지하기 위해서 넣어야할 부가적인 코드가 번거롭게 느껴질 수 있고, 리스트 자료구조는 저장된 순서를 유지해야 하는 자료구조는 아님!*

*더미 노드 - 기존의 노드를 추가, 삭제 그리고 조회하는 방법에 있어서 첫 번째 노드와 두 번째 이후의 노드에 차이가 있음, 이를 해결하기위해 유효한 데이터를 지니지 않는 그냥 빈 노드(더미) 노드를 추가하여, 노드의 추가, 삭제 및 조회의 과정을 일관된 형태로 구성할 수 있다.*

```C
/*
ADT를 제외한 더미노드를 이용하여 꼬리에 데이터 넣는 코드
*/

#include <stdio.h>
#include <stdlib.h>

typedef struct _node {
    int data;
    struct _node* next;
}Node;

int main(int argc, const char * argv[]) {
    
    Node* head = NULL;
    Node* tail = NULL;
    Node* cur = NULL;
    
    Node* newNode = NULL;
    
    int readData;
    
    head = (Node*)malloc(sizeof(Node)); //더미 노드 추가
    tail = head;
    /*
     입력
    */
    
    while(1) {
        printf("자연수를 입력 하세요 : ");
        scanf("%d", &readData);
        
        if(readData < 1) {
            break;
        } else {
            newNode = (Node*)malloc(sizeof(Node));
            newNode -> data = readData;
            newNode -> next = NULL;
            
            tail->next = newNode;
            tail = newNode;
        }
    }
    
    /* 
     출력
    */
    
    cur = head;
    while(cur -> next != NULL) {
        cur = cur -> next;
        printf("%d\n", cur -> data);
    }
    
    /*
     메모리 해제 과정
    */
    
    Node* delNode = head;
    Node* delNextNode = head->next;
    
    if(head -> next == NULL) {
        printf("데이터가 없습니다.");
        return 0;
    }
    
    while(delNextNode != NULL) {
        delNode = delNextNode;
        delNextNode = delNextNode->next;
        printf("%d 삭제\n", delNode -> data);
        free(delNode);
        
    }
    
    return 0;
}
```

