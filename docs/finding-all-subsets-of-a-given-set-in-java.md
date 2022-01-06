# 在 Java 中查找给定集合的所有子集

> 原文:[https://www . geesforgeks . org/find-Java 中给定集合的所有子集/](https://www.geeksforgeeks.org/finding-all-subsets-of-a-given-set-in-java/)

**问题:**求给定集合的所有子集。

```
Input: 
S = {a, b, c, d}
Output:
{}, {a} , {b}, {c}, {d}, {a,b}, {a,c},
{a,d}, {b,c}, {b,d}, {c,d}, {a,b,c}, 
{a,b,d}, {a,c,d}, {b,c,d}, {a,b,c,d}
```

任何给定集合的子集总数等于 2^(集合中元素的数量)。如果我们仔细注意，它只不过是从 0 到 15 的二进制数，如下所示:

<figure class="table">

| 0000
 | {}
 |
| 0001
 | {a}
 |
| 0010
 | {b}
 |
| 0011
 | {a，b}
 |
| 0100
 | {c}
 |
| 0101
 | {a，c}
 |
| 0110
 | {b，c}
 |
| 0111
 | {a，b，c}
 |
| 1000
 | {d}
 |
| 1001
 | {a，d}
 |
| 1010
 | {b，d}
 |
| 1011
 | {a，b，d}
 |
| 1100
 | {c，d}
 |
| 1101
 | {a、c、d}
 |
| 1110
 | {b，c，d}
 |
| 1111
 | {a、b、c、d}
 |

从右开始，第 I 个位置的 1 表示集合中的第 I 个元素存在，而 0 表示该元素不存在。因此，我们要做的只是生成从 0 到 2^n–1 的二进制数，其中 n 是集合的长度或集合中元素的数量。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to print all subsets of a set
import java.io.IOException;

class Main
{
    // Print all subsets of given set[]
    static void printSubsets(char set[])
    {
        int n = set.length;

        // Run a loop for printing all 2^n
        // subsets one by one
        for (int i = 0; i < (1<<n); i++)
        {
            System.out.print("{ ");

            // Print current subset
            for (int j = 0; j < n; j++)

                // (1<<j) is a number with jth bit 1
                // so when we 'and' them with the
                // subset number we get which numbers
                // are present in the subset and which
                // are not
                if ((i & (1 << j)) > 0)
                    System.out.print(set[j] + " ");

            System.out.println("}");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        char set[] = {'a', 'b', 'c'};
        printSubsets(set);
    }
}
```

输出:

```
{ }
{ a }
{ b }
{ a b }
{ c }
{ a c }
{ b c }
{ a b c }
```

时间复杂度:O(n * (2^n))，因为外环为 O(2^n 运行，内环为 O(n)运行。

**相关帖子:**
[在 C/C++](https://www.geeksforgeeks.org/power-set/)
中查找一个集合的所有子集本文由 **Nikhil Tekwani 供稿。**如果你喜欢 GeeksforGeeks 并想投稿，你也可以写一篇文章，把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息

</figure>