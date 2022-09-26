给你一个按非递减顺序排序的整数数组 nums，返回每个数字的平方组成的新数组，要求也按非递减顺序排序。

```
示例 1： 
输入：nums = [-4,-1,0,3,10] 
输出：[0,1,9,16,100] 
解释：平方后，数组变为 [16,1,0,9,100]，排序后，数组变为 [0,1,9,16,100]
```

```
示例 2： 
输入：nums = [-7,-3,2,3,11] 
输出：[4,9,9,49,121]
```





**做这一道题，只需要明确一点就好了：就是平方后的新数组的较大值在哪里出现？**

> 观察后可以发现，新数组靠右边的值只会在原数组的左右两头产生。比如原数组的最小值或最大值才可能是新数组的最大值。

**因此会想到双指针，分别指向开头和结尾，两个指针所指的数进行比较再看移动哪根指针。**



```cpp
//时间复杂度：O(n)
//空间复杂度：O(1)
class Solution{
public:
    vector<int> sortedSquares(vector<int>& nums) {
        //首先定义新数组
        vector<int> result(nums.size(), 0);
        //定义前后指针
        int left = 0, right = nums.size() - 1;
        int k = nums.size() - 1;
        for (; left <= right;) {
            if (nums[left] * nums[left] < nums[right] * nums[right]) {
                result[k--] = nums[right] * nums[right];
                right--;    //取right的值就向左移动一位
            }
            else {
                result[k--] = nums[left] * nums[left];
            }
        }
        return result;
    }
};
```



