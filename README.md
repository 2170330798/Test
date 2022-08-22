# Coding-Studay
Slove some Coding problems
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MaxSize 12    /*最大节点数*/
//队列节点
typedef struct sNode{
   int number;        /*序号域*/
   int value;         /*值域*/
   struct sNode * next; /*指针域*/
}sNode;

//队列
typedef struct QNode{
   struct sNode * front; /*指向队列开头的指针域，删除元素*/
   struct sNode * rear;  /*指向队列末尾的指针域，添加元素*/
}QNode;


QNode * CreateqHeadNode()//创建队列
{
    QNode * head = (QNode*)malloc(sizeof(QNode));
    if(head == NULL){
       printf("申请内存失败!\n");
    return NULL;
    }

    head->front = NULL;
    head->rear  = NULL;
    head->front->number = -1;
    head->front->next = NULL;
    head->rear->number = 0;
    head->rear->next  = NULL;
    return head;
}


QNode * CreateQueueNode(int Data,int Order)//创建队列
{
    QNode * newhead = (QNode*)malloc(sizeof(QNode));
    if(newhead == NULL){
       printf("申请内存失败!\n");
    return NULL;
    }
    newhead->front->number = Order;
    newhead->front->value  = Data;
    newhead->front->next   = NULL;
    newhead->rear->number  = Order;
    newhead->rear->value   = Data;
    newhead->rear->next    = NULL;
    return newhead;
}

void AddQNode(QNode * Ptr ,int Data ,int Order)//添加队列节点
{

    QNode * head = CreateQueueNode(Data,Order);
    if(Ptr->rear->number+1 % MaxSize == Ptr->front->number){
       printf("满\n");
       return NULL;
    }
    head->rear->next = Ptr->rear->next;
    Ptr->rear->next = head->rear;
}

int DeleteQ(QNode * Ptr)//删除队列节点
{
    sNode * FrontCell;
    int FrontElem;
    if( Ptr->front ==NULL){
        printf("空\n");
        return NULL;
    }
    FrontCell = Ptr->front;
    if(Ptr->front == Ptr->rear)
        Ptr->front = Ptr->rear = NULL;
    else
        Ptr->front = Ptr->front->next;
    FrontElem = FrontCell->value;
    free(FrontCell);
    return FrontElem;
}

int main()
{
    QNode * Ptr = CreateqHeadNode();
    AddQNode(Ptr,123,0);
    printf("%d ",DeleteQ(Ptr));
    return 0;
}
