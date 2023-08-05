# Day52 - 动态规划 - 判断子序列, 不同的子序列, 两个字符串的删除操作

## 1.✅**392.判断子序列「[讲解](https://programmercarl.com/0392.%E5%88%A4%E6%96%AD%E5%AD%90%E5%BA%8F%E5%88%97.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- 一左一右，在t串中找匹配。若s串所有都匹配上，则True
- 看范例后：确实O(n)，但是写复杂了。可以直接单向遍历，快慢指针：
    - 快指针：t指针每次固定移动一步
    - 慢指针：当和t指针相同时移动一步
    - 最后检查慢指针是否全部走完即可。
- 看讲解：练了一下dp的写法。O(mn)

## 2.✅**115.不同的子序列「[讲解](https://programmercarl.com/0115.%E4%B8%8D%E5%90%8C%E7%9A%84%E5%AD%90%E5%BA%8F%E5%88%97.html#%E6%80%9D%E8%B7%AF)」**

- 这题因为看到了前面说的“减”的情况，所以看到target串中存在连续的字母，尝试从前一个的结果中减1。其实只是用例子在凑数，遇到不同例子立刻崩盘
- 应当从实际意义和逻辑上去思考如果由前一步的dp值导出这一步的。
- 标准思路：
    - dp[i][j]的含义：以s[i - 1]和t[j - 1]作为结尾的不同子序列的数量。
    - 递推公式：
        - if s[i - 1] == t[j - 1]:
            - dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j]
            
            <aside>
            💡 这两项非常关键，实际含义理解：如果发现s和t两个字符相同，这时子串数量应该等于：这两个字符匹配的不同子串数 + target的这个字符和source中前面的字符匹配的不同子串数。即target的当前最后字符是否和source的当前字符匹配。
            
            </aside>
            
        - if s[i - 1] ≠ t[j - 1]: dp[i][j] = dp[i - 1][j] 理解：target当前字符和source前面字符匹配的不同子串数。
    - 初始化：空与空匹配=1，target>0 与 source=0匹配 = 0.
    - 迭代方向：可以使用滚动数组降维，所以需要内层循环从后向前遍历。

## 3.✅**583. 两个字符串的删除操作「[讲解](https://programmercarl.com/0583.%E4%B8%A4%E4%B8%AA%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E5%88%A0%E9%99%A4%E6%93%8D%E4%BD%9C.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- len1 + len2 - 2 * len(lcs) 直接基于最长公共子序列进行创新。
- 注意初始化：dp[0][0] = 0。别想当然。

贴一个神奇的LCS的写法：有空研究

```python
def LCS(s1: str, s2: str) -> int:
    """请保证: len(s1) <= len(s2)"""
    m = len(s2)
    mapper = DefaultDict[str, List[int]](list)
    for i in reversed(range(m)):
        mapper[s2[i]].append(i)
    nums = []
    for c in s1:
        if c in mapper:
            nums.extend(mapper[c])

    return LIS(nums)
```