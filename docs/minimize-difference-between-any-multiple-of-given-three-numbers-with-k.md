# 用 K

最小化给定三个数的任意倍数之间的差值

> 原文:[https://www . geeksforgeeks . org/最小化给定三个数字的任意倍数与-k 之间的差异/](https://www.geeksforgeeks.org/minimize-difference-between-any-multiple-of-given-three-numbers-with-k/)

给定 4 个整数 **A** 、 **B** 、 **C** 和 **K** ，任务是找出 A、B 和 C 与 K 的任意**倍数**之间的**最小**差

**示例:**

> **输入** : A = 5，B = 4，C = 8，K = 9
> **输出** : 1
> **说明:**A、B、C 最接近大于 9 的倍数为 10。因此，最小差值为 10-9 = 1
> 
> **输入** : A = 6，B = 10，C = 9，K = 2
> **输出** : 4
> **说明:**A、B、C 大于 2 的最近倍数为 6。因此，最小差值为 6-2 = 4

**天真方法**:通过使用 for-loop 获取 A、B 和 C 的**下一个**倍数，通过跟踪刚刚大于 **K** 的**最近倍数**可以解决任务，按照以下步骤解决问题:

*   初始化 3 个布尔变量，比如 fa、fb 和 fc，表示 A、B 和 C 的倍数是否大于 **K**
*   开始将 A、B 和 C 与初始化为 1 的**曲线**相乘
*   一旦三个数字中的一个大于 **K** ，相应地存储最近倍数和 K 之间的差值

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the difference between
// closest multiple of A, B, C with K
void solve(int A, int B, int C, int K)
{

    // Stores the minimum difference
    int ans = INT_MAX;

    // Check whether multiples of A, B and C becomes
    // greater than K
    bool fa = false, fb = false, fc = false;

    // Start multiplication from 1
    int cur = 1;
    while (1) {

        // Finding multiples
        A *= cur;
        B *= cur;
        C *= cur;

        // All the multiples becomes
        // greater than K
        if (fa && fb && fb)
            break;

        // Multiple of A
        if (!fa) {

            // Valid multiple
            if (A >= K) {

                // Minimize ans
                ans = min(ans, A - K);
                fa = true;
            }
        }

        // Multiple of B
        if (!fb) {

            // Valid multiple
            if (B >= K) {

                // Minimize ans
                ans = min(ans, B - K);
                fb = true;
            }
        }

        // Multiple of C
        if (!fc) {

            // Valid multiple
            if (C >= K) {

                // Minimize ans
                ans = min(ans, C - K);
                fc = true;
            }
        }

        cur++;
    }

    // Resultant answer
    cout << ans << endl;
}

// Driver Code
int main()
{
    int A = 6, B = 10, C = 9, K = 2;
    solve(A, B, C, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the difference between
// closest multiple of A, B, C with K
static void solve(int A, int B, int C, int K)
{

    // Stores the minimum difference
    int ans = Integer.MAX_VALUE;

    // Check whether multiples of A, B and C becomes
    // greater than K
    boolean fa = false, fb = false, fc = false;

    // Start multiplication from 1
    int cur = 1;
    while (true) {

        // Finding multiples
        A *= cur;
        B *= cur;
        C *= cur;

        // All the multiples becomes
        // greater than K
        if (fa && fb && fb)
            break;

        // Multiple of A
        if (!fa) {

            // Valid multiple
            if (A >= K) {

                // Minimize ans
                ans = Math.min(ans, A - K);
                fa = true;
            }
        }

        // Multiple of B
        if (!fb) {

            // Valid multiple
            if (B >= K) {

                // Minimize ans
                ans = Math.min(ans, B - K);
                fb = true;
            }
        }

        // Multiple of C
        if (!fc) {

            // Valid multiple
            if (C >= K) {

                // Minimize ans
                ans = Math.min(ans, C - K);
                fc = true;
            }
        }

        cur++;
    }

    // Resultant answer
    System.out.print(ans +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int A = 6, B = 10, C = 9, K = 2;
    solve(A, B, C, K);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the difference between
# closest multiple of A, B, C with K
def solve(A, B, C, K):

    # Stores the minimum difference
    ans = 10 ** 9

    # Check whether multiples of A, B and C becomes
    # greater than K
    fa = False
    fb = False
    fc = False

    # Start multiplication from 1
    cur = 1
    while (1):

        # Finding multiples
        A *= cur
        B *= cur
        C *= cur

        # All the multiples becomes
        # greater than K
        if (fa and fb and fb):
            break

        # Multiple of A
        if (not fa):

            # Valid multiple
            if (A >= K):

                # Minimize ans
                ans = min(ans, A - K)
                fa = True

        # Multiple of B
        if (not fb):

            # Valid multiple
            if (B >= K):

                # Minimize ans
                ans = min(ans, B - K)
                fb = True

        # Multiple of C
        if (not fc):

            # Valid multiple
            if (C >= K):

                # Minimize ans
                ans = min(ans, C - K)
                fc = True

        cur += 1

    # Resultant answer
    print(ans)

# Driver Code
A = 6
B = 10
C = 9
K = 2
solve(A, B, C, K)

 # This code is contributed by saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

// Function to find the difference between
// closest multiple of A, B, C with K
static void solve(int A, int B, int C, int K)
{

    // Stores the minimum difference
    int ans = Int32.MaxValue;

    // Check whether multiples of A, B and C becomes
    // greater than K
    bool fa = false, fb = false, fc = false;

    // Start multiplication from 1
    int cur = 1;
    while (true) {

        // Finding multiples
        A *= cur;
        B *= cur;
        C *= cur;

        // All the multiples becomes
        // greater than K
        if (fa && fb && fb)
            break;

        // Multiple of A
        if (!fa) {

            // Valid multiple
            if (A >= K) {

                // Minimize ans
                ans = Math.Min(ans, A - K);
                fa = true;
            }
        }

        // Multiple of B
        if (!fb) {

            // Valid multiple
            if (B >= K) {

                // Minimize ans
                ans = Math.Min(ans, B - K);
                fb = true;
            }
        }

        // Multiple of C
        if (!fc) {

            // Valid multiple
            if (C >= K) {

                // Minimize ans
                ans = Math.Min(ans, C - K);
                fc = true;
            }
        }

        cur++;
    }

    // Resultant answer
    Console.Write(ans +"\n");
}

    // Driver Code
    public static void Main()
    {
        int A = 6, B = 10, C = 9, K = 2;
        solve(A, B, C, K);
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the difference between
        // closest multiple of A, B, C with K
        function solve(A, B, C, K) {

            // Stores the minimum difference
            let ans = Number.MAX_VALUE;

            // Check whether multiples of A, B and C becomes
            // greater than K
            let fa = false, fb = false, fc = false;

            // Start multiplication from 1
            let cur = 1;
            while (1) {

                // Finding multiples
                A *= cur;
                B *= cur;
                C *= cur;

                // All the multiples becomes
                // greater than K
                if (fa && fb && fb)
                    break;

                // Multiple of A
                if (!fa) {

                    // Valid multiple
                    if (A >= K) {

                        // Minimize ans
                        ans = Math.min(ans, A - K);
                        fa = true;
                    }
                }

                // Multiple of B
                if (!fb) {

                    // Valid multiple
                    if (B >= K) {

                        // Minimize ans
                        ans = Math.min(ans, B - K);
                        fb = true;
                    }
                }

                // Multiple of C
                if (!fc) {

                    // Valid multiple
                    if (C >= K) {

                        // Minimize ans
                        ans = Math.min(ans, C - K);
                        fc = true;
                    }
                }

                cur++;
            }

            // Resultant answer
            document.write(ans + '<br>');
        }

        // Driver Code

        let A = 6, B = 10, C = 9, K = 2;
        solve(A, B, C, K);

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
4
```

***时间复杂度*** : O(min(K/A，K/B，K/C))
***辅助空间*** : O(1)

**有效方法**:上述方法可以概括为一个公式: **min(⌈K/A⌉*A、⌈K/B⌉*B、⌈k/c⌉*c)k**。

*   **⌈K/A⌉*A** 给出的**的最近倍数**刚好大于 **K**
*   **⌈K/B⌉*B** 给出的 **B** 的最近倍数刚好大于 **K**
*   **⌈K/C⌉*C** 给出的 **C** 的最近倍数刚好大于 **K**
*   所有这些的最小值与 **K** 的差值给出了期望的结果

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the difference between
// closest multiple of A, B, C with K
void solve(int A, int B, int C, int K)
{
    // Stores the multiples of A, B, C
    // just greater than K
    int fa, fb, fc;

    // Multiple of A
    if ((K % A) != 0) {

        fa = ((K / A) + 1) * A;
    }
    else {
        fa = (K / A) * A;
    }

    // Multiple of B
    if ((K % B) != 0) {

        fb = ((K / B) + 1) * B;
    }
    else {
        fb = (K / B) * B;
    }

    // Multiple of C
    if ((K % C) != 0) {

        fc = ((K / C) + 1) * C;
    }
    else {
        fc = (K / C) * C;
    }

    // Store the resultant answer
    int ans;
    ans = min(fa - K, min(fc - K, fb - K));
    cout << ans << endl;
}

// Drive code
int main()
{
    int A = 6, B = 10, C = 9, K = 2;
    solve(A, B, C, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to find the difference between
    // closest multiple of A, B, C with K
    static void solve(int A, int B, int C, int K)
    {

        // Stores the multiples of A, B, C
        // just greater than K
        int fa, fb, fc;

        // Multiple of A
        if ((K % A) != 0) {

            fa = ((K / A) + 1) * A;
        }
        else {
            fa = (K / A) * A;
        }

        // Multiple of B
        if ((K % B) != 0) {

            fb = ((K / B) + 1) * B;
        }
        else {
            fb = (K / B) * B;
        }

        // Multiple of C
        if ((K % C) != 0) {

            fc = ((K / C) + 1) * C;
        }
        else {
            fc = (K / C) * C;
        }

        // Store the resultant answer
        int ans;
        ans = Math.min(fa - K, Math.min(fc - K, fb - K));
        System.out.println(ans);
    }

    // Drive code
    public static void main (String[] args)
    {
        int A = 6, B = 10, C = 9, K = 2;
        solve(A, B, C, K);
    }

}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the difference between
# closest multiple of A, B, C with K
def solve( A, B, C, K) :

    # Stores the multiples of A, B, C
    # just greater than K

    # Multiple of A
    if ((K % A) != 0) :
        fa = ((K // A) + 1) * A;
    else :
        fa = (K // A) * A;

    # Multiple of B
    if ((K % B) != 0) :

        fb = ((K // B) + 1) * B;

    else :
        fb = (K // B) * B;

    # Multiple of C
    if ((K % C) != 0) :

        fc = ((K // C) + 1) * C;
    else :
        fc = (K // C) * C;

    # Store the resultant answer
    ans = min(fa - K, min(fc - K, fb - K));

    print(ans);

# Drive code
if __name__ == "__main__" :

    A = 6; B = 10; C = 9; K = 2;
    solve(A, B, C, K);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    // Function to find the difference between
    // closest multiple of A, B, C with K
    static void solve(int A, int B, int C, int K)
    {

        // Stores the multiples of A, B, C
        // just greater than K
        int fa, fb, fc;

        // Multiple of A
        if ((K % A) != 0) {

            fa = ((K / A) + 1) * A;
        }
        else {
            fa = (K / A) * A;
        }

        // Multiple of B
        if ((K % B) != 0) {

            fb = ((K / B) + 1) * B;
        }
        else {
            fb = (K / B) * B;
        }

        // Multiple of C
        if ((K % C) != 0) {

            fc = ((K / C) + 1) * C;
        }
        else {
            fc = (K / C) * C;
        }

        // Store the resultant answer
        int ans;
        ans = Math.Min(fa - K, Math.Min(fc - K, fb - K));
        Console.WriteLine(ans);
    }

    // Drive code
    public static void Main(string[] args)
    {
        int A = 6, B = 10, C = 9, K = 2;
        solve(A, B, C, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the difference between
    // closest multiple of A, B, C with K
    function solve(A , B , C , K)
    {

        // Stores the multiples of A, B, C
        // just greater than K
        var fa, fb, fc;

        // Multiple of A
        if ((K % A) != 0) {

            fa = parseInt((K / A) + 1) * A;
        }
        else {
            fa = parseInt(K / A) * A;
        }

        // Multiple of B
        if ((K % B) != 0) {

            fb = parseInt((K / B) + 1) * B;
        }
        else {
            fb = parseInt(K / B) * B;
        }

        // Multiple of C
        if ((K % C) != 0) {

            fc = parseInt((K / C) + 1) * C;
        }
        else {
            fc = parseInt(K / C) * C;
        }

        // Store the resultant answer
        var ans;
        ans = Math.min(fa - K, Math.min(fc - K, fb - K));
        document.write(ans);
    }

// Drive code
var A = 6, B = 10, C = 9, K = 2;
solve(A, B, C, K);

// This code is contributed by 29AjayKumar
</script>
```

**Output**

```
4
```

***时间复杂度** :* O(1)
***辅助空间*** : O(1)