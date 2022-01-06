# 将字符串的所有字符转换为给定字符所需的最少操作

> 原文:[https://www . geeksforgeeks . org/将字符串中的所有字符转换为给定字符所需的最小操作数/](https://www.geeksforgeeks.org/minimum-operations-required-to-convert-all-characters-of-a-string-to-a-given-character/)

给定字符串 **str** 、字符 **ch** 和整数 **K** ，任务是找到将字符串 **str** 的所有字符转换为 **ch** 所需的最小操作数。每个操作都涉及到从索引 **i** 的每一侧转换 **K** 最接近的字符，即索引**【I–K，I+K】**中的字符可以转换为 **ch** 。
**注意:**每个指标只能是单个操作的一部分。
**例:**

> **输入:** str = "abcsdx "，K = 2，ch = '#'
> **输出:** 2
> **解释:**
> 操作 1:选择 i = 1，因此，str =**a**BCS dx“修改为###sdx”。
> 操作 2:选择 i = 6，因此 str = # # # SD**x**修改为“######”。
> 
> **输入:**str =“hellomipkfsg”，k = 3，ch = ' { content } '-2019；
> **输出:** 2
> 说明:
> 操作 1:选择 i = 2，因此，str =“H**e**llomypkfsg”修改为“$$$mypkfsg”。
> 操作 2:选择 i = 9，因此 str = $ $ $ myp**k**fsg“修改为“$$$$$”。

**方法:**
按照以下步骤解决问题:

1.  对于任何索引 **i** ，可以转换的最大字符数为 **2 * K + 1** 。因此，如果字符串中的字符总数不超过 **2 * K** ，只需要一次操作就可以将整个字符串转换为 **ch** 。
2.  否则所需操作次数为 **ceil(n / (2*k+1))** 。
3.  迭代字符串，从可用于操作的最左边可能的索引开始，并在其后打印每个 **(2*k+1) <sup>第</sup>索引**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of operations required
void countOperations(int n, int k)
{
    // Maximum number of characters that
    // can be changed in one operation
    int div = 2 * k + 1;

    // If length of the string less than
    // maximum number of characters that
    // can be changed in an operation
    if (n / 2 <= k) {
        cout << 1 << "\n";

        // Set the last index as the
        // index for the operation
        if (n > k)
            cout << k + 1;

        else
            cout << n;
    }

    // Otherwise
    else {

        // If size of the string is
        // equal to the maximum number
        // of characters in an operation
        if (n % div == 0) {

            // Find the number of
            // operations required
            int oprn = n / div;

            cout << oprn << "\n";

            // Find the starting position
            int pos = k + 1;

            cout << pos << " ";
            for (int i = 1; i <= oprn; i++) {
                // Print i-th index
                cout << pos << " ";

                // Shift to next index
                pos += div;
            }
        }

        // Otherwise
        else {

            // Find the number of
            // operations required
            int oprn = n / div + 1;
            cout << oprn << "\n";

            int pos = n % div;

            // If n % div exceeds k
            if (n % div > k)
                pos -= k;

            for (int i = 1; i <= oprn; i++) {

                // Print i-th index
                cout << pos << " ";

                // Shift to next index
                pos += div;
            }
        }
    }
}

// Driver Code
int main()
{
    string str = "edfreqwsazxet";
    char ch = '{content}apos;;
    int n = str.size();
    int k = 4;
    countOperations(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to find the minimum
// number of operations required
static void countOperations(int n, int k)
{

    // Maximum number of characters that
    // can be changed in one operation
    int div = 2 * k + 1;

    // If length of the String less than
    // maximum number of characters that
    // can be changed in an operation
    if (n / 2 <= k)
    {
        System.out.print(1 + "\n");

        // Set the last index as the
        // index for the operation
        if (n > k)
            System.out.print(k + 1);

        else
            System.out.print(n);
    }

    // Otherwise
    else
    {

        // If size of the String is
        // equal to the maximum number
        // of characters in an operation
        if (n % div == 0)
        {

            // Find the number of
            // operations required
            int oprn = n / div;

            System.out.print(oprn + "\n");

            // Find the starting position
            int pos = k + 1;

            System.out.print(pos + " ");
            for(int i = 1; i <= oprn; i++)
            {

                // Print i-th index
                System.out.print(pos + " ");

                // Shift to next index
                pos += div;
            }
        }

        // Otherwise
        else
        {

            // Find the number of
            // operations required
            int oprn = n / div + 1;
            System.out.print(oprn + "\n");

            int pos = n % div;

            // If n % div exceeds k
            if (n % div > k)
                pos -= k;

            for(int i = 1; i <= oprn; i++)
            {

                // Print i-th index
                System.out.print(pos + " ");

                // Shift to next index
                pos += div;
            }
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    String str = "edfreqwsazxet";
    char ch = '{content}apos;;
    int n = str.length();
    int k = 4;

    countOperations(n, k);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum
# number of operations required
def countOperations(n, k):

    # Maximum number of characters that
    # can be changed in one operation
    div = 2 * k + 1

    # If length of the less than
    # maximum number of characters that
    # can be changed in an operation
    if (n // 2 <= k):
        print(1)

        # Set the last index as the
        # index for the operation
        if (n > k):
            print(k + 1)
        else:
            print(n)

    # Otherwise
    else:

        # If size of the is
        # equal to the maximum number
        # of characters in an operation
        if (n % div == 0):

            # Find the number of
            # operations required
            oprn = n // div

            print(oprn)

            # Find the starting position
            pos = k + 1

            print(pos, end = " ")
            for i in range(1, oprn + 1):

                # Print i-th index
                print(pos, end = " ")

                # Shift to next index
                pos += div

        # Otherwise
        else:

            # Find the number of
            # operations required
            oprn = n // div + 1
            print(oprn)

            pos = n % div

            # If n % div exceeds k
            if (n % div > k):
                pos -= k

            for i in range(1, oprn + 1):

                # Print i-th index
                print(pos, end = " ")

                # Shift to next index
                pos += div

# Driver Code
if __name__ == '__main__':

    str = "edfreqwsazxet"
    ch = '{content}apos;
    n = len(str)
    k = 4

    countOperations(n, k)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the minimum
// number of operations required
static void countOperations(int n, int k)
{

    // Maximum number of characters that
    // can be changed in one operation
    int div = 2 * k + 1;

    // If length of the String less than
    // maximum number of characters that
    // can be changed in an operation
    if (n / 2 <= k)
    {
        Console.Write(1 + "\n");

        // Set the last index as the
        // index for the operation
        if (n > k)
            Console.Write(k + 1);

        else
            Console.Write(n);
    }

    // Otherwise
    else
    {

        // If size of the String is
        // equal to the maximum number
        // of characters in an operation
        if (n % div == 0)
        {

            // Find the number of
            // operations required
            int oprn = n / div;

            Console.Write(oprn + "\n");

            // Find the starting position
            int pos = k + 1;

            Console.Write(pos + " ");
            for(int i = 1; i <= oprn; i++)
            {

                // Print i-th index
                Console.Write(pos + " ");

                // Shift to next index
                pos += div;
            }
        }

        // Otherwise
        else
        {

            // Find the number of
            // operations required
            int oprn = n / div + 1;
            Console.Write(oprn + "\n");

            int pos = n % div;

            // If n % div exceeds k
            if (n % div > k)
                pos -= k;

            for(int i = 1; i <= oprn; i++)
            {

                // Print i-th index
                Console.Write(pos + " ");

                // Shift to next index
                pos += div;
            }
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    String str = "edfreqwsazxet";
    int n = str.Length;
    int k = 4;

    countOperations(n, k);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach   
// Function to find the minimum
    // number of operations required
    function countOperations(n , k) {

        // Maximum number of characters that
        // can be changed in one operation
        var div = 2 * k + 1;

        // If length of the String less than
        // maximum number of characters that
        // can be changed in an operation
        if (n / 2 <= k) {
            document.write(1 + "<br/>");

            // Set the last index as the
            // index for the operation
            if (n > k)
                document.write(k + 1);

            else
                document.write(n);
        }

        // Otherwise
        else {

            // If size of the String is
            // equal to the maximum number
            // of characters in an operation
            if (n % div == 0) {

                // Find the number of
                // operations required
                var oprn = parseInt(n / div);

                document.write(oprn + "<br/>");

                // Find the starting position
                var pos = k + 1;

                document.write(pos + " ");
                for (i = 1; i <= oprn; i++) {

                    // Print i-th index
                    document.write(pos + " ");

                    // Shift to next index
                    pos += div;
                }
            }

            // Otherwise
            else {

                // Find the number of
                // operations required
                var oprn = parseInt(n / div + 1);
                document.write(oprn + "<br/>");

                var pos = n % div;

                // If n % div exceeds k
                if (n % div > k)
                    pos -= k;

                for (i = 1; i <= oprn; i++) {

                    // Print i-th index
                    document.write(pos + " ");

                    // Shift to next index
                    pos += div;
                }
            }
        }
    }

    // Driver Code

        var str = "edfreqwsazxet";
        var ch = '{content}apos;;
        var n = str.length;
        var k = 4;

        countOperations(n, k);

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
2
4 13
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*