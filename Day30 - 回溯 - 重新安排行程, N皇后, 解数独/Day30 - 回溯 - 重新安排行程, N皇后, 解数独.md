# Day30 - 回溯 - 重新安排行程, N皇后, 解数独

> 三道hard人都麻了
> 

## 1.✅****332.重新安排行程「[讲解](https://programmercarl.com/0332.%E9%87%8D%E6%96%B0%E5%AE%89%E6%8E%92%E8%A1%8C%E7%A8%8B.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)」**

- 第一道完全凭自己做出来的hard，值得纪念。
- 我的初始思路是建立一个树形结构，用dict去存一个所有始发地到其目的地的n叉树。然后遍历+回溯。
- 一开始遇到的bugs：
    - 如何解决搜到的是结果中最小的字典序？
        - 用OrderedDict，key排序；每个key对应的destination list，也排序。这样搜出来就应该是一个最小序的。
    - 如何解决死循环？
        - 这是一开始没想明白的问题，本质是两个事情没想明白：
            - 每张票只能用一次
            - 同层内如何剪枝
        - 其实每张票只能用一次，就代表从同一个始发地到其目的地只能用一次。这个一次性是深度上的（也就是出入递归的）一次性，而非层内横向的一次性。同层剪枝用set，深度剪枝用used数组。
            - 我一开始使用的是deque去做popleft … pushright，回溯里没有这种操作，即使是pop&push也要将其复原到原位。可以pop(i)&insert但这样可想而知复杂度较高。所以使用used数组更好。
            - 后来还尝试只pop不push，也是回溯中不可能有的操作。记住入出递归，一定会还原原本的信息结构（树结构）
    - 查到结果直接返回，所以backtracking要加返回值判断。
    - 一开始没注意必须从JFK开始，其实这样更简单。
    - for k, v in dic.items(): v = sorted(v)不会改变v，因为这时候k,v做了复制。所以要写dic[k] = sorted(v)
- 看讲解后：思想基本一致。还有一种只对tickets遍历来回溯的办法。大体上思路一致。建立hashmap是更清晰的写法。
- 没必要用OrderedDict，因为从JFK开始，keys就不用排序了，只要对每个key对应的list排序即可。

## 2.✅****51.N皇后「[讲解](https://programmercarl.com/0051.N%E7%9A%87%E5%90%8E.html)」**

- 回溯部分的思想很简单：递归深度=行数，横向循环宽度=行数
- 主要在于如何高效判别某个位置是否合法，以及如何将合法性判别也进行回溯。
- Initial Idea:
    - 设一个used matrix = N * N，每加一个，就将这个点以及相应列和对角线上的点都设为True
    - 回溯时再将这些点都设为False
    - bug在于，后面点回溯时会将前面点的列和对角线改为False
    - 我的解法是把True False改为+-1，这样只有==0的点可以放。
    - 空间复杂度n^2，时间也会大大增加，因为每次都要迭代扫过所有的列和对角线。时间复杂度在原本的基础上*n。原本的时间复杂度应该是n!
- 看讲解后：
    - 主要是判断validness这步的复杂度。
    - leetcode时间最快范例：学习并自己写一遍
    
    ```python
    class Solution:
        def solveNQueens(self, n: int) -> List[List[str]]:
            ans = []
            col = [0] * n
            m = 2 * n - 1
            on_path = [False] * n
            pie = [False] * m
            na = [False] * m
    
            def dfs(r):
                if r == n:
                    ans.append(["." * c + "Q" + "." * (n-c-1) for c in col])
                    return
    
                for c, on in enumerate(on_path):
                    if not on and not pie[r+c] and not na[r-c+n-1]:
                        col[r] = c
                        on_path[c] = pie[r+c] = na[r-c+n-1] = True
                        dfs(r+1)
                        on_path[c] = pie[r+c] = na[r-c+n-1] = False
    
            dfs(0)
            return ans
    ```
    
    主要差别在于，这一方法合理使用了每列&每对角线只能有一个。所以就可以只维护三个1*m的True/False数组，并且每次可以通过计算直接对数组进行更改，所以validness判断变为O(1)操作。
    

## 3.✅****37. 解数独「[讲解](https://programmercarl.com/0037.%E8%A7%A3%E6%95%B0%E7%8B%AC.html#%E6%80%9D%E8%B7%AF)」**

- bug：
    - 因为变量较多，一开始写的r, c;后来又写i,j导致忘记修改。还是尽量按顺序一气呵成写代码，就需要先想好代码结构再动笔。
- Initial Idea:
    - 递归深度是遍历每个位置，同层循环是每个位置可以取1～9，用used数组记录[num][行/列/3*3]是否使用，要比每个都迭代去检查快。
    - 回溯函数传参为位置i,j这样能保证当前这个位置填好后直接去看下一个位置。在递归内计算nextR, nextC，传给下一层。
- 看讲解：
    - [leetcode讲解](https://leetcode.cn/problems/sudoku-solver/solution/jie-shu-du-by-leetcode-solution/)：可使用位运算和优化遍历。看麻了。先过完基础知识再看。