给定一个含有 n 个正整数的数组和一个正整数 s ，找出该数组中满足其和 ≥ s 的长度最小的 连续子数组，并返回其长度。如果不存在符合条件的子数组，返回 0。

示例：

```
输入：s = 7, nums = [2,3,1,2,4,3] 
输出：2 
解释：子数组 [4,3] 是该条件下的长度最小的子数组。
```



**这题有几个关键点需要抓住：**

* 长度最小的连续子数组，既然是连续的，则可以考虑用滑动窗口解决。

>滑动窗口的左右又该如何控制呢？
>
>**可以设立快慢指针，快指针控制滑动窗口右边界，慢指针控制滑动窗口左边界。**
>
>for循环带着快指针遍历数组，当判断sum已经满足条件时，对滑动窗口的大小进行判断和处理



```C++
class Solution{
public:
    int minSubArrayLen(int s, vector<int>& nums) {
        int result = INT32_MAX;    // 给result赋值一个极大的数方便处理
        int sum = 0;
        int slow = 0;    //慢指针
        for (int fast = 0; fast < nums.size(); fast++) {
            sum += nums[fast];
            //注意判断窗口用的是while！！！
            while(sum >= s) {
                //当前窗口大小
                int subLength = fast - slow + 1;
                //判断它与result的大小
                result = result < subLength ? result : subLength;
                sum -= nums[slow++];    //这一步很关键，将左窗口逐渐缩小。
            }
        }
        return result == INT32_MAX ? 0 : result;
    }
};
```



