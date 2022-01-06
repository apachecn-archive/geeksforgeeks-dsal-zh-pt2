# 将给定 a 转换为 b 的最小按位运算。

> 原文:[https://www . geesforgeks . org/minimum-bitwise-operations-to-convert-given-a-to-b/](https://www.geeksforgeeks.org/minimum-bitwise-operations-to-convert-given-a-into-b/)

给定两个正整数 a 和 b，你必须通过对 a 的二进制形式应用三个运算中的任何一个来将 a 变成 b。你可以选择 ai 和 aj(任何两位，其中 I！=j ),然后执行如下操作:

*   与运算为:温度= ai & aj，ai =温度& ai，aj =温度& aj
*   OR 运算为:temp = ai | aj，ai = temp | ai，aj = temp | aj
*   异或运算为:temp = ai ^ aj，ai = temp ^ ai，aj = temp ^ aj

其中& =按位 AND，| =按位 OR 和^ =按位 XOR。
找出 a 到 b 转换所需的最小操作。另外，如果 a 到 b 的转换不可能，则打印-1。

示例:

```
Input : a = 12 (1100), b = 10 (1010)
Output : 1
Explanation : select a2 and a3 and perform XOR 

Input : a = 15 (1111), b = 10 (1010)
Output : -1
Explanation : Conversion from a to b is not possible

```

**说明:**首先我们来了解一下这三个操作的工作原理。

1.  **AND operation** as : temp = ai & aj, ai = temp & ai, aj = temp & aj

    如果 ai 或 aj 中的任何一个为 0，则两者都为 0，否则对 ai 和 aj 没有影响。

2.  **OR operation** as : temp = ai | aj, ai = temp | ai, aj = temp | aj

    如果 ai 或 aj 中的任何一个为 1，则两者都为 1，否则对 ai 和 aj 没有影响。

3.  **XOR operation** as : temp = ai ^ aj, ai = temp ^ ai, aj = temp ^ aj

    简单地交换 ai 和 aj 的值。

基于操作工作的一些结论:

1.  如果 a 的所有位都是 1 或 0，那么我们就不能改变 a 的值。
2.  如果 a 等于 b，则不需要操作。
3.  Let n be number of indices i, where ai = 0 and bi = 1.
    Let m be number of indices i, where ai = 1 and bi = 0.

    让我们考虑 n 个元素，其中 ai = 0，bi = 1。我们必须把这些 0 都变成 1。请注意，这至少需要 n 次操作。
    对于所有的 m 个元素都类似，其中 ai = 1，bi = 0。我们必须把这些 1 都变成 0。请注意，这至少需要 m 次操作。

    设 res = max(n，m)。我们可以在 res 运算中使 a 和 b 相等，如下所示。

    让 n >= m。在 A 中取 m ^ 1 和 n ^ 0，并应用异或运算将 0 和 1 交换。之后，您将剩下总共 n-m 个零元素来更改为 1。你可以用单个 1 取这些 0，然后进行“或”运算。
    设 m > = n，取 A 中的 m ^ 1 和 n ^ 0，应用异或运算，将 0 和 1 交换，之后你将剩下 m-n 个元素的总和变为 0。你可以用单个零取其中的每一个，然后应用或运算。

```
// Cpp program to find min operation to convert a to b
#include <bits/stdc++.h>
using namespace std;

// function to return min operation
int minOp(bitset<32> a1, bitset<32> b1)
{
    // if a1 == b1 return 0
    if (a1 == b1)
        return 0;

    // if all bits of a = 0
    if (a1 == 0)
        return -1;

    // if all bits of a =1
    // first convert a1 to int and then cal a1 & a1+1
    if (((int)a1.to_ulong() & ((int)a1.to_ulong() + 1)) 
                                               == 0)
        return -1;

    // convert a and b to binary string
    string a = a1.to_string();
    string b = b1.to_string();

    // check where ai and bi are different
    // and count n where ai = 1 and m where ai = 0
    int n = 0, m = 0;
    for (int i = 0; i < b.size(); i++) {
        if (b[i] != a[i]) {
            if (a[i] == '1')
                n++;
            else
                m++;
        }
    }

    // return result
    return max(n, m);
}

// driver program
int main()
{
    bitset<32> a = 14, b = 1;
    cout << minOp(a, b);
    return 0;
}
```

输出:

```
3

```

本文由**[Shivam Pradhan(anuj _ charm)](http://www.facebook.com/ma5ter6it)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。