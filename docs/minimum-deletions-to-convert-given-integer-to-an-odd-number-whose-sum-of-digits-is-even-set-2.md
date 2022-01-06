# 将给定整数转换为奇数(其位数总和为偶数)的最小删除数|设置 2

> 原文:[https://www . geesforgeks . org/minimum-deletions-convert-给定整数到奇数-其位数总和为偶数-set-2/](https://www.geeksforgeeks.org/minimum-deletions-to-convert-given-integer-to-an-odd-number-whose-sum-of-digits-is-even-set-2/)

给定一个正的[整数](https://www.geeksforgeeks.org/integer-promotions-in-c/) **N** ，任务是找到将 **N** 转换为奇数所需移除的最小位数，该奇数的[位数之和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)为偶数。如果不可能，则打印**“不可能”。**

**示例:**

> **输入:** N = 12345
> **输出:** 1
> **说明:**
> 去掉数字 3 将 N 修改为 1245。
> 由于 N 的位数之和为 14，N 为奇数，所以需要的输出为 1。
> 
> **输入:**N = 222
> T3】输出:不可能

**方法:**想法是利用奇数的偶数计数相加得到偶数的事实。按照以下步骤解决问题:

*   [统计整数 **N**](https://www.geeksforgeeks.org/count-even-odd-digits-integer/) 中出现的总计**奇数**和**偶数** [位数，并将其存储在变量中，比如**奇数**和**偶数。**](https://www.geeksforgeeks.org/count-even-odd-digits-integer/)
*   如果**奇数= 0** ，则不能通过删除任意位数将整数转换为奇数。因此，打印**“不可能”**。
*   否则，如果**奇数= 1** ，那么为了使位数之和为偶数，必须删除该奇数，从而产生偶数。因此，打印“**不可能”。**
*   现在，计算奇数位最后出现后要删除的位数，并将其存储在一个变量中，比如**和**。
*   如果**奇数**是奇数，那么将**和**的计数增加 1，因为必须删除一个奇数位才能使总和为偶数。
*   最后，如果以上情况都不满足，打印**和**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of digits
// required to be remove to make N odd and
// the sum of digits of N even
void minOperations(string& N)
{

    // Stores count of even digits
    int even = 0;

    // Stores count of odd digits
    int odd = 0;

    // Iterate over the digits of N
    for (auto it : N) {

        // If current digit is even
        if ((it - '0') % 2 == 0) {

            // Update even
            even++;
        }

        // Otherwise
        else {

            // Update odd
            odd++;
        }
    }

    // Base conditions
    if (odd == 0 || odd == 1) {
        cout << "Not Possible"
             << "\n";
    }

    else {

        // Stores count of digits required to be
        // removed to make N odd and the sum of
        // digits of N even
        int ans = 0;

        // Iterate over the digits of N
        for (auto it : N) {

            // If current digit is even
            if ((it - '0') % 2 == 0) {

                // Update ans
                ans++;
            }

            // Otherwise,
            else {

                // Update ans
                ans = 0;
            }
        }

        // If count of odd digits is odd
        if (odd % 2) {

            // Update ans
            ans++;
        }

        // Finally print the ans
        cout << ans << endl;
    }
}

// Driver code
int main()
{

    // Input string
    string N = "12345";

    // Function call
    minOperations(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG
{

// Function to find minimum count of digits
// required to be remove to make N odd and
// the sum of digits of N even
static void minOperations(String N)
{

    // Stores count of even digits
    int even = 0;

    // Stores count of odd digits
    int odd = 0;

    // Iterate over the digits of N
    for (int it : N.toCharArray())
    {

        // If current digit is even
        if ((it - '0') % 2 == 0)
        {

            // Update even
            even++;
        }

        // Otherwise
        else
        {

            // Update odd
            odd++;
        }
    }

    // Base conditions
    if (odd == 0 || odd == 1)
    {
        System.out.print("Not Possible"
            + "\n");
    }

    else
    {

        // Stores count of digits required to be
        // removed to make N odd and the sum of
        // digits of N even
        int ans = 0;

        // Iterate over the digits of N
        for (int it : N.toCharArray())
        {

            // If current digit is even
            if ((it - '0') % 2 == 0)
            {

                // Update ans
                ans++;
            }

            // Otherwise,
            else
            {

                // Update ans
                ans = 0;
            }
        }

        // If count of odd digits is odd
        if (odd % 2 != 0)
        {

            // Update ans
            ans++;
        }

        // Finally print the ans
        System.out.print(ans +"\n");
    }
}

// Driver code
public static void main(String[] args)
{

    // Input String
    String N = "12345";

    // Function call
    minOperations(N);
}
}

// This code is contributed by shikhasingrajput.
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to find minimum count of digits
# required to be remove to make N odd and
# the sum of digits of N even
def minOperations(N):

    # Stores count of even digits
    even = 0;

    # Stores count of odd digits
    odd = 0;

    # Iterate over the digits of N
    for it in  N:

        # If current digit is even
        if (int(ord(it) - ord('0')) % 2 == 0):

            # Update even
            even += 1;

        # Otherwise
        else:

            # Update odd
            odd += 1;

    # Base conditions
    if (odd == 0 or odd == 1):
        print("Not Possible" + "");

    else:

        # Stores count of digits required to be
        # removed to make N odd and the sum of
        # digits of N even
        ans = 0;

        # Iterate over the digits of N
        for it in N:

            # If current digit is even
            if (int(ord(it) - ord('0')) % 2 == 0):

                # Update ans
                ans += 1;

            # Otherwise,
            else:

                # Update ans
                ans = 0;

        # If count of odd digits is odd
        if (odd % 2 != 0):

            # Update ans
            ans += 1;

        # Finally print the ans
        print(ans, end=" ");

# Driver code
if __name__ == '__main__':

    # Input String
    N = "12345";

    # Function call
    minOperations(N);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# implementation of the above approach
using System;
class GFG
{

// Function to find minimum count of digits
// required to be remove to make N odd and
// the sum of digits of N even
static void minOperations(String N)
{

    // Stores count of even digits
    int even = 0;

    // Stores count of odd digits
    int odd = 0;

    // Iterate over the digits of N
    foreach (int it in N.ToCharArray())
    {

        // If current digit is even
        if ((it - '0') % 2 == 0)
        {

            // Update even
            even++;
        }

        // Otherwise
        else
        {

            // Update odd
            odd++;
        }
    }

    // Base conditions
    if (odd == 0 || odd == 1)
    {
        Console.Write("Not Possible"
            + "\n");
    }
    else
    {

        // Stores count of digits required to be
        // removed to make N odd and the sum of
        // digits of N even
        int ans = 0;

        // Iterate over the digits of N
        foreach (int it in N.ToCharArray())
        {

            // If current digit is even
            if ((it - '0') % 2 == 0)
            {

                // Update ans
                ans++;
            }

            // Otherwise,
            else
            {

                // Update ans
                ans = 0;
            }
        }

        // If count of odd digits is odd
        if (odd % 2 != 0)
        {

            // Update ans
            ans++;
        }

        // Finally print the ans
        Console.Write(ans +"\n");
    }
}

// Driver code
public static void Main(String[] args)
{

    // Input String
    String N = "12345";

    // Function call
    minOperations(N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find minimum count of digits
// required to be remove to make N odd and
// the sum of digits of N even
function minOperations(N)
{

    // Stores count of even digits
    var even = 0;

    // Stores count of odd digits
    var odd = 0;

    // Iterate over the digits of N
    for (var it =0; it<N.length; it++) {

        // If current digit is even
        if ((N[it] - '0') % 2 == 0) {

            // Update even
            even++;
        }

        // Otherwise
        else {

            // Update odd
            odd++;
        }
    }

    // Base conditions
    if (odd == 0 || odd == 1) {
        document.write( "Not Possible"
             + "<br>");
    }

    else {

        // Stores count of digits required to be
        // removed to make N odd and the sum of
        // digits of N even
        var ans = 0;

        // Iterate over the digits of N
        for (var it =0; it<N.length; it++){

            // If current digit is even
            if ((N[it] - '0') % 2 == 0) {

                // Update ans
                ans++;
            }

            // Otherwise,
            else {

                // Update ans
                ans = 0;
            }
        }

        // If count of odd digits is odd
        if (odd % 2) {

            // Update ans
            ans++;
        }

        // Finally print the ans
        document.write( ans );
    }
}

// Driver code

// Input string
var N = "12345";

// Function call
minOperations(N);

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(log<sub>10</sub>(N))*
***辅助空间:** O(1)*