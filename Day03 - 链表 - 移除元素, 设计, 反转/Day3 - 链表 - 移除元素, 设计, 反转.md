# Day3 - 链表 - 移除元素, 设计, 反转

## 1. ✅ leetcode 203: 移除链表元素 [[讲解](https://programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html)]

- Initial Idea:
    - dummy head
    - pre.next = cur.next
- bugs:
    - 无论是否删除：pre, cur = pre.next, pre.next.next
        - 如果删除后pre.next已经为None就会出问题
    - 逻辑根本就错了，如果删掉的话，pre应该不变
        - 所以应该分情况讨论
- 讲解

## 2. ✅ leetcode 707: 设计链表 [[讲解](https://programmercarl.com/0707.%E8%AE%BE%E8%AE%A1%E9%93%BE%E8%A1%A8.html)]

- Initial Idea：
    - 一开始再纠结是否要head和tail都dummy，后来发现addIndex = length时候最方便的还是有一个dummyTail
- bugs:
    - while的条件 + 出来之后没考虑p = dummyTail.next的情况
        - 应该让while出来要么是target要么是dummyTail
- 讲解

## 3. ✅ leetcode 206: 反转链表 [[讲解](https://programmercarl.com/0206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.html#%E5%8F%8C%E6%8C%87%E9%92%88%E6%B3%95)]

- Initial Idea:
    - 可以迭代和也可以递归，递归不是很熟练，练一下
        - 创一个dummyHead, 递归最内层接在最后一个node后面
- Bugs:
    
    <aside>
    💡 pre, cur设成了head, head.next导致最后没有把head.next改为None，导致形成闭环，输出错误。
    
    </aside>
    
    ```python
    if cur is None: return dummyHead
    revCur.next = pre # 导致丢掉最后一个node
    ```
    
- 看讲解后：
    - 理解很关键：暂存cur.next，然后修改link的方向，然后再把cur和next赋值给pre和cur。