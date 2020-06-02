# 线型DP

## LeetCode410.Split Array Largest Sum  

Given an array which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays. Write an algorithm to minimize the largest sum among these m subarrays.  

```java
Input:nums = [7,2,5,10,8],m = 2  
Output:18
```
1.定义subproblem ``` DP[i][j]: 分割nums[0...i]为j个group ```.  
2.递归公式: ``` DP[i][j] = min{DP[k][j-1]+(nums[k+1]+nums[k+2]+...+nums[j])} 0<=k<j ```.  
3.边界条件: 建立```n x m```的array, 除了DP[0][0]=0, 其余位置等于 Integer.MAX_VALUE.  
4.伪代码  

```java
DP[i][j] -> Integer.MAX_VALUE
DP[0][0] = 0
for i <- 1 to n
  for j <- 1 to m
    for k <- 0 to i
      DP[i][j] = min(DP[i][j], DP[k][j-1]+(nums[k+1]+nums[k+2]+...+nums[j])) 
return DP[n][m]
```
