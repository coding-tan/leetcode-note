# 454. 四数相加 II

[代码随想录文档链接](https://www.programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html#%E6%80%9D%E8%B7%AF)

[力扣题目链接](https://leetcode.cn/problems/4sum-ii/)

给你四个整数数组 nums1、nums2、nums3 和 nums4 ，数组长度都是 n ，请你计算有多少个元组 (i, j, k, l) 能满足：
0 <= i, j, k, l < n
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0
```text
示例 1：
输入：nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
输出：2
解释：
两个元组如下：
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0

示例 2：
输入：nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
输出：1
 
```

## 1. 哈希法（unordered_map）

本题解题步骤：
- 首先定义 一个unordered_map，key放a和b两数之和，value 放a和b两数之和出现的次数。
- 遍历大A和大B数组，统计两个数组元素之和，和出现的次数，放到map中。
- 定义int变量count，用来统计 a+b+c+d = 0 出现的次数。
- 在遍历大C和大D数组，找到如果 0-(c+d) 在map中出现过的话，就用count把map中key对应的value也就是出现次数统计出来。
- 最后返回统计值 count 就可以了
```cpp
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int, int> map; // key: a+b的值，value：a+b数值出现的次数
        // 遍历数组nums1和nums2，统计两个数组元素之和，和出现的次数，填入到map中
        for(int a : nums1 ){
            for(int b : nums2){
                map[a+b]++;
            }
        }
        int count = 0; // 统计a+b+c+d = 0 出现的次数
        // 遍历数组nums3和nums4, 如果找到0-(c+d) 在map中出现的话，就把map中key对应的value也就是出现次数统计出来。
        for(int c : nums3){
            for(int d : nums4){
                if(map.find(0-(c+d)) != map.end()){
                    count += map[0-(c+d)];
                }
            }
        }
        return count;
    }
};
```