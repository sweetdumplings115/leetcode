#题目描述
###1190. 反转每对括号间的子串
给出一个字符串 s（仅含有小写英文字母和括号）。请你按照从括号内到外的顺序，逐层反转每对匹配括号中的字符串，并返回最终的结果。注意，您的结果中 不应 包含任何括号。
###示例 1：
输入：s = "(abcd)"
输出："dcba"
###示例 2：
输入：s = "(u(love)i)"
输出："iloveu"
###示例 3：
输入：s = "(ed(et(oc))el)"
输出："leetcode"
###示例 4：
输入：s = "a(bcdefghijkl(mno)p)q"
输出："apmnolkjihgfedcbq"

##解法一：
暴力法
```
使用栈去匹配括号,
public String reverseParentheses(String s) {
    Stack<Integer> stack = new Stack<>();
    StringBuilder res = new StringBuilder();
    char[] chs = s.toCharArray();

    for (int i = 0; i < chs.length; i++) {
        if (chs[i] == '(') {
            stack.push(i);
        } else if (chs[i] == ')') {
            reverse(chs, stack.pop() + 1, i - 1);
        }
    }
    for (char ch : chs) {
        if (ch != '(' && ch != ')') {//去掉'('和')'
            res.append(ch);
        }
    }
    return res.toString();
}

private void reverse(char[] chs, int start, int end) {
    while (end > start) {//反转括号内字符串
        char temp = chs[end];
        chs[end] = chs[start];
        chs[start] = temp;
        start++;
        end--;
    }
}
```
##解法二：

```
    public String reverseParentheses(String s) {
        int n = s.length();
        Stack<Integer> stack = new Stack<>();
        int[] pair = new int[n];//存放'('和)'所在位置

        //先去找匹配的括号
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else if (s.charAt(i) == ')') {
                int j = stack.pop();
                pair[i] = j;//存放匹配的另一半括号的位置
                pair[j] = i;
            }
        }

        StringBuilder res = new StringBuilder();
        // i是当前位置 | d是方向,1就是向右穿，-1向左
        for (int i = 0, d = 1; i < n; i+=d) {//在括号之间由外到内，左右之间移动
            if (s.charAt(i) == '(' || s.charAt(i) == ')') {
                // 如果碰到括号，那么去他对应的括号，并且将方向置反
                i = pair[i];
                d = -d;
            } else {
                res.append(s.charAt(i));
            }
        }
        return res.toString();
    }
```

