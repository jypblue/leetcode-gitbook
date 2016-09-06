#  19. Remove Nth Node From End of List 

##### Tags
1. Linked List
2. Two Pointers

>  Given a linked list, remove the n<sup>th</sup> node from the end of list and return its head.
>
>  For example,
>
``` Given linked list: 1->2->3->4->5, and n = 2.
 After removing the second node from the end, the linked list becomes 1->2->3->5.
```


##### 题意：
给定一个链接List,去除List中倒数第n个数字后返回该List本身

##### 分析：
本题涉及到链表，前后链接，因为倒序所以不能想正序那样一开始循环走到指定位置，然后将前后节点链接起来。但是呢，思路其实也跟这个差不多，毕竟是链表。只不过需要拐个弯，我们可以类似于做个减法，总长度减去倒序长度，就是正序走的长度了。因此，具体到链表结构，我们只需要设定前后双指针即可，prev指针先跑n步，然后next指针再跟着prev指针一起往后跑，知道prev到达链表终点，next指针所在位置，就是链表正序时所要去除节点的位置。

##### 思路：
通过分析，本题解题思路如下：

1. 新建两个指针faster,slower
2. faster指针先向后移动n步
3. slower指针和faster指针同时相后移动，知道faster.next为null时，即已经跑到链表末尾时停止移动，此时slower指针所在位置就是需要去除的节点
4. 按照该位置的前节点与后节点连接，去除该节点，然后返回该链表

总体思路都差不多，具体实现大同小异。

##### Js实现：
##### 复杂度
时间复杂度O(n)

```
let removeNthFromEnd = function(head,n) {

 if(head === null || head.next === null) return null;

 let faster = head;

 let slower = head;

 for(let i = 0; i<n; i++)

   faster = faster.next;

   if(faster === null){

   head = head.next;

   return head;

 }

 while(faster.next !== null){

   slower = slower.next;

   faster = faster.next;

 }

 slower.next = slower.next.next;

 return head;

}

```



