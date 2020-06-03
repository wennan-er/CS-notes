# 区间DP

## LeetCode410.分割数组的最大值(hard)  

给定一个非负整数数组和一个整数 m，你需要将这个数组分成 m 个非空的连续子数组。设计一个算法使得这 m 个子数组各自和的最大值最小.  

```java
输入:nums = [7,2,5,10,8],m = 2  
输出:18
```

1.定义subproblem ``` DP[i][j]: 分割nums[0...i]为j个group ```.  
2.递归公式: ``` DP[i][j] = min{max(DP[k][j-1],(nums[k+1]+nums[k+2]+...+nums[j]))} 0<=k<j ```.  
3.边界条件: 建立```n x m```的array, 除了```DP[0][0] = 0```, 其余位置等于 ```Integer.MAX_VALUE```.    
```DP[0][0] = 0```是因为把一个长度为0的array拆分成0个group和为0.  
```DP[1][0]...DP[n][0]= INI_MAX```:是因为把一个长度不为0的array拆分成0个group和为INT_MAX.  
```DP[0][1]...DP[0][m]= INI_MAX```:理论上来说```DP[0][1]...DP[0][m]= 0```但是在如下的testcase中:会有overflow的情况发生.  

```java
Input:nums = [1,2147483647],m = 2  
Output:0
Expected Output:2147483647
```
4.伪代码  

```java
DP[i][j] -> Integer.MAX_VALUE
DP[0][0] = 0
for i <- 1 to n
  for j <- 1 to m
    for k <- 0 to i-1
      DP[i][j] = min(DP[i][j], max(DP[k][j-1],(nums[k+1]+nums[k+2]+...+nums[j]))) 
return DP[n][m]
```

## LeetCode188.买卖股票的最佳时机(hard)

给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。设计一个算法来计算你所能获取的最大利润。你最多可以完成 k 笔交易。
注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）  

```java
输入: [3,2,6,5,0,3], k = 2
输出: 7
解释: 在第 2 天 (股票价格 = 2) 的时候买入，在第 3 天 (股票价格 = 6) 的时候卖出, 这笔交易所能获得利润 = 6-2 = 4 。
     随后，在第 5 天 (股票价格 = 0) 的时候买入，在第 6 天 (股票价格 = 3) 的时候卖出, 这笔交易所能获得利润 = 3-0 = 3 。
```
1.定义subproblem ``` DP[t][d]: 在k个transanction之下t天的收益 ```.  
2.递归公式:由于这道题目和上一题不一样，上一题对每个区间求和即可，这一题是在每一个区间内产生一笔交易，值为该区间某一天的股票价减去另一天的股票价。``` DP[t][d] =  DP[k][j-1]+max_profit[]```  


![DP\[t\]\[d\]= \begin{cases} DP\[t\]\[d-1\] \\  price\[d\] + max{DP\[t-1\]\[k\]-price\[k\]}(0 \leq x \le d) \end{cases}](https://render.githubusercontent.com/render/math?math=DP%5Bt%5D%5Bd%5D%3D%20%5Cbegin%7Bcases%7D%20DP%5Bt%5D%5Bd-1%5D%20%5C%5C%20%20price%5Bd%5D%20%2B%20max%7BDP%5Bt-1%5D%5Bk%5D-price%5Bk%5D%7D(0%20%5Cleq%20x%20%5Cle%20d)%20%5Cend%7Bcases%7D)


DP[t][d]= \begin{cases} DP[t][d-1] \\ 
price[d] + max \left\{ DP[t-1][k]-price[k]\right\}(0 \leq x \le d) \end{cases}
