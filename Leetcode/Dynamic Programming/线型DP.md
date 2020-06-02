# 线型DP

## LeetCode410.Split Array Largest Sum  

Given an array which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays. Write an algorithm to minimize the largest sum among these m subarrays.  

```java
Input:nums = [7,2,5,10,8],m = 2  
Output:18
```
1.定义subproblem-```java DP[i][j]: 分割nums[0...i]为j个group ```.
