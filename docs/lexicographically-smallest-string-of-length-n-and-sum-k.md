# 字典上最小的长度为 N 和 K 的字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最小长度字符串 n-and-sum-k/](https://www.geeksforgeeks.org/lexicographically-smallest-string-of-length-n-and-sum-k/)

给定两个整数 **N** 和 **K** 。任务是打印字典上最小长度的字符串 **N** 由小写英文字母组成，这样字符串中字符的总和等于 **K** ，其中**“a”= 1，“b”= 2，“c”= 3，…..和' z' = 26** 。
**举例:**

> **输入:** N = 5，K = 42
> **输出:**aaamz
> “aaany”“babmx”“aablz”等。也是有效字符串
> 但是“aaamz”是字典上最小的。
> **输入:** N = 3，K = 25
> **输出:** aaw

**进场:**

*   初始化大小为 **N** 的字符数组，并用 **'a'** 填充所有元素。
*   如果 **K ≥ 26** ，则从数组末尾开始遍历，并用 **'z'** 替换数组元素，或者用具有 ASCII 值的字符**(K+97–1)**替换。
*   同时将 **K** 的值减少为被替换的元素值，即 **a = 1** ， **b = 2** ， **c = 3** ，…， **z = 26** 。
*   此外，请注意，我们在当前元素之前减去先前的元素值(即总“a”)，并在 for 循环结束之前加上相同的值。
*   检查 **K < 0** 状态，断开 for 循环。
*   返回由 char 数组的元素组成的新字符串作为答案。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the lexicographically
// smallest string of length n that
// satisfies the given condition
string lexo_small(int n, int k)
{
    string arr = "";

    for(int i = 0; i < n; i++)
        arr += 'a';

    // Iteration from the last position
    // in the array
    for (int i = n - 1; i >= 0; i--)
    {
        k -= i;

        // If k is a positive integer
        if (k >= 0)
        {

            // 'z' needs to be inserted
            if (k >= 26)
            {
                arr[i] = 'z';
                k -= 26;
            }

            // Add the required character
            else
            {
                char c= (char)(k + 97 - 1);
                arr[i] = c;
                k -= arr[i] - 'a' + 1;
            }
        }

        else
            break;

        k += i;
    }
    return arr;
}

// Driver code
int main()
{
    int n = 5, k = 42;

    string arr = lexo_small(n, k);

    cout << arr;
}

// This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

public class Main {

    // Function to return the lexicographically
    // smallest string of length n that
    // satisfies the given condition
    public static char[] lexo_small(int n, int k)
    {
        char arr[] = new char[n];

        Arrays.fill(arr, 'a');

        // Iteration from the last position
        // in the array
        for (int i = n - 1; i >= 0; i--) {

            k -= i;

            // If k is a positive integer
            if (k >= 0) {

                // 'z' needs to be inserted
                if (k >= 26) {
                    arr[i] = 'z';
                    k -= 26;
                }

                // Add the required character
                else {
                    arr[i] = (char)(k + 97 - 1);
                    k -= arr[i] - 'a' + 1;
                }
            }

            else
                break;

            k += i;
        }

        return arr;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5, k = 42;

        char arr[] = lexo_small(n, k);

        System.out.print(new String(arr));
    }
}
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the lexicographically
# smallest string of length n that
# satisfies the given condition
def lexo_small(n, k):

    arr = "";

    for i in range(n):
        arr += 'a';

    # Iteration from the last position
    # in the array
    for i in range(n-1,-1,-1):
        k -= i;

        # If k is a positive integer
        if (k >= 0):

            # 'z' needs to be inserted
            if (k >= 26):
                arr = arr[:i] + 'z' + arr[i+1:];
                k -= 26;

            # Add the required character
            else:
                c= (k + 97 - 1);
                arr = arr[:i] + chr(c) + arr[i+1:];
                k -= ord(arr[i]) - ord('a') + 1;

        else:
            break;

        k += i;
    return arr;

# Driver code
if __name__ == '__main__':
    n = 5; k = 42;

    arr = lexo_small(n, k);

    print(arr);

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the lexicographically
    // smallest string of length n that
    // satisfies the given condition
    public static char[] lexo_small(int n, int k)
    {
        char []arr = new char[n];
        int i;

        for(i = 0; i < n; i++)
            arr[i] = 'a' ;

        // Iteration from the last position
        // in the array
        for (i = n - 1; i >= 0; i--)
        {
            k -= i;

            // If k is a positive integer
            if (k >= 0)
            {

                // 'z' needs to be inserted
                if (k >= 26)
                {
                    arr[i] = 'z';
                    k -= 26;
                }

                // Add the required character
                else
                {
                    arr[i] = (char)(k + 97 - 1);
                    k -= arr[i] - 'a' + 1;
                }
            }

            else
                break;

            k += i;
        }
        return arr;
    }

    // Driver code
    public static void Main()
    {
        int n = 5, k = 42;

        char []arr = lexo_small(n, k);

        Console.WriteLine(new string(arr));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the lexicographically
// smallest string of length n that
// satisfies the given condition
function lexo_small(n , k)
{
    var arr = Array.from({length: n}, (_, i) => 'a');

    // Iteration from the last position
    // in the array
    for (var i = n - 1; i >= 0; i--) {

        k -= i;

        // If k is a positive integer
        if (k >= 0) {

            // 'z' needs to be inserted
            if (k >= 26) {
                arr[i] = 'z';
                k -= 26;
            }

            // Add the required character
            else {
                arr[i] = String.fromCharCode(k + 97 - 1);
                k -= arr[i] - 'a' + 1;
            }
        }

        else
            break;

        k += i;
    }

    return arr;
}

// Driver code
var n = 5, k = 42;

var arr = lexo_small(n, k);

document.write(arr.join(''));

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
aaamz
```