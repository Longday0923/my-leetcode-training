# Day28 - 回溯 - 复原IP地址, 子集, 子集II

## 1.✅****93.复原IP地址「[讲解](https://programmercarl.com/0093.%E5%A4%8D%E5%8E%9FIP%E5%9C%B0%E5%9D%80.html#%E5%9B%9E%E6%BA%AF%E4%B8%89%E9%83%A8%E6%9B%B2)」**

- 像回文组合一样的分割问题，递归不同长度的子串
- 本题特殊处理的是每个子串的validness，我的设计是
    - int(t) < 255 break
    - backtracking
    - if s[startId] == “0” break
- int(”0012”) = 12 所以没法排除前导0的情况，而单独的0又是合规的。所以先执行一次，再检查首位为零就跳出。

## 2.✅****78.子集「[讲解](https://programmercarl.com/0078.%E5%AD%90%E9%9B%86.html#%E5%9B%9E%E6%BA%AF%E4%B8%89%E9%83%A8%E6%9B%B2)」**

- 直接用dp解了
- 一开始直接写回溯一直出错，发现习惯性地按照之前的分割去写了。这里相当于从集合中取元素，所以每次加进来只能有一个。下一层递归为了不重复，必须从这之后的元素中取。
- 区分分割和组合的本层循环对象：
    - 组合：for _ in list(靠后的元素)
    - 分割：for _ in 以startId为首的子串

## 3.✅****90.子集II「[讲解](https://programmercarl.com/0090.%E5%AD%90%E9%9B%86II.html#%E6%80%9D%E8%B7%AF)」**

- 子集问题+循环内剪枝，注意不是i>0是i>startId
- 试试dp能不能做:
    - nums排序
    - dp[i]代表到nums[i]为止的所有子集
    - 判定若i>0 and num[i] == nums[i - 1]，记录nums[i - 1]新增子集preLen；nums[i]只在dp[-preLen:]上增加nums[i]因为前面的都被nums[i-1]加过了。
    - 其他正常对dp[i-1]的所有子集append最新元素，加入到总子集集合中。
    - 注意preLen的更新：
        - 正常情况的更新就是当前元素加上前的len(dp)
        - 连续重复元素，不用更新，因为数量等于前一步的preLen。