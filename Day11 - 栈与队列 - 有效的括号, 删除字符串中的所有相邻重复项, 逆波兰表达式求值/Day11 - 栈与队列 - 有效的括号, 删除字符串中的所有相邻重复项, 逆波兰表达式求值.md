# Day11 - 栈与队列 - 有效的括号, 删除字符串中的所有相邻重复项, 逆波兰表达式求值

## 1. ✅ leetcode ****20. 有效的括号「[讲解](https://programmercarl.com/0020.%E6%9C%89%E6%95%88%E7%9A%84%E6%8B%AC%E5%8F%B7.html#%E9%A2%98%E5%A4%96%E8%AF%9D)」**

- 做过，一遍过，复习一下：
    - 用栈实现：检测（左括号的）后进先出
    - 每次进栈一个字符时：
        - 右括号：
            - 若空栈：return false
            - 若栈顶非对应左括号： return false
            - 栈顶对应括号：stack.pop()
        - 左括号：压栈
    - 最后 return not stack：空的是对的

## 2. ✅ leetcode 1047. 删除字符串中的所有相邻重复项「[讲解](https://programmercarl.com/1047.%E5%88%A0%E9%99%A4%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%B8%AD%E7%9A%84%E6%89%80%E6%9C%89%E7%9B%B8%E9%82%BB%E9%87%8D%E5%A4%8D%E9%A1%B9.html)」

- Initial Idea:
    - 看了提示想出来的，否则都忘了用栈了……
    - stack非常合适做这种配对删除问题，尤其是删除，因为他总能记住删除后的上一个。
- 看讲解：
    - （一开始其实想到的）双指针模拟栈操作，练一下

## 3. ✅ leetcode ****150. 逆波兰表达式求值「[讲解](https://programmercarl.com/0150.%E9%80%86%E6%B3%A2%E5%85%B0%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%B1%82%E5%80%BC.html)」**

- Initial Idea:
    - 一开始光看示例还没反应过来什么意思，看到baike的后缀表达式就明白了：遇到符号pop两个算完再push回去
- 看讲解
    - eval算得慢而且最好不用，所以可用dict包lambda
    - int(x/y)不论正负都是向0约的
    - 这里是字符数组所以好算了，如果是字符串，第一更难，第二是否会有二义性？

<aside>
💡 Python中and和or有短路逻辑：
and左侧为False则直接输出false，不计算右侧
or左侧为True则直接输出True，不计算右侧
所以while 和 if可以把越界等条件列在前边，更细致的条件写在后面

</aside>