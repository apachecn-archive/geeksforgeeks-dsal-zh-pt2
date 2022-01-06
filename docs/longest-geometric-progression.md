# 最长几何级数

> 原文:[https://www . geesforgeks . org/最长几何级数/](https://www.geeksforgeeks.org/longest-geometric-progression/)

给定一组数字，找出其中 **L** 最长 **G** 最长 **P** 的长度( **LLGP** )。GP 的公比必须是整数。
示例:

```
set[] = {5, 7, 10, 15, 20, 29}
output = 3
The longest geometric progression is {5, 10, 20}

set[] = {3, 9, 27, 81}
output = 4
```

这个问题类似于[最长等差数列问题](https://www.geeksforgeeks.org/length-of-the-longest-arithmatic-progression-in-a-sorted-array/)。我们可以用动态规划来解决这个问题。
我们首先对给定的集合进行排序。我们使用一个辅助表 L[n][n]来存储子问题的结果。该表中的一个条目 L[i][j]存储集[i]和集[j]为 GP 和 j 的前两个元素的 LLGP>I .该表从右下到左上填充。为了填充表格，首先固定 j(GP 中的第二个元素)。搜索 I 和 k 寻找一个固定的 j，如果 I 和 k 被发现使得 I，j，k 形成一个 GP，那么 L[i][j]的值被设置为 L[j][k] + 1。请注意，当循环从右列遍历到左列时，L[j][k]的值必须已经被填充。
下面是动态规划算法的实现。

## C++

```
// C++ program to find length
// of the longest geometric
// progression in a given set
#include <iostream>
#include <algorithm>
using namespace std;

// Returns length of the
// longest GP subset of set[]
int lenOfLongestGP(int set[], int n)
{
    // Base cases
    if (n < 2)
        return n;
    if (n == 2)
        return (set[1] % set[0] == 0) ? 2 : 1;

    // Let us sort the set first
    sort(set, set+n);

    // An entry L[i][j] in this
    // table stores LLGP with
    // set[i] and set[j] as first
    // two elements of GP
    // and j > i.
    int L[n][n];

    // Initialize result (A single element
    // is always a GP)
    int llgp = 1;

    // Initialize values of last column
    for (int i = 0; i < n - 1; ++i) {
        if (set[n-1] % set[i] == 0)
        {
            L[i][n-1] = 2;
            if (2 > llgp)
              llgp = 2;
        }
        else
        {
            L[i][n-1] = 1;
        }
    }
    L[n-1][n-1] = 1;

    // Consider every element as
    // second element of GP
    for (int j = n - 2; j >= 1; --j)
    {
        // Search for i and k for j
        int i = j - 1, k = j+1;
        while (i>=0 && k <= n-1)
        {

            // Two cases when i, j and k don't form
            // a GP.
            if (set[i] * set[k] < set[j]*set[j])
            {
                ++k;
            }
            else if (set[i] * set[k] > set[j]*set[j])
            {
                if (set[j] % set[i] == 0)
                {
                    L[i][j] = 2;
                }
                else
                {
                    L[i][j] = 1;
                }
                --i;
            }

            // i, j and k form GP, LLGP with i and j as
            // first two elements is equal to LLGP with
            // j and k as first two elements plus 1.
            // L[j][k] must have been filled before as
            // we run the loop from right side
            else
            {
                if (set[j] % set[i] == 0)
                {
                    L[i][j] = L[j][k] + 1;

                    // Update overall LLGP
                    if (L[i][j] > llgp)
                        llgp = L[i][j];
                } else {
                  L[i][j] = 1;
                }

                // Change i and k to fill more L[i][j]
                // values for current j
                --i;
                ++k;
            }
        }

        // If the loop was stopped due to k becoming
        // more than n-1, set the remaining entries
        // in column j as 1 or 2 based on divisibility
        // of set[j] by set[i]
        while (i >= 0)
        {
            if (set[j] % set[i] == 0)
            {
                L[i][j] = 2;
                if (2 > llgp)
                    llgp = 2;
            }
            else
                L[i][j] = 1;
            --i;
        }
    }

    // Return result
    return llgp;
}

// Driver code
int main()
{
    int set1[] = {1, 3, 9, 27, 81, 243};
    int n1 = sizeof(set1)/sizeof(set1[0]);
    cout << lenOfLongestGP(set1, n1) << "\n";

    int set2[] = {1, 3, 4, 9, 7, 27};
    int n2 = sizeof(set2)/sizeof(set2[0]);
    cout << lenOfLongestGP(set2, n2) << "\n";

    int set3[] = {2, 3, 5, 7, 11, 13};
    int n3 = sizeof(set3)/sizeof(set3[0]);
    cout << lenOfLongestGP(set3, n3) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length
// of the longest geometric
// progression in a given set
import java.util.*;

class GFG {

    // Returns length of the longest GP subset of set[]
    static int lenOfLongestGP(int set[], int n)
    {
        // Base cases
        if (n < 2) {
            return n;
        }
        if (n == 2) {
            return (set[1] % set[0] == 0 ? 2 : 1);
        }

        // Let us sort the set first
        Arrays.sort(set);

        // An entry L[i][j] in this table
        // stores LLGP with set[i] and set[j]
        // as first two elements of GP
        // and j > i.
        int L[][] = new int[n][n];

        // Initialize result (A single
        // element is always a GP)
        int llgp = 1;

        // Initialize values of last column
        for (int i = 0; i < n - 1; ++i) {
            if (set[n - 1] % set[i] == 0) {
                L[i][n - 1] = 2;
                if (2 > llgp)
                    llgp = 2;
            }
            else {
                L[i][n - 1] = 1;
            }
        }
        L[n - 1][n - 1] = 1;

        // Consider every element as second element of GP
        for (int j = n - 2; j >= 1; --j) {
            // Search for i and k for j
            int i = j - 1, k = j + 1;
            while (i >= 0 && k <= n - 1) {
                // Two cases when i, j and k
                // don't form a GP.
                if (set[i] * set[k] < set[j] * set[j]) {
                    ++k;
                }
                else if (set[i] * set[k]
                         > set[j] * set[j]) {
                    if (set[j] % set[i] == 0) {
                        L[i][j] = 2;
                        if (2 > llgp)
                            llgp = 2;
                    }
                    else {
                        L[i][j] = 1;
                    }
                    --i;
                }

                // i, j and k form GP, LLGP with i and j as
                // first two elements is equal to LLGP with
                // j and k as first two elements plus 1.
                // L[j][k] must have been filled before as
                // we run the loop from right side
                else {
                    if (set[j] % set[i] == 0) {
                        L[i][j] = L[j][k] + 1;

                        // Update overall LLGP
                        if (L[i][j] > llgp) {
                            llgp = L[i][j];
                        }
                    }
                    else {
                        L[i][j] = 1;
                    }

                    // Change i and k to fill more L[i][j]
                    // values for current j
                    --i;
                    ++k;
                }
            }

            // If the loop was stopped due to k becoming
            // more than n-1, set the remaining entries
            // in column j as 1 or 2 based on divisibility
            // of set[j] by set[i]
            while (i >= 0) {
                if (set[j] % set[i] == 0) {
                    L[i][j] = 2;
                    if (2 > llgp)
                        llgp = 2;
                }
                else {
                    L[i][j] = 1;
                }
                --i;
            }
        }

        // Return result
        return llgp;
    }

    // Driver code
    public static void main(String[] args)
    {
        int set1[] = { 1, 3, 9, 27, 81, 243 };
        int n1 = set1.length;
        System.out.print(lenOfLongestGP(set1, n1) + "\n");

        int set2[] = { 1, 3, 4, 9, 7, 27 };
        int n2 = set2.length;
        System.out.print(lenOfLongestGP(set2, n2) + "\n");

        int set3[] = { 2, 3, 5, 7, 11, 13 };
        int n3 = set3.length;
        System.out.print(lenOfLongestGP(set3, n3) + "\n");
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to find length
# of the longest geometric
# progression in a given sett

# Returns length of the longest GP
# subset of sett[]

def lenOfLongestGP(sett, n):
    # Base cases
    if n < 2:
        return n
    if n == 2:
        return 2 if (sett[1] % sett[0] == 0) else 1
    # let us sort the sett first
    sett.sort()

    # An entry L[i][j] in this
    # table stores LLGP with
    # sett[i] and sett[j] as first
    # two elements of GP
    # and j > i.
    L = [[0 for i in range(n)] for i in range(n)]

    # Initialize result (A single
    # element is always a GP)
    llgp = 1

    # Initialize values of last column
    for i in range(0, n-1):
        if sett[n-1] % sett[i] == 0:
            L[i][n-1] = 2
            if 2 > llgp:
                llgp = 2
        else:
            L[i][n-1] = 1
    L[n-1][n-1] = 1

    # Consider every element as second element of GP
    for j in range(n-2, 0, -1):

        # Search for i and k for j
        i = j - 1
        k = j + 1
        while i >= 0 and k <= n - 1:

            # Two cases when i, j and k don't form
            # a GP.
            if sett[i] * sett[k] < sett[j] * sett[j]:
                k += 1
            elif sett[i] * sett[k] > sett[j] * sett[j]:
                if sett[j] % sett[i] == 0:
                    L[i][j] = 2
                else:
                    L[i][j] = 1
                i -= 1

            # i, j and k form GP, LLGP with i and j as
            # first two elements is equal to LLGP with
            # j and k as first two elements plus 1.
            # L[j][k] must have been filled before as
            # we run the loop from right side
            else:
                if sett[j] % sett[i] == 0:
                    L[i][j] = L[j][k] + 1

                    # Update overall LLGP
                    if L[i][j] > llgp:
                        llgp = L[i][j]
                else:
                    L[i][j] = 1

                # Change i and k to fill more L[i][j]
                # values for current j
                i -= 1
                k += 1

        # If the loop was stopped due to k becoming
        # more than n-1, set the remaining entries
        # in column j as 1 or 2 based on divisibility
        # of sett[j] by sett[i]
        while i >= 0:
            if sett[j] % sett[i] == 0:
                L[i][j] = 2
            else:
                L[i][j] = 1
            i -= 1

    return llgp

# Driver code
if __name__ == '__main__':
    set1 = [1, 3, 9, 27, 81, 243]
    n1 = len(set1)
    print(lenOfLongestGP(set1, n1))

    set2 = [1, 3, 4, 9, 7, 27]
    n2 = len(set2)
    print(lenOfLongestGP(set2, n2))

    set3 = [2, 3, 5, 7, 11, 13]
    n3 = len(set3)
    print(lenOfLongestGP(set3, n3))

# this code is contrubuted by sahilshelangia
```

## C#

```
// C# program to find length
// of the longest geometric
// progression in a given Set
using System;

class GFG
{

    // Returns length of the
    // longest GP subset of Set[]
    static int lenOfLongestGP(int []Set, int n)
    {
        // Base cases
        if (n < 2)
        {
            return n;
        }
        if (n == 2)
        {
            return (Set[1] % Set[0] == 0 ? 2 : 1);
        }

        // Let us sort the Set first
        Array.Sort(Set);

        // An entry L[i,j] in this table
        // stores LLGP with Set[i] and Set[j]
        // as first two elements of GP
        // and j > i.
        int [,]L = new int[n, n];

        // Initialize result (A single
        // element is always a GP)
        int llgp = 1;

        // Initialize values of last column
        for (int i = 0; i < n - 1; ++i)
        {
            if (Set[n - 1] % Set[i] == 0)
            {
                L[i, n - 1] = 2;
                if (2 > llgp)
                    llgp  = 2;
            }
            else
            {
                L[i, n - 1] = 1;
            }
        }
        L[n - 1, n - 1] = 1;

        // Consider every element
        // as second element of GP
        for (int j = n - 2; j >= 1; --j)
        {
            // Search for i and k for j
            int i = j - 1, k = j + 1;
            while (i >= 0 && k <= n - 1)
            {
                // Two cases when i, j and k
                // don't form a GP.
                if (Set[i] * Set[k] < Set[j] * Set[j])
                {
                    ++k;
                }
                else if (Set[i] * Set[k] > Set[j] * Set[j])
                {
                    if (Set[j] % Set[i] == 0)
                    {
                        L[i,j] = 2;
                        if (2 > llgp)
                            llgp = 2;
                    }
                    else
                    {
                        L[i,j] = 1;
                    }
                    --i;
                }

                // i, j and k form GP, LLGP with i and j as
                // first two elements is equal to LLGP with
                // j and k as first two elements plus 1.
                // L[j,k] must have been filled before as
                // we run the loop from right side
                else
                {
                    if (Set[j] % Set[i] == 0)
                    {
                        L[i, j] = L[j, k] + 1;

                        // Update overall LLGP
                        if (L[i, j] > llgp)
                        {
                            llgp = L[i, j];
                        }
                    }
                    else
                    {
                        L[i, j] = 1;
                    }

                    // Change i and k to fill more L[i,j]
                    // values for current j
                    --i;
                    ++k;
                }
            }

            // If the loop was stopped due to k becoming
            // more than n-1, set the remaining entries
            // in column j as 1 or 2 based on divisibility
            // of Set[j] by Set[i]
            while (i >= 0)
            {
                if (Set[j] % Set[i] == 0)
                {
                    L[i, j] = 2;
                    if (2 > llgp)
                        llgp = 2;
                }
                else
                {
                    L[i, j] = 1;
                }
                --i;
            }
        }

        // Return result
        return llgp;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []set1 = {1, 3, 9, 27, 81, 243};
        int n1 = set1.Length;
        Console.Write(lenOfLongestGP(set1, n1) + "\n");

        int []set2 = {1, 3, 4, 9, 7, 27};
        int n2 = set2.Length;
        Console.Write(lenOfLongestGP(set2, n2) + "\n");

        int []set3 = {2, 3, 5, 7, 11, 13};
        int n3 = set3.Length;
        Console.Write(lenOfLongestGP(set3, n3) + "\n");
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to find length
    // of the longest geometric
    // progression in a given set

    // Returns length of the longest GP subset of set[]
    function lenOfLongestGP(set, n)
    {
        // Base cases
        if (n < 2) {
            return n;
        }
        if (n == 2) {
            return (set[1] % set[0] == 0 ? 2 : 1);
        }

        // Let us sort the set first
        set.sort(function(a, b){return a - b});

        // An entry L[i][j] in this table
        // stores LLGP with set[i] and set[j]
        // as first two elements of GP
        // and j > i.
        let L = new Array(n);
        for (let i = 0; i < n; ++i)
        {
            L[i] = new Array(n);
            for (let j = 0; j < n; ++j)
            {
                L[i][j] = 0;
            }
        }

        // Initialize result (A single
        // element is always a GP)
        let llgp = 1;

        // Initialize values of last column
        for (let i = 0; i < n - 1; ++i) {
            if (set[n - 1] % set[i] == 0) {
                L[i][n - 1] = 2;
                if (2 > llgp)
                    llgp = 2;
            }
            else {
                L[i][n - 1] = 1;
            }
        }
        L[n - 1][n - 1] = 1;

        // Consider every element as second element of GP
        for (let j = n - 2; j >= 1; --j) {
            // Search for i and k for j
            let i = j - 1, k = j + 1;
            while (i >= 0 && k <= n - 1) {
                // Two cases when i, j and k
                // don't form a GP.
                if (set[i] * set[k] < set[j] * set[j]) {
                    ++k;
                }
                else if (set[i] * set[k]
                         > set[j] * set[j]) {
                    if (set[j] % set[i] == 0) {
                        L[i][j] = 2;
                        if (2 > llgp)
                            llgp = 2;
                    }
                    else {
                        L[i][j] = 1;
                    }
                    --i;
                }

                // i, j and k form GP, LLGP with i and j as
                // first two elements is equal to LLGP with
                // j and k as first two elements plus 1.
                // L[j][k] must have been filled before as
                // we run the loop from right side
                else {
                    if (set[j] % set[i] == 0) {
                        L[i][j] = L[j][k] + 1;

                        // Update overall LLGP
                        if (L[i][j] > llgp) {
                            llgp = L[i][j];
                        }
                    }
                    else {
                        L[i][j] = 1;
                    }

                    // Change i and k to fill more L[i][j]
                    // values for current j
                    --i;
                    ++k;
                }
            }

            // If the loop was stopped due to k becoming
            // more than n-1, set the remaining entries
            // in column j as 1 or 2 based on divisibility
            // of set[j] by set[i]
            while (i >= 0) {
                if (set[j] % set[i] == 0) {
                    L[i][j] = 2;
                    if (2 > llgp)
                        llgp = 2;
                }
                else {
                    L[i][j] = 1;
                }
                --i;
            }
        }

        // Return result
        return llgp;
    }

    let set1 = [ 1, 3, 9, 27, 81, 243 ];
    let n1 = set1.length;
    document.write(lenOfLongestGP(set1, n1) + "</br>");

    let set2 = [ 1, 3, 4, 9, 7, 27 ];
    let n2 = set2.length;
    document.write(lenOfLongestGP(set2, n2) + "</br>");

    let set3 = [ 2, 3, 5, 7, 11, 13 ];
    let n3 = set3.length;
    document.write(lenOfLongestGP(set3, n3) + "</br>");

// This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
6
4
1
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n <sup>2</sup> )
本文由 **Vivek Pandya** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。