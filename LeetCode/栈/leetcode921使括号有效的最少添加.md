#题目描述
921. 使括号有效的最少添加
给定一个由 '(' 和 ')' 括号组成的字符串 S，我们需要添加最少的括号（ '(' 或是 ')'，可以在任何位置），以使得到的括号字符串有效。
###示例 1：
输入："())"
输出：1
###示例 2：
输入："((("
输出：3
###示例 3：
输入："()"
输出：0
###示例 4：
输入："()))(("
输出：4
##解法
```package Daytest;
import java.util.*;
public class minAddToMakeValid {
    public static void main(String[] args){
        String s="";
        Scanner sc= new Scanner(System.in);
        s=sc.nextLine();
        System.out.println(matching(s));

    }

    public static int  matching(String s){//配对“（）”数量就减2
        int i=0;
        int num=s.length();
        Stack<Character> stack=new Stack<>();
        if(s.equals("")){
            return 0;
        }
        stack.push(s.charAt(i));
        for(i=1;i<s.length();i++){
            while(!stack.isEmpty() && stack.peek().equals('(')  && i<s.length() && s.charAt(i)==')'){
             i++;
             stack.pop();
             num-=2;
            }
            if(i<s.length()){
                stack.push(s.charAt(i));
            }

        }

        return num;
    }
}
```
##解法
保证左右括号数量的 平衡： 计算 '(' 出现的次数减去 ')' 出现的次数。如果值为 0，那就是平衡的，如果小于 0，就要在前面补上缺少的 '('。
计算 S 每个前缀子数组的 平衡度。如果值是负数（比如说，-1），那就得在前面加上一个 '('
```class Solution {
    public int minAddToMakeValid(String S) {
        int ans = 0, bal = 0;
        for (int i = 0; i < S.length(); ++i) {
            bal += S.charAt(i) == '(' ? 1 : -1;
            // It is guaranteed bal >= -1
            if (bal == -1) {
                ans++;
                bal++;
            }
        }

        return ans + bal;//计算 '(' 出现的次数减去 ')' 出现的次数和出现“）”要在前面加上一个 '('的次数
    }
}
```


