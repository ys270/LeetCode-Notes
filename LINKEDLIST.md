## 1.LINKEDLIST

160. intersection of two nodes

idea: the two linked list A, B will intersect at a point when A, B  both pass same amount of nodes, when A reaches the end, let it restart from B, else, let B restart from A.

If the two list do not intersect with each other, they will both reach NULL and break out of the while loop.

Time complexity: O(n)

**Example 1:**

[![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
Output: Reference of the node with value = 8
```

```c++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* a=headA;
        ListNode* b=headB;
        while(a!=b){
            if(a==NULL){
                a=headB;
            }
            else{
                a=a->next;
            }
            if(b==NULL){
                b=headA;
            }
            else{
                b=b->next;
            }
        }
        return a;
     }
};
```

206. Reverse linked list

     ```c++
     Approach 1: iterative
     
     ListNode * reverseList(ListNode* head) {
         ListNode * curr = head;
         ListNode * prev = NULL;
         while(curr!=NULL){
             ListNode* temp = curr->next;
             curr->next = prev;
             prev = curr;
             curr = temp;
             }
             return prev;
         }
     
     O(N)
     ```

     ```c++
     Approach 2:recursive
     
     ListNode * reverseList(ListNode* head) {
         if(head==NULL||head->next == NULL){
             return head;
         }
         ListNode * p = reverseList(head->next);
     
        head->next->next = head;
     
        head->next = NULL;
        return p;
      }
     
     O(N)
     ```

     

     

21. Merge two sorted list

    Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

    **Example:**

    ```
    Input: 1->2->4, 1->3->4
    Output: 1->1->2->3->4->4
    ```

    <font color=red size=3> Approach 1: iterative</font>

    ```c++
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode * dummy = new ListNode(0);
        ListNode * head = dummy;
        while(l1&&l2){
            if(l1->val<l2->val){
                dummy->next = l1;
                l1 = l1->next;
            }
            else{
                dummy->next = l2;
                l2 = l2->next;
            }
            dummy = dummy->next;
        }
            dummy->next = l1!=NULL?l1:l2;
            return head->next;
        }
    ```

    <font color=red size=3>Approach 2: recursive!!!!!!(still need to look)</font>

    ```c++
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == NULL){return l2;}
        if(l2 == NULL){return l1;}
        if(l1->val<l2->val){
            l1->next = mergeTwoLists(l1->next,l2);
            return l1; 
        }
        else{
            l2->next = mergeTwoLists(l1,l2->next);
            return l2;
        }
        }
    ```

208. remove duplicates from sorted list

     **Example 1:**

     ```
     Input: 1->1->2
     Output: 1->2
     ```

     **Example 2:**

     ```
     Input: 1->1->2->3->3
     Output: 1->2->3
     ```

     <font color = red size = 3>recursive!!(still need to look)</font>

     ```c++
     ListNode* deleteDuplicates(ListNode* head) {
         if(head == NULL||head->next == NULL){return head;}
         head->next = deleteDuplicates(head->next);
         return (head->val == head->next->val ? head->next:head);
         }
     ```

     19. Remove Nth Node From End of List

     Given a linked list, remove the *n*-th node from the end of list and return its head.

     **Example:**

     ```
     Given linked list: 1->2->3->4->5, and n = 2.
     
     After removing the second node from the end, the linked list becomes 1->2->3->5.
     ```

     <font color = red size = 3>make last n+1before first !</font>

     ```c++
     ListNode* removeNthFromEnd(ListNode* head, int n) {
         if(head==NULL||n==0){return head;}
             ListNode * first = head;
             while(n>0){
                 first = first->next;
                 n--;
             }
             if(first == NULL){
                 return head->next;
             }
             first = first->next;
             ListNode * last = head;
             while(first!=NULL){
                 first = first->next;
                 last = last->next;
             }
             last->next = last->next->next;
             return head;
         }
     ```

     

24. Swap Nodes in Pairs

Given a linked list, swap every two adjacent nodes and return its head.

You may **not** modify the values in the list's nodes, only nodes itself may be changed.

**Example:**

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

```c++
approach 1:
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(head == NULL || head->next == NULL){
            return head;
        }
        ListNode* a = head;
        ListNode* b = head->next;
        ListNode* c = head->next->next;
        b->next = a;
        a->next = swapPairs(c);
        return b;
    }
};
```

```c++
approach 2:
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
    ListNode* prev = new ListNode(-1);
    prev->next = head;
    ListNode * node = prev;
    while(prev->next!=NULL&&prev->next->next!=NULL){
        ListNode * a = prev->next;
        ListNode * b = prev->next->next;
        a->next = b->next;
        b->next = a;
        prev->next = b;
        prev = a;
    }
        return node->next;
    }
};
```

445. Add Two Numbers II

You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**

```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

```c++
approach1:(using stack--avoid reversing the linked list)
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
     stack<int> s1,s2;
     buildstack(l1,s1);
     buildstack(l2,s2);
     ListNode * newlist = NULL;
     int cout = 0;
     while(s1.size()>0||s2.size()>0||cout==1){
         int x = s1.size()>0?s1.top():0;
         int y = s2.size()>0?s2.top():0;
         int sum = x+y+cout;
         cout = sum / 10;
         sum = sum % 10;
         if(s1.size()>0){
            s1.pop();
         }
         if(s2.size()>0){
            s2.pop();   
         }
         ListNode* newnode = new ListNode(sum);
         newnode->next = newlist;
         newlist = newnode;
     }
        return newlist;   
    }
    
    void buildstack(ListNode* head,stack<int> & s){
        while(head!=NULL){
            s.push(head->val);
            head = head->next;
        }
    }
};
```

