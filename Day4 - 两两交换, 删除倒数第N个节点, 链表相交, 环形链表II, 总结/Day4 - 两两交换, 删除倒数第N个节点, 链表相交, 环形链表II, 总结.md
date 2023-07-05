# Day4 - 两两交换, 删除倒数第N个节点, 链表相交, 环形链表II, 总结

## 1. ✅ leetcode ****24: 两两交换链表中的节点 [[讲解](https://programmercarl.com/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html)]**

- Initial Idea:
    - while loop: pre, cur, tmp
    - 相比revLinkedList, 需要在初始化和循环条件中设计pre, curLeft, curRight的用法
        - 初始条件：pre = dummyHead, curLeft = Head
        - while (curLeft and curLeft.next) # 这样跳出循环时只需要把curLeft作为末尾节点即可，如果curLeft is not None则是单数个，不用换；如果是None，正好。
- bugs：
    - while loop结束的赋值写成了pre = curRight，但是交换后已经变为curLeft了。
- 讲解：
    
    > 一定要画图，不画图，操作多个指针很容易乱，而且要操作的先后顺序
    > 

## 2. ✅ leetcode 19: ****删除链表的倒数第N个节点 [[讲解](https://programmercarl.com/0019.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B9.html#_19-%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACn%E4%B8%AA%E8%8A%82%E7%82%B9)]**

- initial idea:
    - 找到倒数第n个：递归+搜一遍还得倒回来，不论递归还是转成数组都是O(n)的内存，直接list. 设一个dummyHead然后直接del list[-n-1]
- 看讲解后：
    - 双指针法，快指针提前慢指针n+1步，然后fastP is None的时候删掉slowP.next
    - 这里的设计在于没有前驱指针，所以要slowP找到的是obj的前一个，所以要快n+1步。具体快几步选个例子算一下就好。
    - 空间复杂度O(1)

## 3. ✅ leetcode 面试题02.07: 链表相交 [[讲解](https://programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html#%E6%80%9D%E8%B7%AF)]

- Initial Idea:
    - 一开始没看懂题意，原来是要找ListNode对象相同的节点
- 看讲解后：
    - 先实现了讲解中写的第一个方法：因为相交后必须一直相交，所以末尾对齐，然后从前端开始往后迭代，时间O(n)空间O(1)
    - 这样的写法的问题是过两遍链表，而且中间还要判断哪个长哪个短。
- 看leetcode题解：
    - a-c and b-c → a+b-c = a+b-c。所以让两个链表相连，指针相同时就是相交点或Nul

## 4.  ✅ leetcode 142: 环形链表II [[讲解](https://leetcode.cn/problems/linked-list-cycle-ii/solution/linked-list-cycle-ii-kuai-man-zhi-zhen-shuang-zhi-/)]

- Initial Idea：
    - 没什么想法，一开始只能想到hashmap
- 看讲解后：
    - 这类链表题目一般都是使用双指针法解决的，例如寻找距离尾部第 K 个节点、寻找环入口、寻找公共尾部入口等。
    - 这种链表切分成多段的，通常将不同段设未知数，然后计算一个规律，再用双指针/有时候再多一个指针（只要是常数个就行）自动化的实现规律