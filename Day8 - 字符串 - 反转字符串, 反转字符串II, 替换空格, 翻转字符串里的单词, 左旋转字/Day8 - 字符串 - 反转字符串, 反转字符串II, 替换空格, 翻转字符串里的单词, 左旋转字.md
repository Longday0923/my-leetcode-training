# Day8 - 字符串 - 反转字符串, 反转字符串II, 替换空格, 翻转字符串里的单词, 左旋转字符串

## 1. ✅ leetcode ****344. 反转字符串「[讲解](https://programmercarl.com/0344.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)」**

- 要求原地操作：
    - s[::-1]，s.reverse()，[s[i] for i …]均生成新的list
    - 双指针从两侧对称交换
- 讲解：
    - while i<j 比 for i in range(len // 2)慢，因为每次循环要比较？实测不然，猜测因为range内部要计算j对应元素的索引

## 2. ✅ leetcode ****541. 反转字符串II「[讲解](https://programmercarl.com/0541.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2II.html)」**

- Initial Idea
    - 每次往前走2k, 最后一次根据还剩多长判断如何reverse，写一个reverseSlice的函数
    - 循环条件的边界和函数的边界分清各自的定义
- 看讲解后：
    - string的slice：
        - s[len(s):]返回”“, s[3:len(s)+10]返回s[3:len(s)]
        - 按照这种自适应的选择可以：
            - 每次传给reverse函数的选择可以简化
            - 直接写成s = p之前+p:2p+2p之后三段的和，这样不用定义list，虽然也是每次都多了memory

## 3. ✅ ****剑指Offer 05. 替换空格「[讲解](https://programmercarl.com/%E5%89%91%E6%8C%87Offer05.%E6%9B%BF%E6%8D%A2%E7%A9%BA%E6%A0%BC.html)」**

- 这题直接用python的string操作了，练习两种写法
    - s.replace(” ”, “%20”)
    - “%20”.join(s.split(” ”))
- 看懂了讲解的双指针法：后缀方法 + 快慢指针

## 4. ✅ leetcode ****151. 翻转字符串里的单词「[讲解](https://programmercarl.com/0151.%E7%BF%BB%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%E9%87%8C%E7%9A%84%E5%8D%95%E8%AF%8D.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)」**

- Initial Idea：
    - 直接python built-in function了。
    - split()可直接去掉所有多余空格并切分为单词，然后再“ ”.join(s[::-1])即可
- 看讲解后：
    - 整体思想：双指针清楚多余空格 → 整体反转 + 单词内部反转
    - 练一下双指针的列表替换：
        - 单独写一个循环让fast跳过开头空格
        - 中间的空格因为要保留一个，所以在while loop里限制性一次s[slow] = s[fast]，再while fast < len and s[fast]==” ” and s[fast - 1]==” ”跳过多余空格
            - 注意while loop条件：边界条件先写 and 主要条件。while 是判断条件不成立时跳出，所以一旦第一个边界条件不满足，就不会判断后半部分了。
            - if不能这么用！还不知道为什么。
        - 结尾的如何处理？考虑两种情况下最终两个指针的表现：
            1. 结尾不是空格：fast = len(s), s[slow - 1]不是空格，return s[:slow]
            2. 结尾时是空格（1个或n个）：fast = len(s), s[slow - 1]是空格，这里应该有且只有一个有效空格：return s[:slow - 1]
            
            这里不应该用s[slow]判断！因为跳出while的slow是最后一次复制fast的下一个，有可能越界，有可能是原本已经复制过的靠后的字符，也有可能是空格，无法用来判断。所以要看最后一次复制的是什么！
            

## 5. ✅ ****剑指Offer58-II. 左旋转字符串「[讲解](https://programmercarl.com/%E5%89%91%E6%8C%87Offer58-II.%E5%B7%A6%E6%97%8B%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)」**

- Initial Idea:
    - 没理解空间发复杂度O(1)的含义，应该是只能两两交换的意思，如果直接保存整个需要旋转的字符则是O(k)。
- 如何只用两两交换实现？回想上一题的两次反转方法。