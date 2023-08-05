# Day51 - 动态规划 - 最长公共子序列, 不相交的线, 最大子序和

## 1.✅**1143.最长公共子序列「[讲解](https://programmercarl.com/1035.%E4%B8%8D%E7%9B%B8%E4%BA%A4%E7%9A%84%E7%BA%BF.html#%E6%80%9D%E8%B7%AF)」**

- 2维dp，代表截止s1[i], s2[j]的最长公共子序列。
- 递推公式：dp[i][j] = dp[i - 1][j - 1] + 1 if s1[i] == s2[j] else max(dp[i - 1][j], dp[i][j - 1])
- 初始化，多一行0
- 遍历顺序：两个字符串均从前至后。

## 2.✅**1035.不相交的线「[讲解](https://programmercarl.com/1035.%E4%B8%8D%E7%9B%B8%E4%BA%A4%E7%9A%84%E7%BA%BF.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- 原来和上题一模一样……
- 总是list out of index，注意i,j到底是nums中的ij还是dp数组中的ij，以及初始化的时候外层不要忘了+1.

## 3.✅**53. 最大子序和「[讲解](https://programmercarl.com/0053.%E6%9C%80%E5%A4%A7%E5%AD%90%E5%BA%8F%E5%92%8C%EF%BC%88%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%89.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- 贪心法：
    - cnt, res = 0, -inf
    - cnt += num
        - if cnt > res: res = cnt
        - if cnt < 0: cnt = 0
    
    若加到某个数导致和为负，就不再连续了，因为前面一个负的和加到后面的数字上，肯定会导致整体的和更小。
    
    也有可能一直是负数，所以res需要每一步都更新。
    
- 动态规划：
    - 这题我直接想贪心了，动规中规中矩：
        
        ```python
        dp = [nums[0]] + [0] * (len(nums) - 1)
        for i in range(1, len(nums)):
        		dp[i] = max(nums[i], dp[i - 1] + nums[i])
        return max(dp)
        ```