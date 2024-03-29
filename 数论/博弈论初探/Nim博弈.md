### nim博弈

**定义**：有 $n$ 堆物品，每堆物品的个数为 $a_i$，双方轮流从中取物品，每次只能从一堆物品中**取部分或全部**物品，最少取一件，取到最后一件物品的人获胜(没有东西可以取的人输)。

**结论**：把每堆物品数全部异或起来，如果结果 $0$，那么先手必败，否则先手必胜。

**先手必胜**：当前状态下有办法必胜，将当前状态转为必败态。

**先手必败**：当前状态下必定会输。

**两个关键点**

* **必胜态**一定**可以转换**为一个必输态。
* **必输态**不可能转换为另一个必输态，**只能转换为必胜态**。

**必输态**：$0\wedge 0\wedge  ... 0=0$。当前是先手必输态，根据上面的两条，该状态由必胜态转换而来。
当 $a_1\wedge a_2\wedge ... \wedge a_n = x!= 0$ 的时候，一定可以通过拿取操作将剩下的元素异或值变为 $0$（变为下个人必输的状态），因为异或是  **同零异一**，即零和一的个数都是偶数个，现在异或结果不为 $0$，说明多出来奇数个 $0$ 和 $1$，只需要将多出来的拿走即可。
所以 $a_1\wedge a_2\wedge ... \wedge a_n = x!= 0$ 时，当前操作的人必胜。

```c++
for (int i = 0; i < n; i ++) {
    int a;
    cin >> a;
    x = x ^ a;
}
if (x != 0) {}
else {}
```

### 变体一：台阶

现在，有一个 $n$ 级台阶的楼梯，每级台阶上都有若干个石子，其中第 $i$ 级台阶上有 $a_i$ 个石子。两位玩家轮流操作，每次操作可以从任意一级台阶上拿若干个石子放到下一级台阶中（不能不拿）。已经拿到地面上的石子不能再拿，最后无法进行操作的人视为失败。

**分析**：对于偶数级台阶上的，先手将其放到奇数台阶上，后手接着将其放到偶数台阶上（最终放到地上），则状态不变，即偶数台阶对最终结果无影响，只需要考虑奇数台阶的异或结果。

### 变体二：集合