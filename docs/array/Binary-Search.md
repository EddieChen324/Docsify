给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

示例 1:

```text
输入: nums = [-1,0,3,5,9,12], target = 9     
输出: 4       
解释: 9 出现在 nums 中并且下标为 4     
```

示例 2:

```text
输入: nums = [-1,0,3,5,9,12], target = 2     
输出: -1        
解释: 2 不存在 nums 中因此返回 -1       
```



**使用二分法的前提条件**

* 有序数组
* 数组中无重复元素（否则查找的元素下标不唯一）



**要点**

> *坚持循环不变量的原则*
>
> *区间就是不变量*



**二分法**

* 左闭右闭
  * while (left <= right) 要使用 <= ，因为left == right是有意义的，所以使用 <=
  * if (nums[middle] > target) right 要赋值为 middle - 1，因为当前这个nums[middle]一定不是target，那么接下来要查找的左区间结束下标位置就是 middle - 1

* 左闭右开
  * while (left < right)，这里使用 < ,因为left == right在区间[left, right)是没有意义的
  * if (nums[middle] > target) right 更新为 middle，因为当前nums[middle]不等于target，去左区间继续寻找，而寻找区间是左闭右开区间，所以right更新为middle，即：下一个查询区间不会去比较nums[middle]



```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        while (left <= right) {
            int middle = left + (right - left) / 2;//防止溢出
            if (nums[middle] < target) {
                left = middle + 1;
            }
            else if (nums[middle] > target) {
                right = middle - 1;
            }
            else return middle;
        }
        return -1;
    }
}
```











 





​	



