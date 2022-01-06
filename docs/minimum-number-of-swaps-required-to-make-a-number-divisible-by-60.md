# 使一个数可被 60 整除所需的最小互换次数

> 原文:[https://www . geeksforgeeks . org/最小交换次数-需要进行 60 除数/](https://www.geeksforgeeks.org/minimum-number-of-swaps-required-to-make-a-number-divisible-by-60/)

给定一个整数 **N** ，任务是找到使 N 能被 60 整除所需的最小交换次数。如果不可能，则打印“ **-1** ”。
**例:**

> **输入:** N = 603
> **输出:** 2
> **说明:**
> 需要两次交换操作:
> 第一次交换(0，3): 630
> 第二次交换(6，3): 360
> 现在 360 可以被 60 整除。
> 因此，至少需要两次互换。
> **输入:** N = 205
> **输出:** -1

**进场:**

1.  一个数要能被 60 整除，它必须能被 2、3 和 10 整除。因此:
    *   如果数字的位数之和不能被 3 整除，或者
    *   如果没有可被 2 整除的数字，或者
    *   如果数字不包含任何 0，
2.  那么所需的最小互换数量可以通过以下规则来确定:
    *   如果数字已经可以被 60 整除，则需要 **0 交换**。如果最后一个数字(LSB)为 0，并且第二个最后一个数字可被 2 整除，则可以确定这一点。
    *   如果以下任一情况为真，则需要 **1 交换**。
        *   如果最后一个数字(LSB)是 0，第二个最后一个数字不能被 2 整除，或者，最后一个数字(LSB)可以被 2 整除，第二个最后一个数字是 0。
        *   如果最后一个数字(LSB)是 0，第二个最后一个数字不能被 2 整除，并且数字中有 1 个以上的零。
    *   否则需要 2 次互换

以下是上述方法的实施

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find minimum number
// of swap operations required
#include <bits/stdc++.h>
using namespace std;

// Function that print minimum number
// of swap operations required
void MinimumSwapOperations(string s)
{
    bool zero_exist = false;
    bool multiple_of_2 = false;
    int sum = 0;
    int index_of_zero;
    bool more_zero = false;

    for (int i = 0; i < s.length(); i++) {
        int val = s[i] - '0';

        // Condition if more than one
        // zero exist
        if (zero_exist == true)
            more_zero = true;

        // Condition if zero_exist
        if (val == 0) {
            zero_exist = true;
            index_of_zero = i;
        }

        // Computing total sum of all digits
        sum += val;
    }

    // Condition if zero does not exist or
    // the sum is not divisible by 3
    if (zero_exist == false || sum % 3 != 0) {
        cout << "-1"
             << "\n";
        return;
    }

    for (int i = 0; i < s.length(); i++) {
        int val = s[i] - '0';

        // Condition to find a digit that is
        // multiple of 2 other than one zero
        if (val % 2 == 0 && i != index_of_zero)
            multiple_of_2 = true;
    }

    // Condition if multiple of 2
    // do not exist
    if (multiple_of_2 == false) {
        cout << "-1"
             << "\n";
        return;
    }

    int last_val = s[s.length() - 1] - '0';
    int second_last_val = s[s.length() - 2]
                          - '0';

    // Condition for zero swaps
    // means the number is already
    // is divisible by 60
    if (last_val == 0
        && second_last_val % 2 == 0)
        cout << 0 << "\n";

    // Condition for only one swap
    else if ((last_val == 0
              && second_last_val % 2 != 0)
             || (last_val % 2 == 0
                 && second_last_val == 0))
        cout << 1 << "\n";

    else if (more_zero == true
             && (last_val == 0
                 && second_last_val % 2 != 0))
        cout << 1 << "\n";

    // Otherwise 2 swaps required
    else
        cout << 2 << "\n";
}

// Driver Code
int main()
{
    string N = "20";

    MinimumSwapOperations(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// of swap operations required
class GFG {

    // Function that print minimum number
    // of swap operations required
    static void MinimumSwapOperations(String s)
    {
        boolean zero_exist = false;
        boolean multiple_of_2 = false;
        int sum = 0;
        int index_of_zero = 0;
        boolean more_zero = false;

        for (int i = 0; i < s.length(); i++) {
            int val = s.charAt(i) - '0';

            // Condition if more than one
            // zero exist
            if (zero_exist == true)
                more_zero = true;

            // Condition if zero_exist
            if (val == 0) {
                zero_exist = true;
                index_of_zero = i;
            }

            // Computing total sum of all digits
            sum += val;
        }

        // Condition if zero does not exist or
        // the sum is not divisible by 3
        if (zero_exist == false || sum % 3 != 0) {
            System.out.println("-1");
            return;
        }

        for (int i = 0; i < s.length(); i++) {
            int val = s.charAt(i) - '0';

            // Condition to find a digit that is
            // multiple of 2 other than one zero
            if (val % 2 == 0 && i != index_of_zero)
                multiple_of_2 = true;
        }

        // Condition if multiple of 2
        // do not exist
        if (multiple_of_2 == false) {
            System.out.println("-1");
            return;
        }

        int last_val = s.charAt(s.length() - 1)- '0';
        int second_last_val = s.charAt(s.length() - 2)- '0';

        // Condition for zero swaps
        // means the number is already
        // is divisible by 60
        if (last_val == 0&& second_last_val % 2 == 0)
            System.out.println(0);

        // Condition for only one swap
        else if ((last_val == 0
                  && second_last_val % 2 != 0)
                 || (last_val % 2 == 0
                     && second_last_val == 0))
            System.out.println(1);

        else if (more_zero == true
                 && (last_val == 0
                     && second_last_val % 2 != 0))
            System.out.println(1) ;

        // Otherwise 2 swaps required
        else
            System.out.println(2) ;
    }

    // Driver Code
    public static void main (String[] args)
    {
        String N = "20";

        MinimumSwapOperations(N);

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find minimum number
# of swap operations required

# Function that prminimum number
# of swap operations required
def MinimumSwapOperations(s):
    zero_exist = False
    multiple_of_2 = False
    sum = 0
    index_of_zero = 0
    more_zero = False

    for i in range(len(s)):
        val = ord(s[i]) - ord('0')

        # Condition if more than one
        # zero exist
        if (zero_exist == True):
            more_zero = True

        # Condition if zero_exist
        if (val == 0):
            zero_exist = True
            index_of_zero = i

        # Computing total sum of all digits
        sum += val

    # Condition if zero does not exist or
    # the sum is not divisible by 3
    if (zero_exist == False or sum % 3 != 0):
        print("-1")
        return

    for i in range(len(s)):
        val = ord(s[i]) - ord('0')

        # Condition to find a digit that is
        # multiple of 2 other than one zero
        if (val % 2 == 0 and i != index_of_zero):
            multiple_of_2 = True

    # Condition if multiple of 2
    # do not exist
    if (multiple_of_2 == False):
        print("-1")
        return

    last_val = ord(s[len(s) - 1]) - ord('0')
    second_last_val = ord(s[len(s) - 2])- ord('0')

    # Condition for zero swaps
    # means the number is already
    # is divisible by 60
    if (last_val == 0
        and second_last_val % 2 == 0):
        print(0)

    # Condition for only one swap
    elif ((last_val == 0
            and second_last_val % 2 != 0)
            or (last_val % 2 == 0
                and second_last_val == 0)):
        print(1)

    elif (more_zero == True
            and (last_val == 0
                and second_last_val % 2 != 0)):
        print(1)

    # Otherwise 2 swaps required
    else:
        print(2)

# Driver Code
if __name__ == '__main__':
    N = "20"

    MinimumSwapOperations(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find minimum number
// of swap operations required
using System;

class GFG {

    // Function that print minimum number
    // of swap operations required
    static void MinimumSwapOperations(string s)
    {
        bool zero_exist = false;
        bool multiple_of_2 = false;
        int sum = 0;
        int index_of_zero = 0;
        bool more_zero = false;

        for (int i = 0; i < s.Length; i++) {
            int val = s[i] - '0';

            // Condition if more than one
            // zero exist
            if (zero_exist == true)
                more_zero = true;

            // Condition if zero_exist
            if (val == 0) {
                zero_exist = true;
                index_of_zero = i;
            }

            // Computing total sum of all digits
            sum += val;
        }

        // Condition if zero does not exist or
        // the sum is not divisible by 3
        if (zero_exist == false || sum % 3 != 0) {
            Console.WriteLine("-1");
            return;
        }

        for (int i = 0; i < s.Length; i++) {
            int val = s[i] - '0';

            // Condition to find a digit that is
            // multiple of 2 other than one zero
            if (val % 2 == 0 && i != index_of_zero)
                multiple_of_2 = true;
        }

        // Condition if multiple of 2
        // do not exist
        if (multiple_of_2 == false) {
            Console.WriteLine("-1");
            return;
        }

        int last_val = s[(s.Length - 1)- '0'];
        int second_last_val = s[(s.Length - 2)- '0'];

        // Condition for zero swaps
        // means the number is already
        // is divisible by 60
        if (last_val == 0&& second_last_val % 2 == 0)
           Console.WriteLine(0);

        // Condition for only one swap
        else if ((last_val == 0
                  && second_last_val % 2 != 0)
                 || (last_val % 2 == 0
                     && second_last_val == 0))
           Console.WriteLine(1);

        else if (more_zero == true
                 && (last_val == 0
                     && second_last_val % 2 != 0))
            Console.WriteLine(1) ;

        // Otherwise 2 swaps required
        else
            Console.WriteLine(2) ;
    }

    // Driver Code
    public static void Main (string[] args)
    {
        string N = "20";

        MinimumSwapOperations(N);

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript program to find minimum number
// of swap operations required

    // Function that prlet minimum number
    // of swap operations required
    function MinimumSwapOperations(s)
    {
        let zero_exist = false;
        let multiple_of_2 = false;
        let sum = 0;
        let index_of_zero = 0;
        let more_zero = false;

        for (let i = 0; i < s.length; i++) {
            let val = s[i] - '0';

            // Condition if more than one
            // zero exist
            if (zero_exist == true)
                more_zero = true;

            // Condition if zero_exist
            if (val == 0) {
                zero_exist = true;
                index_of_zero = i;
            }

            // Computing total sum of all digits
            sum += val;
        }

        // Condition if zero does not exist or
        // the sum is not divisible by 3
        if (zero_exist == false || sum % 3 != 0) {
            document.write("-1");
            return;
        }

        for (let i = 0; i < s.length; i++) {
            let val = s[i] - '0';

            // Condition to find a digit that is
            // multiple of 2 other than one zero
            if (val % 2 == 0 && i != index_of_zero)
                multiple_of_2 = true;
        }

        // Condition if multiple of 2
        // do not exist
        if (multiple_of_2 == false) {
            document.write("-1");
            return;
        }

        let last_val = s.charAt[s.length - 1] - '0';
        let second_last_val = s[(s.length - 2)]- '0';

        // Condition for zero swaps
        // means the number is already
        // is divisible by 60
        if (last_val == 0&& second_last_val % 2 == 0)
            document.write(0);

        // Condition for only one swap
        else if ((last_val == 0
                  && second_last_val % 2 != 0)
                 || (last_val % 2 == 0
                     && second_last_val == 0))
            document.write(1);

        else if (more_zero == true
                 && (last_val == 0
                     && second_last_val % 2 != 0))
            document.write(1) ;

        // Otherwise 2 swaps required
        else
            document.write(2) ;
    }

// Driver Code

    let N = "20";

    MinimumSwapOperations(N);

</script>
```

**Output:** 

```
-1
```

***时间复杂度:** O(N)*

***辅助空间:**O(1)*T4】