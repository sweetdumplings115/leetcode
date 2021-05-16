#题目描述
946.给定 pushed 和 popped 两个序列，每个序列中的 值都不重复，只有当它们可能是在最初空栈上进行的推入 push 和弹出 pop 操作序列的结果时，返回 true；否则，返回 false 。
###示例 1：
输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
###示例 2：

输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
输出：false
解释：1 不能在 2 之前弹出。
##解法
所有的元素一定是按顺序 push 进去的，重要的是怎么 pop 出来
将 pushed 队列中的每个数都 push 到栈中，同时检查这个数是不是 popped 序列中下一个要 pop 的值，如果是就把它 pop 出来。
最后，检查不是所有的该 pop 出来的值都是 pop 出来了。
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        int N = pushed.length;
        Stack<Integer> stack = new Stack();

        int j = 0;
        for (int x: pushed) {
            stack.push(x);
            while (!stack.isEmpty() && j < N && stack.peek() == popped[j]) {
                stack.pop();
                j++;
            }
        }

        return j == N;
    }
}

##解法自己（太烂）
import java.util.*;
import java.util.Map;
import java.util.HashMap;
public class validateStackSequences {
    public static void main(String[] args) {
        int pushed[]={1,2,3,4,5};
        int popped[]={4,3,5,1,2};

        int length=pushed.length;
        int i=0;
        int j=0;
        int n=-1,m=-1;
        HashMap <Integer,Integer> hash=new HashMap<Integer,Integer>();
        for(i=0;i<length;i++)
        {
            hash.put(pushed[i],i);
        }
        if(hash.isEmpty()){
           System.out.println("true");
        }
        if(hash.containsKey(popped[j])){//找到popped第一个在push位置
            n=hash.get(popped[j])-1;//向前走
            m=n+2;//向后
            hash.remove(popped[j]);
        }else{
            System.out.println("false");
        }
        while(j<length-1){
            j++;
            if(n==hash.get(popped[j]) && n>=0){//相邻
                    hash.remove(popped[j]);
                    n--;
            }else if(m==hash.get(popped[j]) && m<length){//相邻
                    hash.remove(popped[j]);
                    m++;
            }else if(m<hash.get(popped[j]) && m<length){//在后面
                n=hash.get(popped[j])-1;
                m=n+2;;
                hash.remove(popped[j]);
            }else if(n>hash.get(popped[j]) && n>=0 && hash.containsValue(n)){//在前面且中间有数
                Sytem.out.println("false");
                goto loop;
            }else if(n>hash.get(popped[j]) && n>=0  ){//在前面且中间没有数
                while(!hash.containsValue(n)){
                    n--;
                }
                j--;
            }

        }
        loop :
        if(hash.isEmpty()){
            System.out.println("true");
        }else{
            System.out.println("false");
        }
    }
}
