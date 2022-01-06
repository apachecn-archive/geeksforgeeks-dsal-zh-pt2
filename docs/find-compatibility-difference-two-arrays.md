# 找出两个数组的兼容性差异

> 原文:[https://www . geesforgeks . org/find-兼容性-差异-两个数组/](https://www.geeksforgeeks.org/find-compatibility-difference-two-arrays/)

假设有两个朋友，现在他们想测试他们的友谊，他们有多兼容。给定从 1 …n 开始编号的数字 n，要求他们对这些数字进行排序。任务是找出它们之间的兼容性差异。兼容性差异是他们给出的同一部电影的相对排名中的误匹配数量。

**示例:**

```
Input : a1[] = {3, 1, 2, 4, 5} 
        a2[] = {3, 2, 4, 1, 5}
Output : 2
Explanation : Compatibility difference is two
because first ranks movie 1 before 2 and 4 but
other ranks it after.

Input : a1[] = {5, 3, 1, 2, 4} 
        a2[] = {3, 1, 2, 4, 5}
Output : 5
Total difference is four due to mis-match in
position of 5
```

沃尔玛实验室询问

这个想法是遍历两个数组。
1)如果当前元素相同，则不执行任何操作。
2)查找 a2[]中 a1[i]的下一个位置。让这个位置为 j .一个一个移动 a2[j]到 a2[i](类似于[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)的冒泡步骤)

下面是以上步骤的实现。

## C++

```
// C++ program to count of misplacements
#include <bits/stdc++.h>
using namespace std;
int findDifference(int a1[], int a2[], int n)
{
    int res = 0;

    for (int i = 0; i < n; i++) {

        // If elements at current position
        // are not same
        if (a1[i] != a2[i]) {

            // Find position of a1[i] in a2[]
            int j = i + 1;
            while (a1[i] != a2[j])
                j++;

            // Insert the element a2[j] at
            // a2[i] by moving all intermediate
            // elements one position ahead.
            while (j != i) {
                swap(a2[j], a2[j - 1]);
                j--;
                res++;
            }
        }
    }
    return res;
}

// Driver code
int main()
{
    int a1[] = { 3, 1, 2, 4, 5 };
    int a2[] = { 3, 2, 4, 1, 5 };
    int n = sizeof(a1)/sizeof(a1[0]);
    cout << findDifference(a1, a2, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of misplacements
public class Compatability_difference {

    static int findDifference(int a1[], int a2[], int n)
    {
        int res = 0;

        for (int i = 0; i < n; i++) {

            // If elements at current position
            // are not same
            if (a1[i] != a2[i]) {

                // Find position of a1[i] in a2[]
                int j = i + 1;
                while (a1[i] != a2[j])
                    j++;

                // Insert the element a2[j] at
                // a2[i] by moving all intermediate
                // elements one position ahead.
                while (j != i) {

                    //swap
                    int temp = a2[j - 1];
                    a2[j - 1] = a2[j];
                    a2[j] = temp;
                    j--;
                    res++;
                }
            }
        }
        return res;
    }

    // Driver code
    public static void main(String args[])
    {
        int a1[] = { 3, 1, 2, 4, 5 };
        int a2[] = { 3, 2, 4, 1, 5 };
        int n = a1.length;

        System.out.println(findDifference(a1, a2, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to count misplacements

def findDifference(a1, a2, n):

    res = 0

    for i in range(0, n):

        # If elements at current
        # position are not same
        if a1[i] != a2[i]:

            # Find position of a1[i] in a2[]
            j = i + 1
            while (a1[i] != a2[j]):
                j += 1
                if i >= n or j >= n:
                    break

            # Insert the element a2[j] at
            # a2[i] by moving all intermediate
            # elements one position ahead.
            while (j != i):
                a2[j],a2[j-1] = a2[j-1],a2[j]
                res += 1
                j -= 1
                if i >= n or j >= n:
                    break

    return res

# Driver code
a1 = [ 3, 1, 2, 4, 5 ]
a2 = [ 3, 2, 4, 1, 5 ]
n = len(a1)
print(findDifference(a1, a2, n))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to count of misplacements
using System;

public class Compatability_difference
{
    static int findDifference(int []a1, int []a2, int n)
    {
        int res = 0;

        for (int i = 0; i < n; i++) {

            // If elements at current
            // position are not same
            if (a1[i] != a2[i]) {

                // Find position of a1[i] in a2[]
                int j = i + 1;
                while (a1[i] != a2[j])
                    j++;

                // Insert the element a2[j] at
                // a2[i] by moving all intermediate
                // elements one position ahead.
                while (j != i) {

                    //swap
                    int temp = a2[j - 1];
                    a2[j - 1] = a2[j];
                    a2[j] = temp;
                    j--;
                    res++;
                }
            }
        }
        return res;
    }

    // Driver code
    public static void Main()
    {
        int []a1 = {3, 1, 2, 4, 5};
        int []a2 = {3, 2, 4, 1, 5};
        int n = a1.Length;

        // Function calling
        Console.WriteLine(findDifference(a1, a2, n));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript program to count of misplacements
function findDifference(a1, a2, n)
{
    let res = 0;

    for(let i = 0; i < n; i++)
    {

        // If elements at current position
        // are not same
        if (a1[i] != a2[i])
        {

            // Find position of a1[i] in a2[]
            let j = i + 1;
            while (a1[i] != a2[j])
                j++;

            // Insert the element a2[j] at
            // a2[i] by moving all intermediate
            // elements one position ahead.
            while (j != i)
            {

                // Swap
                let temp = a2[j - 1];
                a2[j - 1] = a2[j];
                a2[j] = temp;
                j--;
                res++;
            }
        }
    }
    return res;
}

// Driver code
let a1 = [ 3, 1, 2, 4, 5 ];
let a2 = [ 3, 2, 4, 1, 5 ];
let n = a1.length;

document.write(findDifference(a1, a2, n));

// This code is contributed by sravan kumar

</script>
```

输出:

```
2
```

本文由**拉克什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。