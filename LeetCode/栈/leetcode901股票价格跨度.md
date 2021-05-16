#题目描述
901. 股票价格跨度
###输入：
["StockSpanner","next","next","next","next","next","next","next"], [[],[100],[80],[60],[70],[60],[75],[85]]
输出：[null,1,1,1,2,1,4,6]
解释：
首先，初始化 S = StockSpanner()，然后：
S.next(100) 被调用并返回 1，
S.next(80) 被调用并返回 1，
S.next(60) 被调用并返回 1，
S.next(70) 被调用并返回 2，
S.next(60) 被调用并返回 1，
S.next(75) 被调用并返回 4，
S.next(85) 被调用并返回 6。


##解法
我们用单调栈维护一个单调递减的价格序列，并且对于每个价格，存储一个 weight 表示它离上一个价格之间（即最近的一个大于它的价格之间）的天数。如果是栈底的价格，则存储它本身对应的天数。例如 [11, 3, 9, 5, 6, 4, 7] 对应的单调栈为 (11, weight=1), (9, weight=2), (7, weight=4)。

当我们得到了新的一天的价格，例如 10，我们将所有栈中所有小于等于 10 的元素全部取出，将它们的 weight 进行累加，再加上 1 就得到了答案。在这之后，我们把 10 和它对应的 weight 放入栈中，得到 (11, weight=1), (10, weight=7)。
```class StockSpanner {
    Stack<Integer> prices, weights;

    public StockSpanner() {
        prices = new Stack();
        weights = new Stack();
    }

    public int next(int price) {
        int w = 1;
        while (!prices.isEmpty() && prices.peek() <= price) {
            prices.pop();
            w += weights.pop();
        }

        prices.push(price);
        weights.push(w);
        return w;
    }
}
```