#### 解题步骤
这又是一道可以用[Stack](http://www.xingxingpark.com/search/label/Stack)来解决的问题。

1.  建立降序栈`stk`,存`temperatures`数组对应的 index
2.	 建立返回数组`rets`并且初始化为0
3.  遍历`temperatures`数组：
	- 每一个元素`temp`和`stk`的栈顶元素对应值比较，如果`temp`较大，说明遇到了 warmer temperature，所以在`rets`中更新栈顶元素对应的值，并且 pop 栈顶元素
	- 重复上述过程，直到`stk`为空或者`temp`比栈顶值小，将当前`index` 进栈

#### 实例演算


#### 示例代码

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        int n = temperatures.size();
        // 注意需要初始化为0
        vector<int> rets(n, 0);
        stack<int> stk;
        for (int i = 0; i < n; ++i) {
            while (!stk.empty() && temperatures[i] > temperatures[stk.top()]) {
                rets[stk.top()] = i - stk.top();
                stk.pop();
            }
            // 注意push的是index，不是值
            stk.push(i);
        }
        return rets;
    }
};
```
#### 复杂度分析
因为每个字符`push`和`pop`都是最多一次，所以：

- 时间复杂度：`O(n)`
- 空间复杂度：`O(n)`

#### 总结归纳：
运用[Stack](http://www.xingxingpark.com/search/label/Stack)的题目很多，这类问题的做法是遍历输入数组，当前元素与栈顶元素比较，如果当前元素更优（不同题目条件不同，比如本题对应当前元素较大）则pop栈顶元素，直到栈顶元素更优为止，而后插入当前元素。

类似的题目还有：
[[LeetCode 316] Remove Duplicate Letters 移除重复字母](http://www.xingxingpark.com/2018/03/leetcode-remove-duplicate-letters.html)

最近会总结更多这类题目更新在[Stack Tag](http://www.xingxingpark.com/search/label/Stack)中，尽请期待，吃香蕉去了：）