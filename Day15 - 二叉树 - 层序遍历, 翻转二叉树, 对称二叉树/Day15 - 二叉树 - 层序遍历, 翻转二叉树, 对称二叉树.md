# Day15 - 二叉树 - 层序遍历, 翻转二叉树, 对称二叉树

## 1. ✅ 102. 二叉树的层序遍历「[讲解](https://programmercarl.com/0102.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.html)」

- Initial Idea:
    - 利用队列实现的层序遍历之前写过，复习一下
    - 需要每层区分开，使用cnt记录下层新增多少node
- 看讲解后
    - 因为每层结束后天然只剩下一层的node数，所以可以使用len(q)来，就不用cnt了。
    - len(q)不随循环内对q的变化而改变，可以理解为是一个一开始就取好的定值。
- 一口气刷10道层序遍历：
    1. 107. 二叉树的层序遍历 II
        1. return res[::-1]
    2. 199.二叉树的右视图
        1. 每层最后一个才res.append(node.val)
        2. node可以直接在内层循环直接定义，不需要先定义None
    3. 637.二叉树的层平均值
    4. 429.N叉树的层序遍历
    5. 515.在每个树行中找最大值
    6. 116.填充每个节点的下一个右侧节点指针
        1. 一开始如何每次pop两个有点卡住，后来想到不用pop两个，每次pop一个然后指向q[0]即可
        2. 注意最后一个不能再指向下一个了，所以循环迭代次数应该减1.
    7. 117.填充每个节点的下一个右侧节点指针II
    8. 104.二叉树的最大深度
    9. 111.二叉树的最小深度
        1. 耍了小聪明然后翻车：
            1. if node.left, elif node.right, else return直接导致右节点不会被入队
            2. 可以改为if left, if right, elif not left: return

## 2. ✅ ****226.翻转二叉树「[讲解](https://programmercarl.com/0226.%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91.html)」**

- 没太多想就层序+交换左右子树了，想象中就是每两个换位置。确实像卡哥所说，容易稀里糊涂就对了。
- 原理在于只要每个节点的子树只交换过一次，整体就是翻转。

## 3. ✅ ****101. 对称二叉树「[讲解](https://programmercarl.com/0101.%E5%AF%B9%E7%A7%B0%E4%BA%8C%E5%8F%89%E6%A0%91.html#%E9%80%92%E5%BD%92%E6%B3%95)」**

- Initial Idea
    - 层序遍历，每层维护一个栈，类似括号检测，保证每层对称。跑出来时空效率都很差，因为需要保存所有的None节点。
    - 双端队列，根节点的左右子树做类似前序的对称入队出队，一旦发现不同即可return False。
- 看讲解后：
    - 主要思想是根节点左右子树同步递归/迭代。
    - 迭代法就是我自己想的第二个方法的思路，但可以不用非要在一个队列里，左右各自维护一个队列即可。
    - 递归法这样理解：递归函数一开始设计的时候是一个虚的概念，比如最开始需要比较根节点的左右子树是否对称，那么需要比较左的左和右的右，左的右和右的左，这就是递归线路。
    - 可以再写一遍递归法。