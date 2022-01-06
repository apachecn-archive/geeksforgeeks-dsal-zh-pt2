# 执行给定操作后阵列中最大可能乘积

> 原文:[https://www . geeksforgeeks . org/执行给定操作后阵列中产品的最大可能数量/](https://www.geeksforgeeks.org/maximum-possible-product-in-array-after-performing-given-operations/)

给定大小为 n 的数组。您可以对给定的数组执行两种类型的操作，如下所述:

1.  选择一些位置 **i** 和 **j** ，使得 **(i 不等于 j)** ，将**a【j】**的值替换为**a【I】* a【j】**，并从 **i** <sup>第</sup>个单元格中删除该数字。
2.  选择某个位置 **i** 并从 **i** <sup>第</sup>个单元格中删除该数字(该操作最多可执行一次，可在任何时间点执行，不一定在开始时执行)。

任务是用数组精确地执行 N-1 个操作，使得数组中剩下的唯一数字是最大可能的。这个数字可能相当大，所以不打印它，而是打印导致这个最大数字的操作序列。

输出应该正好包含 N-1 行:

> *   If the operation is the first type, print **1ij** .
> *   If the operation is the second type, print **2I** .

**注**:该数组被认为是有基于 1 的索引。

**示例**:

```
Input : a[] = { 5, -2, 0, 1, -3 }
Output : 2 3
         1 1 2
         1 2 4
         1 4 5
Explanation: 
Step 1: a[3] is removed.
Step 2: a[2] = a[2]*a[1] = -10; a[1] is removed.
Step 3: a[4] = a[4]*a[2] = -10; a[2] is removed.
Step 4: a[5] = a[5]*a[4] = 30; a[4] is removed.
So, the maximum product is 30.

Input : a[] = { 0, 0, 0, 0 }
Output : 1 1 2
         1 2 3
         1 3 4
```

**处理方法:**问题中有几种情况。设数组中的零个数为 **cntZero** ，负元素个数为 **cntNeg** 。同样让 **maxNeg** 成为数组中最大负元素的位置，如果数组中没有负元素，则为-1。

让答案部分是答案中所有数字的乘积，而去掉的部分是第二类运算将去掉的所有数字的乘积。

案例如下:

1.  第一种情况是当 **cntZero=0** 和 **cntNeg=0** 时。那么答案部分就是数组中所有数字的乘积。移除的零件是空的。
2.  第二种情况是 **cntNeg** 为奇数时。那么答案部分就是数组中除了全 0 和**a【maxNeg】**之外的所有数字的乘积。移除的部分是全零和**a【maxNeg】**的乘积。
3.  第三种情况是 **cntNeg** 为偶数时。那么答案部分就是数组中除零以外的所有数字的乘积。移除的部分是数组中所有零的乘积(小心 **cntNeg=0** 和 **cntZero=n** )。

下面是上述想法的实现:

## C++

```
// CPP program for maximum possible product
// with given array of numbers
#include <bits/stdc++.h>
using namespace std;

// Function that prints operations in each step
void MaximumProduct(int a[], int n)
{
    int cntneg = 0;
    int cntzero = 0;

    int used[n] = { 0 };
    int pos = -1;

    // count number of zeros and negative numbers
    for (int i = 0; i < n; ++i) {
        if (a[i] == 0) {
            used[i] = 1;
            cntzero++;
        }

        if (a[i] < 0) {
            cntneg++;

            // To get negative number which
            // is nearest to zero, that is maximum
            // negative number
            if (pos == -1 || abs(a[pos]) > abs(a[i]))
                pos = i;
        }
    }

    // if number of negative number are odd then
    // remove negative number at position pos
    if (cntneg % 2 == 1)
        used[pos] = 1;

    // initial condition
    if (cntzero == n || (cntzero == n - 1 &&
                                    cntneg == 1)) {
        for (int i = 0; i < n - 1; ++i)
            cout << 1 << " " << i + 1 << " "
                                << i + 2 << endl;
        return;
    }

    int lst = -1;
    for (int i = 0; i < n; ++i) {
        if (used[i]) {
            if (lst != -1)
                cout << 1 << " " << lst + 1 << " "
                                << i + 1 << endl;
            lst = i;
        }
    }

    // perform second type operation
    if (lst != -1)
        cout << 2 << " " << lst + 1 << endl;

    lst = -1;

    // for remaining numbers
    for (int i = 0; i < n; ++i) {
        // if it is not removed yet
        if (!used[i]) {
            if (lst != -1)
                cout << 1 << " " << lst + 1 << " "
                                    << i + 1 << endl;
            lst = i;
        }
    }
}

// Driver code
int main()
{
    int a[] = { 5, -2, 0, 1, -3 };

    int n = sizeof(a) / sizeof(a[0]);

    MaximumProduct(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for maximum possible product
// with given array of numbers
class GFG {

// Function that prints operations in each step
static void MaximumProduct(int a[], int n) {
    int cntneg = 0;
    int cntzero = 0;

    int used[] = new int[n];
    int pos = -1;

    // count number of zeros and negative numbers
    for (int i = 0; i < n; ++i) {
        if (a[i] == 0)
        {
            used[i] = 1;
            cntzero++;

        }

        if (a[i] < 0) {
            cntneg++;

            // To get negative number which
            // is nearest to zero, that is maximum
            // negative number
            if (pos == -1 || Math.abs(a[pos]) > Math.abs(a[i])) {
                pos = i;

            }

        }

    }

    // if number of negative number are odd then
    // remove negative number at position pos
    if (cntneg % 2 == 1) {
        used[pos] = 1;

    }

    // initial condition
    if (cntzero == n || (cntzero == n - 1 && cntneg == 1))
    {             
        for (int i = 0; i < n - 1; ++i) {
            System.out.println(1 + " " + (i + 1) + " "
                        + (i + 2));

        }
        return;

    }

    int lst = -1;
    for (int i = 0; i < n; ++i) {
        if (used[i] == 1) {
            if (lst != -1) {
                System.out.println(1 + " " + (lst + 1) + " "
                            + (i + 1));

            }
            lst = i;

        }

    }

    // perform second type operations
    if (lst != -1) {
        System.out.println(2 + " " + (lst + 1));

    }
    lst = -1;
    // for remaining numbers
    for (int i = 0; i < n; ++i)
    {
        // if it is not removed yet
        if (used[i] != 1)
        {
            if (lst != -1)
            {
                System.out.println(1 + " " + (lst + 1) + " "
                            + (i + 1));

            }
            lst = i;
        }
    }

}

// Driver code
public static void main(String[] args)
{
    int a[] = {5, -2, 0, 1, -3};
    int n = a.length;
    MaximumProduct(a, n);

}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for maximum possible product
# with given array of numbers

# Function that prints operations
# in each step
def MaximumProduct(a, n):
    cntneg = 0
    cntzero = 0

    used = [0] * n
    pos = -1

    # count number of zeros and
    # negative numbers
    for i in range(n):
        if (a[i] == 0) :
            used[i] = 1
            cntzero += 1

        if (a[i] < 0):
            cntneg += 1

            # To get negative number which
            # is nearest to zero, that is maximum
            # negative number
            if (pos == -1 or abs(a[pos]) > abs(a[i])):
                pos = i

    # if number of negative number are odd then
    # remove negative number at position pos
    if (cntneg % 2 == 1):
        used[pos] = 1

    # initial condition
    if (cntzero == n or (cntzero == n - 1 and
                         cntneg == 1)):
        for i in range(n - 1):
            print (1, " ", i + 1, " ", i + 2)
        return

    lst = -1
    for i in range(n) :
        if (used[i]) :
            if (lst != -1):
                print (1, " ", lst + 1, " ", i + 1)
            lst = i

    # perform second type operation
    if (lst != -1):
        print (2, " ", lst + 1)

    lst = -1

    # for remaining numbers
    for i in range( n) :

        # if it is not removed yet
        if (not used[i]) :
            if (lst != -1):
                print (1, " ", lst + 1, " ", i + 1)
            lst = i

# Driver code
if __name__ == "__main__":
    a = [ 5, -2, 0, 1, -3 ]

    n = len(a)

    MaximumProduct(a, n)

# This code is contributed by ita_c
```

## C#

```
// C# program for maximum possible product
// with given array of numbers
using System;

class GFG
{

// Function that prints
// operations in each step
static void MaximumProduct(int []a, int n)
{
    int cntneg = 0;
    int cntzero = 0;

    int []used = new int[n];
    int pos = -1;

    // count number of zeros
    // and negative numbers
    for (int i = 0; i < n; ++i)
    {
        if (a[i] == 0)
        {
            used[i] = 1;
            cntzero++;

        }

        if (a[i] < 0)
        {
            cntneg++;

            // To get negative number which
            // is nearest to zero, that is
            //  maximum negative number
            if (pos == -1 || Math.Abs(a[pos]) >
                                Math.Abs(a[i]))
            {
                pos = i;

            }

        }

    }

    // if number of negative number are odd then
    // remove negative number at position pos
    if (cntneg % 2 == 1)
    {
        used[pos] = 1;

    }

    // initial condition
    if (cntzero == n || (cntzero == n - 1 &&
                                cntneg == 1))
    {        
        for (int i = 0; i < n - 1; ++i)
        {
            Console.WriteLine(1 + " " + (i + 1) + " "
                        + (i + 2));
        }
        return;

    }

    int lst = -1;
    for (int i = 0; i < n; ++i)
    {
        if (used[i] == 1)
        {
            if (lst != -1)
            {
                Console.WriteLine(1 + " " + (lst + 1) + " "
                            + (i + 1));
            }
            lst = i;

        }

    }

    // perform second type operations
    if (lst != -1)
    {
        Console.WriteLine(2 + " " + (lst + 1));

    }
    lst = -1;

    // for remaining numbers
    for (int i = 0; i < n; ++i)
    {
        // if it is not removed yet
        if (used[i] != 1)
        {
            if (lst != -1)
            {
                Console.WriteLine(1 + " " + (lst + 1) + " "
                            + (i + 1));
            }
            lst = i;
        }
    }

}

    // Driver code
    static public void Main ()
    {
        int []a = {5, -2, 0, 1, -3};
        int n = a.Length;
        MaximumProduct(a, n);
    }
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>

// JavaScript program for maximum possible product
// with given array of numbers

// Function that prints operations in each step
function MaximumProduct(a, n)
{
    let cntneg = 0;
    let cntzero = 0;

    let used = new Uint8Array(n);
    let pos = -1;

    // count number of zeros and negative numbers
    for (let i = 0; i < n; ++i) {
        if (a[i] == 0) {
            used[i] = 1;
            cntzero++;
        }

        if (a[i] < 0) {
            cntneg++;

            // To get negative number which
            // is nearest to zero, that is maximum
            // negative number
            if (pos == -1 || Math.abs(a[pos]) > Math.abs(a[i]))
                pos = i;
        }
    }

    // if number of negative number are odd then
    // remove negative number at position pos
    if (cntneg % 2 == 1)
        used[pos] = 1;

    // initial condition
    if (cntzero == n || (cntzero == n - 1 &&
                                    cntneg == 1)) {
        for (let i = 0; i < n - 1; ++i)
            document.write(1 + " " + (i + 1) + " "
                                + (i + 2) + "<br>");
        return;
    }

    let lst = -1;
    for (let i = 0; i < n; ++i) {
        if (used[i]) {
            if (lst != -1)
                document.write(1 + " " + (lst + 1) + " "
                                + (i + 1) + "<br>");
            lst = i;
        }
    }

    // perform second type operation
    if (lst != -1)
        document.write(2 + " " + (lst + 1) + "<br>");

    lst = -1;

    // for remaining numbers
    for (let i = 0; i < n; ++i) {
        // if it is not removed yet
        if (!used[i]) {
            if (lst != -1)
                document.write(1 + " " + (lst + 1) + " "
                                    + (i + 1) + "<br>");
            lst = i;
        }
    }
}

// Driver code

    let a = [ 5, -2, 0, 1, -3 ];

    let n = a.length;

    MaximumProduct(a, n);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
2 3
1 1 2
1 2 4
1 4 5
```

**时间复杂度:** O(n)