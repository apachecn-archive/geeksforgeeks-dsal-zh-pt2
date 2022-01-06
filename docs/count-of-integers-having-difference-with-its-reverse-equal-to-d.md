# 倒数等于 D 的整数计数

> 原文:[https://www . geeksforgeeks . org/与其反向等于 d 的整数计数/](https://www.geeksforgeeks.org/count-of-integers-having-difference-with-its-reverse-equal-to-d/)

给定一个整数 **D** ，任务是找出所有可能的正整数 **N** 的个数，使得[T5】反向(N)](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/)T8】= N+D。

**示例:**

> **输入:** D = 63
> **输出:** 2
> **说明:**
> 对于 N = 18，18 + 63 = 81，满足条件 N + D =反转(N)。
> 对于 N = 29，29 + 63 = 92，满足条件 N + D =反(N)。
> 因此，要求的输出为 2
> 
> **输入:**D = 75
> T3】输出: 0

**方法:**根据以下观察结果可以解决问题:

> N + D =倒档(N)= > N–倒档(N) = D
> = > D = ∑ <sub>(i=0 至【L/2】-1)</sub>(10<sup>L-1-I</sup>-10<sup>I</sup>)*(N<sub>I</sub>–N<sub>L-1-I</sub>，L = N 位数。
> 
> 如果 d<sub>I</sub>= n<sub>【I】</sub>—n<sub>-l-1-I</sub>(0≤I≤l/2-【1】
> 【反向】-【n】<sub>(I = 0to)</sub>

按照以下步骤解决问题:

*   让 **f(L，D) =反向(N)N**。找到满足给定公式的 **N** 的个数，几乎相当于在**【9，9】****{ d<sub>0</sub>，d <sub>1</sub> 的范围内枚举 L 对和一个整数序列。。。，d <sub>⌊L/2⌋−1</sub> }** (不过要考虑到对应于 d <sub>i</sub> 序列的 n 不止一个)。在此，对于任何 **i** 使得**0≤I<⌊l/2⌋1**的情况，以下情况成立:

> 10<sup>l-1-I</sup>—10<sup>【I】</sup>><sub>(j = I+1 to[l/2–1])</sub>(10<sup>【l-1】-j</sup>-

*   设**L<sub>D</sub>T3】为十进制记数法中 **D** 的位数。然后，当**L>2L<sub>D</sub>T9】和 **f(L，d) > 0** 时，可以看出 **f(L，d) > D** 。****
*   因此，将**L<sub>D</sub>T3**2L<sub>D</sub>T7】之间的值考虑为 **L** 的值就足够了。****
*   对于 **L** 的固定值，考虑枚举序列 **{ d <sub>0</sub> 、d <sub>1</sub> 、…、d <sub>⌊L/2⌋−1</sub> }** ，使得 **f(L，d) = D** (并且找到满足给定公式的 n 的计数)，通过从 **d <sub>0</sub>** 开始执行深度优先搜索。
*   当到**d<sub>I-1</sub>**的值已经决定时，可以看出最多有两个候选的**d<sub>I</sub>T7】值需要考虑:最大值为**(10<sup>I</sup>10<sup>L-1 I</sup>)d<sub>I</sub>≤dif**，最小值为**((直观来看，如果搜索时 **f(L，d)** 的“中途”值离 **D** 太远，就不可能“回退”，因而应该“待近”到 **D** 。)****
*   因此，对于 **L** 的固定值，求 **O(2 <sup>⌊L/2⌋</sup> )** 时间中满足给定公式的 **N** 的计数。

下面是上述方法的实现:

## C++

```
// Cpp program for the
// above approach
#include <bits/stdc++.h>

using namespace std;

// Maximum digits in N
int MAXL = 17;
int N;
vector<int> v;

// Function to find count
// of possible values
// of N such that N + D = reverse(N)
int count(int D, int l, int t, int x[])
{

    // Base Case
    if (t == N) {

        // If D is not qual to 0
        if (D != 0)
            return 0;

        // Stores count of possible values
        // of N such that N + D = reverse(N)
        long ans = 1;

        for (int i = 0; i < N; i++) {

            // Update ans
            ans *= (i == 0 ? 9 : 10) - abs(x[i]);
        }

        // If l is even
        if (l % 2 == 0) {

            // Update ans
            ans *= 10;
        }

        return ans;
    }

    // Stores count of possible values
    // of N such that N + D = reverse(N)
    long ans = 0;

    // Iterae over the range [-9, 9]
    for (int m = -9; m <= 9; m++) {

        if (-v[t] < D + v[t] * m && D +
                      v[t] * m < v[t]) {

            x[t] = m;

            // Update ans
            ans += count(D + v[t] * m, l,
                                 t + 1, x);
        }
    }

    return ans;
}

// Utility function to find count of N
// such that N + D = reverse(N)
int findN(int D)
{

    // If d is a multiple of 9,
    // no such value N found
    if (D % 9 != 0)
        return 0;

    // Divide D by 9 check reverse
    // of number and its sum
    D /= 9;

    // B[i]: Stores power of (10, i)
    vector<int> B(MAXL);
    B[0] = 1;

    // Calculate power(10, i)
    for (int i = 1; i < MAXL; i++) {

        // Update B[i]
        B[i] = B[i - 1] * 10;
    }

    // Stores count of N such
    // that N + D = reverse(N)
    int ans = 0;

    // Iterate over the range [1, MAXL]
    for (int i = 1; i <= MAXL; i++) {

        N = (i + 1) / 2;
        v.clear();
        v.resize(N);
        for (int j = 0; j < N; j++)
            for (int k = j; k < i - j; k++)
                v[j] += B[k];

        int arr[N];
        ans += count(D, i, 0, arr);
    }

    return ans;
}

// Driver Code
int main()
{
    int D = 63;

    // Function call
    cout << findN(D);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

public class Main {

    // Maximum digits in N
    static final int MAXL = 17;
    static int N;
    static long[] v;

    // Utility function to find count of N
    // such that N + D = reverse(N)
    static long findN(int D)
    {

        // If d is a multiple of 9,
        // no such value N found
        if (D % 9 != 0)
            return 0;

        // Divide D by 9 check reverse
        // of number and its sum
        D /= 9;

        // B[i]: Stores power of (10, i)
        long[] B = new long[MAXL];
        B[0] = 1;

        // Calculate power(10, i)
        for (int i = 1; i < MAXL; i++) {

            // Update B[i]
            B[i] = B[i - 1] * 10;
        }

        // Stores count of N such
        // that N + D = reverse(N)
        long ans = 0;

        // Iterate over the range [1, MAXL]
        for (int i = 1; i <= MAXL; i++) {

            N = (i + 1) / 2;
            v = new long[N];
            for (int j = 0; j < N; j++)
                for (int k = j; k < i - j; k++)
                    v[j] += B[k];

            // Update ans
            ans += count(D, i, 0, new int[N]);
        }

        return ans;
    }

    // Function to find count of possible values
    // of N such that N + D = reverse(N)
    static long count(long D, int l,
                      int t, int[] x)
    {

        // Base Case
        if (t == N) {

            // If D is not qual to 0
            if (D != 0)
                return 0;

            // Stores count of possible values
            // of N such that N + D = reverse(N)
            long ans = 1;

            for (int i = 0; i < N; i++) {

                // Update ans
                ans *= (i == 0 ? 9 : 10)
                       - Math.abs(x[i]);
            }

            // If l is even
            if (l % 2 == 0) {

                // Update ans
                ans *= 10;
            }

            return ans;
        }

        // Stores count of possible values
        // of N such that N + D = reverse(N)
        long ans = 0;

        // Iterae over the range [-9, 9]
        for (int m = -9; m <= 9; m++) {

            if (-v[t] < D + v[t] * m
                && D + v[t] * m < v[t]) {

                x[t] = m;

                // Update ans
                ans += count(D + v[t] * m,
                             l, t + 1, x);
            }
        }

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);
        int D = 63;

        // Function call
        System.out.println(findN(D));

        sc.close();
    }
}
```

## 蟒蛇 3

```
# Python program of the above approach

# Maximum digits in N
MAXL = 17;
N = 0;
v = 0;

# Utility function to find count of N
# such that N + D = reverse(N)
def findN(D):
    global N;
    global v;

    # If d is a multiple of 9,
    # no such value N found
    if (D % 9 != 0):
        return 0;

    # Divide D by 9 check reverse
    # of number and its sum
    D //= 9;

    # B[i]: Stores power of (10, i)
    B = [0]*MAXL;
    B[0] = 1;

    # Calculate power(10, i)
    for i in range(1, MAXL):

        # Update B[i]
        B[i] = B[i - 1] * 10;

    # Stores count of N such
    # that N + D = reverse(N)
    ans = 0;

    # Iterate over the range [1, MAXL]
    for i in range(1, MAXL + 1):
        N = (i + 1) // 2;
        v = [0]*N;
        for j in range(N):
            for k in range(j, i - j):
                v[j] += B[k];

        # Update ans
        temp = [0]*N;
        ans += count(D, i, 0, temp);
        return ans;

# Function to find count of possible values
# of N such that N + D = reverse(N)
def count(D, l, t, x):
    global N;
    global v;

    # Base Case
    if (t == N):

        # If D is not qual to 0
        if (D != 0):
            return 0;

        # Stores count of possible values
        # of N such that N + D = reverse(N)
        ans = 1;
        for i in range(N):

            # Update ans
            ans *= (9 if i == 0 else 10) - abs(x[i]);

        # If l is even
        if (l % 2 == 0):

            # Update ans
            ans *= 10;
        return ans;

    # Stores count of possible values
    # of N such that N + D = reverse(N)
    ans = 0;

    # Iterae over the range [-9, 9]
    for m in range(-9, 10):
        if (-v[t] < D + v[t] * m and D + v[t] * m < v[t]):
            x[t] = m;

            # Update ans
            ans += count(D + v[t] * m, l, t + 1, x);
    return ans;

# Driver Code
if __name__ == '__main__':
    D = 63;

    # Function call
    print(findN(D));

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Maximum digits in N
    static int MAXL = 17;
    static int N;
    static long[] v;

    // Utility function to find count of N
    // such that N + D = reverse(N)
    static long findN(int D)
    {

        // If d is a multiple of 9,
        // no such value N found
        if (D % 9 != 0)
            return 0;

        // Divide D by 9 check reverse
        // of number and its sum
        D /= 9;

        // B[i]: Stores power of (10, i)
        long[] B = new long[MAXL];
        B[0] = 1;

        // Calculate power(10, i)
        for (int i = 1; i < MAXL; i++)
        {

            // Update B[i]
            B[i] = B[i - 1] * 10;
        }

        // Stores count of N such
        // that N + D = reverse(N)
        long ans = 0;

        // Iterate over the range [1, MAXL]
        for (int i = 1; i <= MAXL; i++)
        {
            N = (i + 1) / 2;
            v = new long[N];
            for (int j = 0; j < N; j++)
                for (int k = j; k < i - j; k++)
                    v[j] += B[k];

            // Update ans
            ans += count(D, i, 0, new int[N]);
        }
        return ans;
    }

    // Function to find count of possible values
    // of N such that N + D = reverse(N)
    static long count(long D, int l,
                      int t, int[] x)
    {

        // Base Case
        if (t == N)
        {

            // If D is not qual to 0
            if (D != 0)
                return 0;

            // Stores count of possible values
            // of N such that N + D = reverse(N)
            long ans = 1;
            for (int i = 0; i < N; i++)
            {

                // Update ans
                ans *= (i == 0 ? 9 : 10)
                       - Math.Abs(x[i]);
            }

            // If l is even
            if (l % 2 == 0)
            {

                // Update ans
                ans *= 10;
            }
            return ans;
        }

        // Stores count of possible values
        // of N such that N + D = reverse(N)
        long anss = 0;

        // Iterae over the range [-9, 9]
        for (int m = -9; m <= 9; m++)
        {
            if (-v[t] < D + v[t] * m
                && D + v[t] * m < v[t])
            {
                x[t] = m;

                // Update ans
                anss += count(D + v[t] * m,
                             l, t + 1, x);
            }
        }
        return anss;
    }

  // Driver code
  public static void Main(String[] args)
  {
        int D = 63;

        // Function call
        Console.WriteLine(findN(D));
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
// javascript program of the above approach

    // Maximum digits in N
    let MAXL = 17;
    let N;
    let v = []

    // Utility function to find count of N
    // such that N + D = reverse(N)
    function findN(D)
    {

        // If d is a multiple of 9,
        // no such value N found
        if (D % 9 != 0)
            return 0;

        // Divide D by 9 check reverse
        // of number and its sum
        D /= 9;

        // B[i]: Stores power of (10, i)
        let B = new Array(MAXL).fill(0); 

        B[0] = 1;

        // Calculate power(10, i)
        for (let i = 1; i < MAXL; i++) {

            // Update B[i]
            B[i] = B[i - 1] * 10;
        }

        // Stores count of N such
        // that N + D = reverse(N)
        let ans = 0;

        // Iterate over the range [1, MAXL]
        for (let i = 1; i <= MAXL; i++) {

            N = Math.floor((i + 1) / 2);
            v = new Array(N).fill(0);
            for (let j = 0; j < N; j++)
                for (let k = j; k < i - j; k++)
                    v[j] += B[k];

            // Update ans
            ans += count(D, i, 0, new Array(N));
        }

        return ans;
    }

    // Function to find count of possible values
    // of N such that N + D = reverse(N)
    function count(D, l, t, x)
    {

        // Base Case
        if (t == N) {

            // If D is not qual to 0
            if (D != 0)
                return 0;

            // Stores count of possible values
            // of N such that N + D = reverse(N)
            let ans = 1;

            for (let i = 0; i < N; i++) {

                // Update ans
                ans *= (i == 0 ? 9 : 10)
                       - Math.abs(x[i]);
            }

            // If l is even
            if (l % 2 == 0) {

                // Update ans
                ans *= 10;
            }

            return ans;
        }

        // Stores count of possible values
        // of N such that N + D = reverse(N)
        let ans = 0;

        // Iterae over the range [-9, 9]
        for (let m = -9; m <= 9; m++)
        {

            if (-v[t] < D + v[t] * m
                && D + v[t] * m < v[t])
            {

                x[t] = m;

                // Update ans
                ans += count(D + v[t] * m,
                             l, t + 1, x);
            }
        }

        return ans;
    }

    // Driver Code
        let D = 63;

        // Function call
        document.write(findN(D));

 // This code is contributed by target_2.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(2<sup>L</sup>T5<sup>D</sup>T8】，其中 L <sub>D</sub> 表示十进制记数法中 D 的位数。*
***辅助空间:** O( L <sub>D</sub> )*