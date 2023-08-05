# Day48 - 动态规划 - 买卖股票的最佳时机（I, II, III）

## 1.✅**121. 买卖股票的最佳时机「[讲解](https://programmercarl.com/0121.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BA.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- 一开始和之前有一道投资总和混淆，一直想着通过收集正利去算，还要每天分买入、持有、卖出考虑。后来发现，只需要记录每一天之前的min，以及每天的maxprofit，即可。
- 看讲解：
    - 这个写法是贪心！找到左边最小和右边最大！
    - 动态规划确实是要去考虑是否“持有”的问题，但是并不用分那么多种情况，每天只要考虑是否持有即可。
    - 递推公式：dp[i] = Hold: dp[i - 1][0], Sell: max(dp[i - 1][1], dp[i - 1][0] + val[i])
    - 初始化：dp[0] = -val[0], 0

## 2.✅**122.买卖股票的最佳时机II「[讲解](https://programmercarl.com/0122.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAII%EF%BC%88%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%89.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- 还是分每天是否持有，持有时相比上题变化一下即可。

## 3.✅**123.买卖股票的最佳时机III「[讲解](https://programmercarl.com/0123.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAIII.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- 自己没想出来……如何考虑（最多）两次买入卖出？
- 因为有两次可能的买入卖出，所以要设置四个状态呢，分别是第一次的买入卖出和第二次的买入卖出，因为第二次的买入卖出依赖第一次的操作。
- hold1, sell1, hold2, sell2 = -prices[0], 0, -prices[0], 0可以理解为都是第一天的重复操作
- 递推公式：
    - hold1 = max(hold1, -prices[i])理解为第一次持有要么是报纸之前的，要么就是能之前都没有买入，当天刚买入的。
    - sell1 = max(sell1, hold1 + prices[i])正常操作
    - hold2 = max(hold2, sell1 - prices[i])这里是最关键的一步，必须基于sell1而产生的hold2
    - sell2 = max(sell2, hold2 + prices[i])正常操作
- 最后返回sell2
- 检查一下hold2的合理性，因为hold2在一开始初始化和hold1相同，为什么不会导致两次交易有重叠？
    - 假设hold1, prices[i - 1] = hold1 + 1, prices[i] = hold1 + 2，所以sell1: 1 → 2
    - hold2 = -hold1（两天都是），sell2 = 1→2。
    - 例子看出，可能重叠的时候，其实sell2会直接等于sell1，相当于只进行了一次交易。