```c++
approach 2: reverse the list first
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        l1 = reverselist(l1);
        l2 = reverselist(l2);
        ListNode * newlist= NULL;
        int sum = 0;
        int cout = 0;
        while(l1!=NULL&&l2!=NULL){
            sum = l1->val + l2->val + cout;
            if(sum>=10){
                cout = 1;
                sum = sum - 10;
            }
            else{
                cout = 0;
            }
            l1 = l1->next;
            l2 = l2->next;
            ListNode * newadd = new ListNode(sum);
            newadd->next = newlist;
            newlist = newadd;
        }
        while(l1!=NULL){
            sum = l1->val+cout;
            if(sum>=10){
                cout = 1;
                sum = sum - 10;
            }
            else{
                cout = 0;
            }
            l1 = l1->next;
            ListNode * newadd = new ListNode(sum);
            newadd->next = newlist;
            newlist = newadd;
        }
        while(l2!=NULL){
            sum = l2->val+cout;
            l2 = l2->next;
            if(sum>=10){
                cout = 1;
                sum = sum - 10;
            }
            else{
                cout = 0;
            }
            ListNode * newadd = new ListNode(sum);
            newadd->next = newlist;
            newlist = newadd;
        }
        if(cout==1){
           ListNode * newadd = new ListNode(1);
           newadd->next = newlist;
           newlist = newadd;
        }
        return newlist;
    }
    
    ListNode * reverselist(ListNode* l){
        if(l == NULL||l->next==NULL){
            return l;
        }
       ListNode * p = reverselist(l->next);
       l->next->next=l;
       l->next = NULL;
        return p;
    }
};
```

234. Palindrome Linked List

Given a singly linked list, determine if it is a palindrome.

**Example 1:**

```
Input: 1->2
Output: false
```

**Example 2:**

```
Input: 1->2->2->1
Output: true
```

```c++
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        if(head==NULL||head->next==NULL){
            return true;
        }
        ListNode * slow = head;
        ListNode * fast = head->next;
        while(fast!=NULL&&fast->next!=NULL){
            fast = fast ->next->next;
            slow =slow->next;
        }
        if(fast!= NULL){
            slow = slow->next;//统一list长度为奇数和偶数两种情况
        }
        cutlist(head,slow);
        slow = reverse(slow);
        while(head!=NULL&&slow!=NULL){
            if(slow->val!=head->val){
                return false;
            }
            slow = slow->next;
            head = head->next;
        }
        return true;     
    }
    void cutlist(ListNode* head,ListNode* slow){
        while(head->next!=slow){
            head = head->next;    
        }
        head->next = NULL;
    }
    ListNode* reverse(ListNode * head){
        if(head==NULL||head->next ==NULL){
            return head;
        }
        ListNode * p = reverse(head->next);
        head->next->next = head;
        head->next = NULL;
        return p;
    }
};
```

725. Split Linked List in Parts

Given a (singly) linked list with head node `root`, write a function to split the linked list into `k` consecutive linked list "parts".

The length of each part should be as equal as possible: no two parts should have a size differing by more than 1. This may lead to some parts being null.

The parts should be in order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal parts occurring later.

Return a List of ListNode's representing the linked list parts that are formed.

Examples 1->2->3->4, k = 5 // 5 equal parts [ [1], [2], [3], [4], null ]

**Example 1:**

```
Input:
root = [1, 2, 3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The input and each element of the output are ListNodes, not arrays.
For example, the input root has root.val = 1, root.next.val = 2, \root.next.next.val = 3, and root.next.next.next = null.
The first element output[0] has output[0].val = 1, output[0].next = null.
The last element output[4] is null, but it's string representation as a ListNode is [].
```

```c++
class Solution {
public:
    vector<ListNode*> splitListToParts(ListNode* root, int k) {
        int count = 0;
        ListNode* curr = root;
        while(curr!=NULL){
            count++;
            curr = curr->next;
        }
        int avg = count / k;
        int remain = count % k;
        vector<ListNode*> res;
        while(k>0){
            k--;
            res.push_back(root);
            if(remain>0){
                int c = avg + 1;
                remain--;
                while(c>1){
                   root = root->next;
                    c--;
                }
                ListNode* temp = root->next;
                root->next =NULL;
                root = temp;
            }
            else if(remain==0&&root!=NULL){
                int c = avg;
                while(c>1){
                    root = root->next;
                    c--;
                }
                ListNode* temp = root->next;
                root->next =NULL;
                root = temp;
            }
        }
        return res;
    }
};
```

328. Odd Even Linked List

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

**Example 1:**

```
Input: 1->2->3->4->5->NULL
Output: 1->3->5->2->4->NULL
```

**Example 2:**

```
Input: 2->1->3->5->6->4->7->NULL
Output: 2->3->6->7->1->5->4->NULL
```

```c++
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if(head == NULL||head->next == NULL){
            return head;
        }
        ListNode* odd = head;
        ListNode* even = head->next;
        ListNode* evenhead = even;
        while(even!=NULL&&even->next != NULL){
            odd->next = odd->next->next;
            odd = odd->next;
            even->next = even->next->next;
            even = even->next;
        }
        odd->next = evenhead;
        return head;
    }
};
```

