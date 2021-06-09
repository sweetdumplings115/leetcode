#题目描述
剑指 Offer 10- II. 青蛙跳台阶问题
一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。
答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。
用递归要超时
###示例 1：
输入：n = 2
###输出：2
示例 2：
输入：n = 7
###输出：21
###示例 3：
输入：n = 0
输出：1
##解法一：
假如青蛙跳到了第n(n >= 2)节台阶上，那么他只可能是从n - 1节台阶 和 n - 2节台阶上跳上去了，所以也就有了跟斐波那契数列差不多公式：
但是F(0) = F(1) = 1;
F(N) = F(N - 1) + (N - 2)，N >= 2
```java
class Solution {
    public int numWays(int n) {
        if(n < 2) return 1;
        long[] result = new long[n + 1];
        result[0] = 1;
        result[1] = 1;
        for(int i = 2; i <= n; i++){
            result[i] = result[i - 1] + result[i - 2];
            result[i] %= (Math.pow(10,9) +7);
        }
        return (int)result[n];
    }
}
```
##解法二：
```java
class Solution {
    public int numWays(int n) {
        int a = 1, b = 1, sum;
        for(int i = 0; i < n; i++){
            sum = (a + b) % 1000000007;
            a = b;
            b = sum;
        }
        return a;
    }
}
```
