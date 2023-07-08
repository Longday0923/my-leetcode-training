# Day10 - 栈与队列 - 用栈实现队列, 用队列实现栈

## 1. ✅ leetcode ****232. 用栈实现队列「[讲解](https://programmercarl.com/0232.%E7%94%A8%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97.html)」**

- 已经做过再复习一遍：两个栈两次反向实现队列的正向
    - 如果outStack非空直接在outStack上操作
    - 否则需要先把整个inStack导入outStack

## 2. ✅ leetcode ****225. 用队列实现栈「[讲解](https://programmercarl.com/0225.%E7%94%A8%E9%98%9F%E5%88%97%E5%AE%9E%E7%8E%B0%E6%A0%88.html)」**

- 一开始模仿栈→队列的两次反序得到正序，发现不行
- 那么如何设计尽量少的多余空间？
    - 让队列循环起来即可
- peek的时候别忘最后再把第一个循环到队尾