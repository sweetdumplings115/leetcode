#题目描述
20.  有效的括号
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。
有效字符串需满足：
左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
###示例示例 1：
输入：s = "()"
输出：true
示例 2：
###示例示例 2：
输入：s = "()[]{}"
输出：true
示例 3：
###示例示例 3：
输入：s = "(]"
输出：false
示例 4：
###示例示例 4：
输入：s = "([)]"
输出：false
示例 5：
###示例示例 5：
输入：s = "{[]}"
输出：true
##解法
用栈stack
```java
public class isValid {
    public static void main(String[] args) {
        Stack<Character>  stack= new Stack<>();
        String s=new Scanner(System.in).nextLine();
        int length =s.length();
        boolean n=false;
        if(length%2==1){//长度为奇数，直接返回 False
            System.out.println("不可以");
        }

      for(int i=0;i<length;i++){
          char a=s.charAt(i);
          if(!stack.isEmpty()){
             char b=stack.peek();// peek( ) 查看堆栈顶部的对象，但不从堆栈中移除它
             if(b=='(' && a==')' || b=='[' && a==']' || b=='{' && a=='}'){
                 stack.pop();//左右括号匹配，压出栈顶的左括号
                 continue;
             }
          }
          stack.push(a);//不匹配压入
      }

        if(stack.isEmpty()){
            System.out.println("可以");
        }
    }
}
```
##解法
```java
class Solution {
    public boolean isValid(String s) {
        int n = s.length();
        if (n % 2 == 1) {
            return false;
        }

        Map<Character, Character> pairs = new HashMap<Character, Character>() {{
            put(')', '(');
            put(']', '[');
            put('}', '{');
        }};
        Deque<Character> stack = new LinkedList<Character>();//Java堆栈Stack类已经过时，Java官方推荐使用Deque替代Stack//使用。Deque堆栈操///作方法：push()、pop()、peek()。
        
        for (int i = 0; i < n; i++) {
            char ch = s.charAt(i);
            if (pairs.containsKey(ch)) {
                if (stack.isEmpty() || stack.peek() != pairs.get(ch)) {
                    return false;
                }
                stack.pop();
            } else {
                stack.push(ch);
            }
        }
        return stack.isEmpty();
    }
}
```