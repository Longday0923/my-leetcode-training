# Day7 - 哈希表 - 四数相加II, 赎金信, 三数之和, 四数之和, 总结

## 1. ✅ leetcode ****454: 四数相加II 「[讲解](https://programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)」**

- 一开始没想到怎么写，模仿前一天的两数之和只能化简到O(n^3)?
- 大概看了一下讲解：
    - 把四个数分成2+2复杂度从O(n^4)降到O(n^2)
    - 自己继续实现：
        - 先把1&2， 3&4各自的两两和算出来，然后和的数组再模仿两数之和，区别是value存的是和出现过的次数
        - 次数统计用Counter
            - 这里查了一下Counter和defaultdict的适用范围：
                1. Counter适合已经存在一个可迭代的对象（list / string）然后直接Counter(obj)
                2. defaultdict适合从无到有逐渐生成
    - 再练一下defaultdict的用法：
        - defaultdict(int) = defaultdict(lambda: 0) # 都是默认0值的意思
        - 明显比counter的写法快一截，因为list初始化遍历一遍，counter计数又遍历一遍
    - 学到了dict.get(key[, value])的写法，若没有key则返回value

## 2. ✅ leetcode 383: 赎金信 「[讲解](https://programmercarl.com/0383.%E8%B5%8E%E9%87%91%E4%BF%A1.html#%E6%80%9D%E8%B7%AF)」

- Initial Idea
    - 看到提示和有效字母异位词相似，用Counter解
    - 要求note包含于magazine：
        - 先判断.keys()，再判断相减后的value是否都<0
- 看解析：
    - 写麻烦了：
        - Counter A-B直接是A比B多的pair，如果对应计数B>A，直接从A中去掉。
        - 所以一句话：return Counter(Note) - Counter(magazine)
        - 测试发现上面的写法快一些，应该先判断keys就能return的话就省去了继续算完其他Counter的时间
    - 还有一种string.count()的写法
        - 要对set(list(Note))中所有的字母遍历，Note.count(c) ≤ Magazine.count(c) 然后 all([])
        - all, any的用法：可以直接学一遍built-in-function，也不强求记住，碰到时候要想起来用。
        
        [Python 内置函数 | 菜鸟教程](https://www.runoob.com/python/python-built-in-functions.html)
        

## 3. ✅ leetcode ****15: 三数之和 「[讲解](https://leetcode.cn/problems/3sum/solution/3sumpai-xu-shuang-zhi-zhen-yi-dong-by-jyd/)」**

- Initial Idea:
    - 还是模仿上面用set去存两两之和，但很难写去重。需存两两之和每一个组合，但和第三个组合后还要set去重
- 看讲解后：
    - 粗略浏览后先自己实现一下，主要问题卡在k, i, j跳过重复
        - i, j跳过重复需要保证每次第一个不跳过（i在k+1不能跳，j在len-2不能跳）
        - k跳过需要保证不跳过0（k-1越界）
        - 我自己的实现方法是都写在while i<j的循环里，合并sum < 0和跳过i的情况，j类似。
    - 仔细看了K神的解法：
        - 跳过但不能跳过第一个：可以先执行一个，然后用while去跳过后面的
        - 用while来跳过i, j, k，外面套sum的判定。这样代码会多一点，但是看着逻辑更清楚（sum只需比较大于小于等于0即可）

## 4. ✅ leetcode ****18: 四数之和 「[讲解](https://programmercarl.com/0018.%E5%9B%9B%E6%95%B0%E4%B9%8B%E5%92%8C.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)」**

- Initial Idea
- bugs:
    - 如果每一次循环都left+=1 or right-=1，会导致少掉很多情况
    - 剪枝：单纯判断nums[left]>target是不行的，可能target<0.
        - 可以写成target ≥ 0 and nums[left] > target
    - 一开始写的循环是left, i, j, right且right in range(left + 3, len(nums)) 这样会跳过一些情况
        - 可以改为right in range(len(nums) - 1, left + 2, -1)
- 看解析后：
    - left, right, i, j也可以，不会导致确实情况
    - 可以在left和right都定了之后再进行一次剪枝：nums[left] + nums[right] > target and target ≥ 0
    - s>tar 和 s<tar的情况中，不手动去重更快一些。猜测因为直接算下一次的sum，即使重复也不会计入res，同时算sum能比寻址num[i-1]更快一些。不过无伤大雅。

## 总结

- 双指针法：
    - 数组需要排序
    - 时间O(n^2) → O(n)，空间替代hash变为O(1)
    - 去重和剪枝：
        - 情况要考虑全面，例如四数之和的target<0的情况，不能直接照搬。可以多设几组数试一试。
        - 去重和剪枝用一个while loop实现可读性更强
    - 循环直接尝试用快慢指针判断
- Counter：直接减会把kv pair减掉，可以利用这个性质
- defaultdict可以多用，自带初始化的dict，增强代码可读性。