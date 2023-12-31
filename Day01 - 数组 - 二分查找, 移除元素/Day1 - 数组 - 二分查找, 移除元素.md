# Day1 - 数组 - 二分查找, 移除元素

> 代码随想录算法训练营第1天
> 

## 二分查找

### TL;DR

搜索区间的**开闭** - 决定 - 边界条件：

1. 循环（left ? right）是否有等号
2. mid给下一轮的赋值（left/right = mid ? 1）是否+-1

时间复杂度：O(logN)，空间复杂度：O(1)。

<aside>
💡 个人倾向用“闭”搜索区间

</aside>

### 经典例题

1. ✅ [leetcode 704: 二分查找](https://leetcode.cn/problems/binary-search/) [[讲解](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html#_704-%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE)]
2. ✅ [leetcode 35: 搜索插入位置](https://leetcode.cn/problems/search-insert-position/) [[讲解](https://programmercarl.com/0035.%E6%90%9C%E7%B4%A2%E6%8F%92%E5%85%A5%E4%BD%8D%E7%BD%AE.html)]
    - Initial Idea:
        - 相当于分析二分查找后，最终状态下left和right的模式（二分查找最后一步的行为）：
        - 若使用[left, right]：
            - (left = right) → **(left = right + 1)**: nums[right] < target
            - (left = right) → **(right = left - 1)**: nums[left] > target
        - 若使用[left, right): 跳出循环时left==right，就没办法直接判断了。
    - Bugs:
        
        <aside>
        ❗ 有点问题: left = right + 1 和 -1是等价的
        
        </aside>
        
    - 看解析：
        - 4种情况最后一步行为：(left, right)
            
            ![Untitled](Untitled.png)
            
            1. … → (0, 0) → (0, -1), 此时应输出left
            2. … → (1, 1) → return mid=1
            3. (0, 3) → (1, 3) → (2, 3) → (3, 3) → (3, 2), 此时应输出left
                
                若target = 2：(0, 3) → (0, 1) → (1, 1) → (1, 0), 此时应输出left
                
            4. … → (3, 3) → (4, 3), 此时应输出left
                
                <aside>
                💡 这才导致一直输出的是left！原来的写法有问题，结果对了是巧合！
                
                </aside>
                
3. ✅ [leetcode 34: 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/) [[讲解](https://programmercarl.com/0034.%E5%9C%A8%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E6%9F%A5%E6%89%BE%E5%85%83%E7%B4%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%92%8C%E6%9C%80%E5%90%8E%E4%B8%80%E4%B8%AA%E4%BD%8D%E7%BD%AE.html)]
    
    <aside>
    💡 要习惯设计test case（general，corner case）
    
    </aside>
    
    - initial idea:
        - 二分查找分别找出左右端点（2个while loop）
        - 通过把nums[mid] = target的情况并入“小于” / “大于”，让其中之一恰好错过左/右端点
        - 测试了普通，全target的情况
    - bugs:
        1. 忘记无target的test case：
            1. 在第一个while loop后判断nums[left or right] == target
        2. 忘记无target+target大于小于max/min的test case，数组寻址错误：
            1. 在bug1的判断上再套三个if else，保证数组取值合理.
    - 看解析后：
        1. 先找出left & right border，若没有target可以通过border直接判断
        2. 分情况：
            1. target在最左或最右，但没有
            2. target在中间但没有
            3. 有target
        3. if条件若有顺序可以从左往右写，例如先判断是否数组越界，再分析不越界情况，and连接。
        4. 题解里面最后根据left / right border的判断条件有点复杂，搜出来后如果没有target（case 1 or 2）则一定有：rightborder - leftborder = 1，不用单独判断是否越界了。若>1则一定存在target。想全test case的重要性！
4. ✅ [leetcode 69: x的平方根](https://leetcode.cn/problems/sqrtx/)
5. ✅ [leetcode 367: 完全平方数](https://leetcode.cn/problems/sqrtx/)

这两题都是easy，基本直接套二分查找。但是都有数学解法，之后应该学一下牛顿法的原理。

## 移除元素

### TL;DR

- 快&慢指针：目的→O(n^2)变O(n)
- 保序和不保序

### 经典例题

1. ✅ [leetcode 27: 移除元素](https://leetcode.cn/problems/remove-element/) [[讲解](https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html#_27-%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0)]
    - 练习了快慢指针和相向指针法
    - 需要注意：
        - 赋值而不是交换，因为不用管后面是什么
        - 注意要求的输出对应的是哪个指针，分别考虑几种testcase

> 为了赶赶进度，先只完成一题，之后有时间不上拓展题。
>