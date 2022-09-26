给定一个正整数 n，生成一个包含 1 到 n^2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

示例:

```
输入: 3 
输出: [ [ 1, 2, 3 ], [ 8, 9, 4 ], [ 7, 6, 5 ] ]
```

![spiraln](spiraln.jpg)



> 这个题目于我而言是一个很熟悉的题，但是每次碰到它的时候，我总喜欢下意识避开它因为感觉自己绕不清楚，这次自己弄清原理后自己写便豁然开朗。

**首先应该明确，这个矩阵是如何生成的，从图中可以看出，它遵循着：**

* 首先从左到右
* 然后从上到下
* 然后从右到左
* 然后从下到上

因为涉及转圈，所以我们要明确每次for循环的区间，在这里我们可以遵循**左闭右开**的原则，可以保证4个for循环的结构类似。

>注意的点：
>
>* 要转多少圈？
>
>  可以由n % 2 得到，例如n = 3时，转一圈就可以。
>
>* 奇数圈和偶数圈需要加以区分吗？
>
>  需要的，如果是奇数圈的话，最中间的数需要单独填充。
>
>* 每转完一圈需要做什么处理？
>
>  x、y的起始位置分别加1，偏移大小也需要加1。



```cpp
class Solution{
public:
    vector<vector<int>> generateMatrix(int n) {
        //首先定义生成的数组
        vector<vector<int>> res(n, vector<int>(n,0));
        //定义起始位置
        int startX = 0, startY = 0;
        //定义偏移大小
        int offset = 1;    //偏移大小是变化的，因为我们总是取n为基准
        //定义圈数
        int loop = n / 2;
        //定义赋值的参数
        int count = 1;
        //循环条件 当loop为0时终止循环
        while(loop--) {
            //定义两个参数来移动
            int i = startX, j = startY;
            for (; j < n - offset; j++) {
                res[startX][j] = count++;  //若n = 3时，j会加到2然后停止。
            }
            for (; i < n - offset; i++) {
                res[i][j] = count++; //注意这里不能用startY，因为j已经移动了。
            }
            for (; j > startY; j--) {
                res[i][j] = count++;
            }
            for (; i > startX; i--) {
                res[i][j] = count++;
            }
            
            //转一圈结束了，对参数进行处理
            startX++;
            startY++;
            
            offset++;
        }
        if (n % 2 == 1) {
            res[n / 2] = n * n;
        }
        return res;
    }
};
```



