# 2 Add Two Numbers
### 1.传统数学解法
>具体思路---[LeetCode Solution Approach1](https://leetcode.com/problems/add-two-numbers/solution/)
##### C++
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *l3=NULL;//L3头指针
        ListNode **node=&l3;//node为指向L3头指针的指针
        ListNode *p=l1;//P指针指向L1链表
        ListNode *q=l2;//q指针指向L2链表
        int carry=0;//设置进位标志,默认为0
        int x,y;//用于表示p,q指针指向的值
        int sum=0;
        while(p!=NULL||q!=NULL)
        {
           //由于题设链表是反向的，所以头结点的下一个节点是最低有效位
           //从链表开始节点遍历，用于模仿传统计算方法
           //如果p,q某一个到达了链表END，就将x或y设置为0，否则正常赋值
            if(p!=NULL)  
            {
                x=p->val;
                p=p->next;
            }
            else x=0;
            if(q!=NULL)
            {
                y=q->val;
                q=q->next;
            }
            else y=0;
            sum=x+y+carry;
            //判断是否溢出,如果溢出则carry值设置为1，否则依旧为零
            carry=sum/10;
            (*node)=new ListNode(sum%10);
            (*node)->next=NULL;//next置空后前移
            node=&((*node)->next);  
        }
        if(carry==1)
        {
            (*node)=new ListNode(1);
            (*node)->next=NULL;//next置空后前移
        }
        return l3;
    }
};
```
---
##### python
```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        carry=0
        l3=ListNode(0)
        node=l3
        while l1 or l2:
            if l1==None:
                x=0
            else:
                x=l1.val
                l1=l1.next
            if l2==None:
                y=0
            else:
                y=l2.val
                l2=l2.next
            sum=x+y+carry
            carry=sum//10 
            node.val=sum%10
            p=node #倒数第二个节点
            node.next=ListNode(0)
            node=node.next
        if carry==1:
            node.val=carry
        else:
            p.next=None
        return l3
  
```
---
### 2.递归解法
##### 递归解法后续会补上