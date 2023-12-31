# Day21 - 二叉树 - 二叉搜索树的最小绝对差, 二叉搜索树中的众数, 二叉树的最近公共祖先

## 1.✅530.二叉搜索树的最小绝对差「[讲解](https://programmercarl.com/0530.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E7%9A%84%E6%9C%80%E5%B0%8F%E7%BB%9D%E5%AF%B9%E5%B7%AE.html)」

- 常规中序遍历然后记录preVal和minDiff，初始化为float(”inf”)即可
- 讲解：
    - 也可以保存上一个节点而非节点的值，加一个not None判断即可。

## 2.✅****501.二叉搜索树中的众数「[讲解](https://programmercarl.com/0501.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E4%B8%AD%E7%9A%84%E4%BC%97%E6%95%B0.html)」**

- Initial Idea:
    - 题目要求不能用额外空间，一开始认为众数可能很多，空间复杂度是O(n)的，必须要用到。
- 看讲解：
    - 理解为：过程中记录众数是必须而为之，其他不能多用。
    - 思路就清晰了，首先是常规二叉搜索树的中序遍历，然后中间节点的处理分为两部分：
        - 首先检查node.val
            - ==preVal, cnt += 1
            - preVal, cnt = 1
            - 如果记录的是preNode, 还需要写一个if preNode is None: cnt = 1
        - 根据cnt:
            - ==maxCnt, res.append(node.val)
            - >maxCnt, res = [node.val]
    - 写当前node递归内操作时，不要稀里糊涂if 套 if，一步一步检查然后操作。
- 尝试用node = node.left的写法实现迭代，应该是不行的，这样会在while node中死循环。中序遍历必须递归，否则需要辅助栈。

## 3.✅****236. 二叉树的最近公共祖先「[讲解](https://programmercarl.com/0236.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E8%BF%91%E5%85%AC%E5%85%B1%E7%A5%96%E5%85%88.html)」**

- Initial Idea:
    - 图省事儿，很多值都设成了global。
    - 我设计后序递归每次返回的是p和q是否找到了，两个flag
        - 为了让上层不覆盖下层，所以还设了一个foundFlag
        - 因为每次需要node合法才进入，所以还需要设计递归内p, q的flag，与左右子节点递归返回结果取or
        - 还单设了一个res
- 看讲解后：
    - 分析给出函数的参数：
        - root, p, q：应该不论递归到什么节点都是这三个参数，含义都是一样的
        - 是否能够设计通用的返回值：
            - 返回值类型：node
            - 若都没找到：返回None
            - 找到任意一个节点：返回该节点
            - 在某一节点两个都找到：返回该节点
    - 练习编写
    - 和我自己洗的方法对比：
        - 首先一个比较巧妙的设计是当node == p or q的时候直接返回node，如果p or q一个是另一个的祖先，那么后遍历到的直接覆盖之前的递归返回值即可
        - 排除上面这种情况后，就只剩正常的共同祖先，这时根据左右子树的返回值判断即可。
        - 这种写法的返回值同时表示了很多含义：
            - return None说明当前节点没找到p or q
                1. 当前节点为None
                2. 当前节点下没有p or q
            - return 是Node有以下几种情况：
                1. return的就是p or q说明当前节点已经找到了p or q
                2. return的是最近公共祖先，是我们想要的结果
            - 这种写法里，为什么正确答案不会被覆盖：因为返回的是节点。不论是p, q还是公共祖先，只会出现一次符合要求的情况。一旦经过了最近公共祖先，就不会再出现左右都不为None的情况了。这个公共祖先就可以被一直返回出去。