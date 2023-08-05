# Day49 - 动态规划 - 买卖股票的最佳时机IV, 最佳买卖股票时机含冷冻期, 买卖股票的最佳时机含手续费

## 1.✅**188.买卖股票的最佳时机IV「[讲解](https://programmercarl.com/0188.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAIV.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- III的进化版，其实就是dp数组加长了一些，变成简单题了。

## 2.✅**309.最佳买卖股票时机含冷冻期「[讲解](https://programmercarl.com/0309.%E6%9C%80%E4%BD%B3%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E6%97%B6%E6%9C%BA%E5%90%AB%E5%86%B7%E5%86%BB%E6%9C%9F.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- 推一下递推公式，发现相比II只有hold的公式有变化，需要hold[i] = max(hold[i - 1], sell[i - 2] - prices[i])。所以需要多存一个preSell来记录隔一个的前面是什么。
- 举例子看初始化，preSell初始化为0即可，其他照搬。
- 题解是给每天多设一个状态，若当前是冷静期。我的方法还是保持每天只有是否持有两个状态。如果要买入的话，需要跳过前一天，基于大前天去判断，通过数组可取值的范围来限制冷冻期。

## 3.✅**714.买卖股票的最佳时机含手续费「[讲解](https://programmercarl.com/0714.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BA%E5%90%AB%E6%89%8B%E7%BB%AD%E8%B4%B9%EF%BC%88%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%89.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)」**

- 加入了手续费之后，核心难点在于初始化和递推公式中手续费含义的统一。
    - 假设认为手续费在买入时候就需要交
    - 初始化：hold, sell = -prices[0] - fee, 0注意这里sell的情况，是当前最大的sell，此时最大的sell是不买，所以为0
    - 递推公式：
        - hold = max(hold, sell - prices[i] - fee)
        - sell = max(sell, hold + prices[i])买入时交手续费。
        - 也可以换为卖出时交手续费。核心点在于sell和hold记录的是max，所以初始化不要sell = -fee