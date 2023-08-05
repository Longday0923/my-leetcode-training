# Day50 - 动态规划 - 最长递增子序列, 最长连续递增序列, 最长重复子数组

## 1.✅**300.最长递增子序列「[讲解](https://programmercarl.com/0300.%E6%9C%80%E9%95%BF%E4%B8%8A%E5%8D%87%E5%AD%90%E5%BA%8F%E5%88%97.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- 正常写是O(n^2)的时间复杂度，每加入一个新的，就基于过去所有的结果重新更新。
- 题目要求降到O(nlogn)时间复杂度，看大神题解：「讲解：[简介版](https://leetcode.cn/problems/longest-increasing-subsequence/solution/zui-chang-shang-sheng-zi-xu-lie-dong-tai-gui-hua-e/)，[K神详细版](https://leetcode.cn/problems/longest-increasing-subsequence/solution/zui-chang-shang-sheng-zi-xu-lie-dong-tai-gui-hua-2/)」
    - 肯定要遍历所有的数组元素，那么需要每个元素查询时间为logn，logn在数组中是排序后二分查找的时间复杂度，思考如何能二分查找。
    - 一开始我自己想用小顶堆来维护已经遍历过的元素和对应的子序列长度。后来发现因为需要一个个pop→比较→push，其实还是n^2的时间。
    - 大神解法：还是动态规划，但是设计不同的状态空间：
        - dp[k]代表当前子序列长度为k+1最小的末尾元素。
        - 演示：input: [7,8,9,1,2,3,4]
        - dp的变化：
            - [7]
            - [7,8]
            - [7,8,9]
            - [1,8,9]
            - [1,2,9]
            - [1,2,3,]
            - [1,2,3,4]
        - 这样设计保证了dp数组的长度是当前最长子序列的长度，同时每个位置记录最小的末尾元素，保证后面大但不够大的元素可以继续接上来。·

## 2.✅**674. 最长连续递增序列「[讲解](https://programmercarl.com/0674.%E6%9C%80%E9%95%BF%E8%BF%9E%E7%BB%AD%E9%80%92%E5%A2%9E%E5%BA%8F%E5%88%97.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- 连续了就简单了
- 我直接使用的dp数组，初始化为全1.
- 看题解：可以降维至O(1)，再设一个res存max。实测比上面的慢，res = max(res, cnt)的写法在python中会慢一些。

## 3.✅**718. 最长重复子数组「[讲解](https://programmercarl.com/0718.%E6%9C%80%E9%95%BF%E9%87%8D%E5%A4%8D%E5%AD%90%E6%95%B0%E7%BB%84.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

三种方法层层递进，hash + 二分查找看懵了。

- 方法一：独立完成的朴素dp：
    - dp[i][j]表示以nums1[i]和nums2[j]结尾的最长重复子数组长度。
    - 递推公式：dp[i][j] = dp[i - 1][j - 1] + 1 if nums1[i] == num2[j] else 0
    - 初始化：要在nums1[0]和nums2[0]前多设一行一列，所以是(m+1) * (n+1)的全零数组。
    - 遍历顺序：长短无所谓。
- 方法二：滑动窗口+最长连续相同序列
    - 滑动窗口指遍历所有nums1和nums2的对齐情况，在每种对齐情况下只考虑相同脚标的相同子数组，相当于是上一题的简化版。
    - 滑动窗口要想好怎么设，保证有剪枝但不要遗漏。剪枝是通过先比较较长的重叠区间。若已有重叠发现，后面更短的重叠区间就无需再比较了。
- 方法三：哈希设计 + 二分查找
    - Rabin-Karp 算法可以用来对序列进行哈希。
    - 某一序列S的hash值为：base通常为一较小素数，mod为1较大素数。
        
        $$
        hash(S) = \Sigma{i}_{0}^{|S| - 1} base^i * S[i]  \%  mod
        $$
        
    - 若hash值相等，则认为两序列相同。
    - 给定一个固定序列长度，可以遍历nums1和nums2中所有此长度的子序列，若有hash值相同的则说明，存在大于等于这一序列长度的相同子序列。
    - 利用二分查找，找到最大的序列长度。
    - 注意二分查找时res的记录：
        
        ```python
        if checkLen(mid): # if True 当前长度有重复子序列
        		res = mid
        		left = mid + 1
        else: right = mid - 1
        ```