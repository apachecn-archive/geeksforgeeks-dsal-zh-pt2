# 通过反转任意长度的前缀使 N 均匀所需的最小操作

> 原文:[https://www . geeksforgeeks . org/最小操作-通过反转任意长度的前缀来制造 n 偶数/](https://www.geeksforgeeks.org/minimum-operations-required-to-make-n-even-by-reversing-prefix-of-any-length/)

给定一个整数 **N** ，任务是找到使 **N** 均匀所需的最小操作数，使得在一个操作中，任何长度的前缀都可以颠倒。如果无法使 **N** 为偶数打印 **-1。**

**示例:**

> **输入:** N = 376502
> **输出:** 0
> **解释:**
> **–N**已经可以被 2 整除，因此它是一个偶数，因此前缀互换的总数将为 0。
> 
> **输入:** N = 36543
> **输出:** 2
> **说明:**
> **–**N 不是偶数，所以要使其为偶数先交换长度为 2 的前缀。现在**N**= 63543
> **–**现在交换长度 5 的前缀和 **N** =34536。

**进场:**

可以有 2 种情况。

> *   **N** 是 **T5【安**偶号****
> *   **普通是一奇号**.****

**现在，**

*   **如果 **N** 是偶数，使 **N** 成为偶数的最小步数将为 0。**
*   **如果 **N** 是奇数，可以有 3 种情况。

    1.  **N** 不包含任何偶数。在这种情况下，不可能使 **N** 为偶数，因此答案为-1。
    2.  **N** 包含偶数位， **N** 的第一位是偶数。在这种情况下，我们可以交换整数，所以使 **N** 成为偶数的最小步数将是 1。
    3.  **N** 包含偶数位， **N** 的第一位不是偶数。在这种情况下，我们可以先交换前缀到任意偶数，然后交换整数，这样使 **N** 成为偶数的最小步数就是 2。** 

**按照以下步骤解决问题:**

*   **将字符串 **s[]** 初始化为 **N.** 的字符串表示**
*   **将变量**和**初始化为 **-1** ，将**变量**初始化为字符串**的长度。****
*   **如果**(s[len-1]–‘0’)% 2 = = 0**，则将**和**设置为 **0。****
*   **否则，执行以下任务:

    *   如果字符串 **s[]** 的第一个字符是**偶数**，则将 **ans** 设置为 **1。**
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，伦)**，并执行以下任务:
        *   如果**s【I】**为偶数，则将 **ans** 设置为 **2** 并断开。** 
*   **执行上述步骤后，打印**和**的值作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number
// of steps required to make N an even number
void MinSteps(int N)
{

    // Converting N into string
    string s = to_string(N);

    int ans = -1;

    // Number of digits in N
    int len = s.size();

    // If the number is even
    if ((s[len - 1] - '0') % 2 == 0) {
        ans = 0;
    }
    else {

        // If the first digit is even
        if ((s[0] - '0') % 2 == 0) {
            ans = 1;
        }
        else {

            // Cheaking if s contains
            // any even digits
            for (int i = 0; i < len; i++) {
                if ((s[i] - '0') % 2 == 0) {
                    ans = 2;
                    break;
                }
            }
        }
    }

    // Printing the minium number
    // of steps to make N an even number
    cout << ans << "\n";
}

// Driver Code
int main()
{
    int N;
    N = 36543;

    MinSteps(N);
}
```

## **java 描述语言**

```
<script>

// JavaScript code for the above approach

// Function to find minimum number
// of steps required to make N an even number
const MinSteps = (N) => {

    // Converting N into string
    let s = N.toString();

    let ans = -1;

    // Number of digits in N
    let len = s.length;

    // If the number is even
    if ((s.charCodeAt(len - 1) -
       '0'.charCodeAt(0)) % 2 == 0)
    {
        ans = 0;
    }
    else
    {

        // If the first digit is even
        if ((s.charCodeAt(0) -
           '0'.charCodeAt(0)) % 2 == 0)
        {
            ans = 1;
        }
        else
        {

            // Cheaking if s contains
            // any even digits
            for(let i = 0; i < len; i++)
            {
                if ((s.charCodeAt(i) -
                   '0'.charCodeAt(0)) % 2 == 0)
                {
                    ans = 2;
                    break;
                }
            }
        }
    }

    // Printing the minium number
    // of steps to make N an even number
    document.write(`${ans}<br/>`);
}

// Driver Code
let N = 36543;

MinSteps(N);

// This code is contributed by rakeshsahni

</script>
```

****Output**

```
2
```** 

*****时间复杂度:** O(len)，其中 len 是字符串的长度。*
***辅助空间:** O(镜头)***