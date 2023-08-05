# Day38 - 动态规划 - 斐波那契数, 爬楼梯, 使用最小花费爬楼梯

## 1.✅509. 斐波那契数「[讲解](https://programmercarl.com/0509.%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0.html#%E6%80%9D%E8%B7%AF)」

## 2.✅70. 爬楼梯「[讲解](https://programmercarl.com/0070.%E7%88%AC%E6%A5%BC%E6%A2%AF.html)」

斐波那契数，我的方法是直接把a设为第一个，最后返回a即可。那么需要注意迭代器的开始和结束。

## 3.✅746. 使用最小花费爬楼梯「[讲解](https://programmercarl.com/0746.%E4%BD%BF%E7%94%A8%E6%9C%80%E5%B0%8F%E8%8A%B1%E8%B4%B9%E7%88%AC%E6%A5%BC%E6%A2%AF.html)」

直接在cost数组上原地修改。

注意直接返回cost[-1]的话相当于必须要走最后一个台阶，其实不一定。所以可以在cost后面append一个0，然后再返回cost[-1]