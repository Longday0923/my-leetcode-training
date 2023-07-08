# Day6 - 哈希表 - 有效的字母异位词,

## 1. ✅ leetcode ****242: 有效的字母异位词 [[讲解](https://programmercarl.com/0242.%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)]**

- Initial Idea:
    - hashmap, s+ t-最后看是否都等于零
- 看讲解后：
    - 可以直接建立对应26个字母的数组，不用维护动态的hashmap
    - 可以用数组的时候就不用字典
    - defaultdict(int)可以直接+=
    - Counter(s)可以直接计算

## 2. ✅ leetcode ****349: 两个数组的交集 [[讲解](https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html)]**

- Initial Idea:
    - set(nums1), if n in nums2 and in nums1, add to set. return list(set)
- 看讲解后：
    - python内置set的用法：
        - .add()
        - .remove()抛出Error，.discard()不报错
        - 交集：&, 并集：|，差集 A - B = A\B，对称差集 A^B.

## 3. ✅ leetcode ****202: 快乐数 [[讲解](https://leetcode.cn/problems/happy-number/solution/shi-yong-kuai-man-zhi-zhen-si-xiang-zhao-chu-xun-h/)]**

- Initial Idea:
    - set检测循环
    - list对象unhashable
        - “”.join(sorted(list(str(n))))这样能包括数字顺序不一样的
    - 别忘记更新n
- 看讲解后：
    - 动态大小的set确实容易出问题，抛开hashmap的练习，应该用快慢指针检测循环
    - 小bug:
        - slow = func(n)写顺手了，要写成slow！
        - slow和fast初始化为n，slow==fast的判定条件要写在while loop的最后！

## 4. ✅ leetcode 1: 两数之和 [[讲解](https://programmercarl.com/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.html#_1-%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C)]

- 一开始确实只想到了O(n^2)的解法
- 看讲解后：
    - 为什么想到用hash：因为是一分为二，知道其中一半查另一半是否出现过 → 时间复杂度降至 O(n)。
    - map: 需要返回的是索引。
    - 小bugs：变量/对象名定义有误需要修改时，认真检查所有使用过的地方。