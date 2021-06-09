#题目描述
找出所有相加之和为 n 的 k 个数的组合。组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。
说明：
所有数字都是正整数。
解集不能包含重复的组合。 
###示例 1:
输入: k = 3, n = 7
输出: [[1,2,4]]
###示例 2:
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
##我的解法：//	1 ms	35.9 MB
```java
public class text {
    List<List<Integer>> ans =new LinkedList<>();
    List<Integer> t=new LinkedList<>();
    boolean[] uesd=new boolean[10];
    public  List<List<Integer>> combinationSum3(int k, int n) {
        dsf(k,n);
        return ans;
    }
    public  void dsf(int k,int n){
        if (k==0){
            if (n==0){
                ans.add(new LinkedList<>(t));
                return;
            }
            return;
        }


        for(int i=1;i<10;i++){
            if(i>n){
               return;
            }
            if(!uesd[i]){
                if(t.size()>0 && i<t.get(t.size()-1)){//顺序要依次增加 比较要加入的i和t的末尾数字大小
                    continue;
                }
                t.add(i);
                uesd[i]=true;
                dsf(k-1,n-i);
                uesd[i]=false;
                t.remove(t.size()-1);
            }

        }
    }
        public static void main(String[] args) {
          /*  HashMap<String,Integer> hashMap= new HashMap<>();
           hashMap.put("123",12);*/
            int n=11;//和
            int k=3;//个数
            text text=new text();
            System.out.println(text.combinationSum3(k,n));
        }
    }
```
##解法一：
二进制（子集）枚举//2 ms	35.9 MB
```java
class Solution {
    List<Integer> temp = new ArrayList<Integer>();
    List<List<Integer>> ans = new ArrayList<List<Integer>>();

    public List<List<Integer>> combinationSum3(int k, int n) {
        for (int mask = 0; mask < (1 << 9); ++mask) {//1左移9是2^9,00000001->1000000000,即原序列中有 99 个数，每个数都有两种状态，「被选择///到子集中」和「不被选择到子集中」，所以状态的总数为 2^9
            if (check(mask, k, n)) {
                ans.add(new ArrayList<Integer>(temp));
            }
        }
        return ans;
    }

    public boolean check(int mask, int k, int n) {// n为 和, k 为个数
        for (int i = 0; i < 9; ++i) {
            if (((1 << i) & mask) != 0) {//表示在mark状态中,是否被选中
                temp.add(i + 1);
            }
        }
        if (temp.size() != k) {
            return false;
        }
        int sum = 0;
        for (int num : temp) {
            sum += num;
        }
        return sum == n;
    }
}
```
##解法二：//	1 ms	36.4 MB	Java
```java
class Solution {
    List<Integer> temp = new ArrayList<Integer>();
    List<List<Integer>> ans = new ArrayList<List<Integer>>();

    public List<List<Integer>> combinationSum3(int k, int n) {
        dfs(1, 9, k, n);
        return ans;
    }

    public void dfs(int cur, int n, int k, int sum) {
        if (temp.size() + (n - cur + 1) < k || temp.size() > k) {
            return;
        }
        if (temp.size() == k) {
            int tempSum = 0;
            for (int num : temp) {
                tempSum += num;
            }
            if (tempSum == sum) {
                ans.add(new ArrayList<Integer>(temp));
                return;
            }
        }
        temp.add(cur);
        dfs(cur + 1, n, k, sum);
        temp.remove(temp.size() - 1);
        dfs(cur + 1, n, k, sum);
    }
}
```
