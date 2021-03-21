# -
数据结构实验一
```
#include <stdio.h>
#include <stdlib.h> 
#include <stdbool.h>
#define ElemType int 


// 定义
typedef struct LNode{
	ElemType Data;            //数据域
	struct LNode *Next;      //指针域
	int length;
}LNode,*LinkList;

LinkList CreateList_Head(LinkList L);          // 以头插法创建单链表
LinkList CreateList_Tail(LinkList L);			// 以尾插法创建单链表
bool ReverseLink(LinkList &L);					// 链表的反转
bool LinkListMerge(LinkList a,LinkList b,LinkList c);	//链表的合并
bool LinkListMerge11(LinkList a,LinkList b,LinkList c);	//链表的合并
LinkList Get_Common(LinkList a,LinkList b);				//链表的合并
LinkList MutualLinkList444(LinkList a,LinkList b);		//链表的合并
void PrintListqq(LinkList L);							//打印链表	
LinkList GetElem(LinkList l,int i);						//按位序查找
LinkList LocateElem(LinkList l,ElemType e);				//按值查找
LinkList Delete(LinkList l,int i);						//删除结点
LinkList Delete1(LinkList l,int i);						//删除结点
void PrintList(LinkList L);								//打印链表
LinkList Insertion(LinkList l,int i,int x);				//插入函数
LinkList LocateElem2(LinkList l,ElemType e); //这个直接打印出位置main直接调用就可以了
// 主函数
int main()
{
	LinkList a,b,c,f;
	printf("请创建a链表,输入9999结束\n");
	a=CreateList_Tail(a);
	printf("创建完毕，链表如下：\n");
	PrintList(a);
	printf("请创建b链表,输入9999结束\n");
	b=CreateList_Tail(b);
	printf("创建完毕，链表如下：\n");
	PrintList(b);
	//printf("取a和b链表的交集合并成c链表，链表如下:\n");
	//c=MutualLinkList444(a,b);
	//PrintList(c);
	printf("查找序号为2序号开始查找\n");
	if(GetElem(a,2)!=NULL){
		printf("该序号查找到的值为：%d\n",GetElem(a,2)->Data);
		}
	else{
		printf("没有找到序号2的结点");
	}
	printf("\n查找值为2按值开始查找\n");

	if(LocateElem(a,2)!=NULL){
		printf("按该值查找到的值为：%d\n",LocateElem(a,2)->Data);
	}
	else{
		printf("没有值为2的结点");
	}

	printf("\n删除第二个结点之后的链表如下:\n");
	PrintList(Delete(a,2));
	printf("将元素87，插入第2个位置\n");
	Insertion(a,2,87);
	PrintList(a);
	printf("弄完了\n");
	return 0;
	
}

//打印函数
void PrintList(LinkList L)
{
    LinkList p;
	if(L==NULL)
		printf("没有找到\n");
	else 
	{
	p=L->Next;
	printf("链表元素如下：\n");
    while(p!=NULL)
    {
        printf("%d ",p->Data);
        p=p->Next;
    }
    printf("\n");
	}
}

//1.头插法
LinkList CreateList_Head(LinkList L)       //函数的定义
{
	LinkList s; int x;
	L = (LNode*)malloc(sizeof(LNode));     //创建头结点 
	L->Next=NULL;                          
	scanf("%d",&x);                       
	while(x!=9999){                             
		s=(LNode*)malloc(sizeof(LNode));  
		s->Data=x;                           
		s->Next=L->Next;                      
		L->Next=s;                          //插入结点
		scanf("%d",&x);
		L->length++;
	}
	return L;
}

//2.尾插法
LinkList CreateList_Tail(LinkList L)
{
	int x;
	int k;
	L = (LNode*)malloc(sizeof(LNode));
	LNode *s,*r=L;
	
	scanf("%d",&x);
	while(x!=9999){                             
		s=(LNode*)malloc(sizeof(LNode));     //创建新的结点 
		s->Data=x;                           
		r->Next=s;                      
		r=s;
		scanf("%d",&x);
		k++;
		
	}
	r->Next=NULL;
	L->length=k;
	printf("长度为：%d\n",L->length);
	return L;
 } 

// 链表倒置
bool ReverseLink(LinkList &L){
	LinkList q,p,s;
	p=L->Next;
	q=p->Next;
	s=q->Next;
	p->Next=NULL;
	while(s->Next){
		int i=1;
		
		q->Next=p;
		p=q;q=s;s=s->Next;
		i++;
		printf("p是：%d，q是：%d，s是：%d\n",p->Data,q->Data,s->Data);

	}
	q->Next=p;s->Next=q;L->Next=s;
	return true;
}

// 链表的合并
bool LinkListMerge(LinkList a,LinkList b,LinkList c){
	LNode *p,*q,*pc,*r,*s;
	p=a->Next,q=b->Next;
	pc=(LNode*)malloc(sizeof(LNode));
	c=pc;
	while(a&&b){
		if(p->Data < q->Data){
			//s->Next=p;
			if(p->Next!=NULL){
				p=p->Next;
			}
		}
		if(p->Next==NULL){
				p=a->Next;
				q=q->Next;
			}
		if(p->Data > q->Data){
			if(q->Next!=NULL){
				q=q->Next;
			}
		}
		if(q->Next==NULL){
				q=b->Next;
				p=p->Next;
			}
		if(p->Data==q->Data&&q->Next!=NULL&&p->Next!=NULL){
			s=(LNode*)malloc(sizeof(LNode));
			s->Data=p->Data;
			pc->Next=s;
			pc=s;
			p=p->Next;
			q=q->Next;
		}
	}
	return true;
}

// 答案给的
bool LinkListMerge11(LinkList a,LinkList b,LinkList c){
	LNode *p,*q,*pc,*r,*s;
	p=a->Next,q=b->Next;
	pc=(LNode*)malloc(sizeof(LNode));
	c=pc;
	while(a&&b){
		if(p->Data < q->Data){
				p=p->Next;
		}
		else if(p->Data > q->Data){
				q=q->Next;
		}
		else{
			s=(LNode*)malloc(sizeof(LNode));
			s->Data=p->Data;
			pc->Next=s;
			pc=s;
			p=p->Next;
			q=q->Next;
		}
	}
	return true;
}

// 参考书上的
LinkList Get_Common(LinkList a,LinkList b){
	LNode *p=a->Next,*q=b->Next,*r,*s;
	LinkList c=(LinkList)malloc(sizeof(LNode));
	r=c;
	while (p!=NULL&&q!=NULL)
	{
		if(p->Data<q->Data)
			p=p->Next;
		else if(p->Data>q->Data)
			q=q->Next;
		else{
			s=(LNode*)malloc(sizeof(LNode));
			s->Data=p->Data;
			r->Next=s;
			r=s;
			p=p->Next;
			q=q->Next;
		
		}
	}
	r->Next=NULL;
	return c;
	
}
// 改进的算法
LinkList MutualLinkList444(LinkList a,LinkList b) {  // a∩b
    LNode *C,*pa,*pb,*pc,*qc;
	//LinkList *pa;
   	C = pc = (LinkList )malloc(sizeof(LinkList));
    pc->Data = 0;
    pa = a->Next;
    pb = b;
    while(pa != NULL) {
        pb = b->Next;
        while(pb != NULL) {
            if(pb->Data == pa->Data) {
                qc = (LinkList)malloc(sizeof(LinkList));
                qc->Data = pb->Data;
                pc->Next = qc;
                pc = qc;
            }
            pb = pb->Next;
        }
        pa = pa->Next;
    }
    pc->Next = NULL;
    return C;
}

// 按序号查找结点值
LinkList GetElem(LinkList l,int i){
	int j=1;
	LNode *p=l->Next;
	if(i==0)
		return l;
	if(i<1)
		return NULL;
	if(i>l->length)
		return NULL;
	while (p&&j<i)
	{
		p=p->Next;
		j++;
	}
	return p;
	
}

// 按值查找
LinkList LocateElem(LinkList l,ElemType e){
	LNode *p=l->Next;
	
	while (p!=NULL&&p->Data!=e)
	{
		p=p->Next;

	}
	//if(p==NULL) return NULL;
	return p;
	
}



LinkList LocateElem2(LinkList l,ElemType e){
	LNode *p=l->Next;
	int m=0;
	while (p!=NULL)
	{
		if(p->Data==e&&p!=NULL){
			printf("在第%d个位置发现要查找的\n",m);
		}
		p=p->Next;
		m++;
		

	}
	//if(p==NULL) return NULL;
	return p;
	
}

// 删除
LinkList Delete(LinkList l,int i){
	if(GetElem(l,i)==NULL)
		return NULL;
	else {
		LNode *p,*q;
		p=GetElem(l,i);
		
		if(p->Next==NULL){
			q=GetElem(l,i-1);
			q->Next=NULL;
			/*p=NULL;
			free(p);
			return l;*/
		}
		else {
		q=p->Next;
		p->Data=p->Next->Data;
		p->Next=q->Next;
		free(q);
		}
		return l;
		
	}
}


// 插入结点
 LinkList Insertion(LinkList l,int i,int x){
	LNode *p,*s;
	p=GetElem(l,i-1);
	if(p==NULL){
		printf("超出了\n");
		return l;
	}
	s->Data=x;
	s->Next=p->Next;
	p->Next=s;
	return l;
 }







```
