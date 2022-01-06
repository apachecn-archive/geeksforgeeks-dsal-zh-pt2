# 一个范围内数组中数字的分布

> 原文:[https://www . geesforgeks . org/范围内数组中数字的分布/](https://www.geeksforgeeks.org/distribution-of-a-number-in-array-within-a-range/)

给定整数 **S** 、 **N** 、 **K** 、 **L** 和 **R** ，其中 **S** 必须分布在大小为 **N** 的数组中，使得每个元素必须来自范围**【L，R】**，并且数组中 **K** 个元素的总和应大于剩余 **N 的总和**

**示例:**

> **输入:** N = 5，K = 3，L = 1，R = 3，S = 13，S<sub>K</sub>= 9
> T5】输出:3 3 2
> 
> **输入:** N = 5，K = 3，L = 1，R = 3，S = 15，S<sub>K</sub>= 9
> T5】输出:3 3 3 3 3 3 3

**方法:**如果 S <sub>k</sub> 可以平均分配到 k 个元素中，那么将 S <sub>k</sub> /k 存储到数组的所有前 k 个元素中，否则数组的第一个元素将是(S <sub>k</sub> /k) + (S <sub>k</sub> % k)，剩下的 k–1 个元素将是(S<sub>k</sub>–S<sub>k</sub>% k)% k–1。同样，将 S-S <sub>k</sub> 分配到 n-k 元素中。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function for the distribution of the number
void distribution(int n, int k, int l,
                  int r, int S, int Sk)
{
    int a[n];
    int len = k, temp, rem, s;
    int diff = S - Sk;
    for (int i = 0; i < len; i++) {
        // Distribute the number
        // among k elements
        temp = Sk / k;
        rem = Sk % k;
        if (temp + rem >= l && temp + rem <= r) {
            a[i] = temp;
        }
        else if (temp + rem > r) {
            a[i] = r;
        }
        else if (temp + rem < r) {
            cout << "-1";
            return;
        }
        Sk = Sk - a[i];
        k = k - 1;
    }

    // If there is some remaining
    // sum to distribute
    if (Sk > 0) {
        cout << "-1";
        return;
    }

    // If there are elements remaining
    // to distribute i.e. (n - k)
    if (len) {
        k = n - len;
        for (int i = len; i < n; i++) {
            // Divide the remaining sum into
            // n-k elements
            temp = diff / k;
            rem = diff % k;
            if (temp + rem >= l && temp + rem <= r) {
                a[i] = temp;
            }
            else if (temp + rem > r) {
                a[i] = r;
            }
            else if (temp + rem < r) {
                cout << "-1";
                return;
            }
            diff = diff - a[i];
            k = k - 1;
        }
        if (diff) {
            cout << "-1";
            return;
        }
    }

    // Print the distribution
    for (int i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
}

// Driver code
int main()
{
    int n = 5, k = 3, l = 1,
        r = 5, S = 13, Sk = 9;

    distribution(n, k, l, r, S, Sk);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function for the distribution of the number
    static void distribution(int n, int k, int l,
                            int r, int S, int Sk)
    {
        int a[] = new int[n];
        int len = k, temp, rem, s;
        int diff = S - Sk;

        for (int i = 0; i < len; i++)
        {

            // Distribute the number
            // among k elements
            temp = Sk / k;
            rem = Sk % k;
            if (temp + rem >= l && temp + rem <= r)
            {
                a[i] = temp;
            }
            else if (temp + rem > r)
            {
                a[i] = r;
            }
            else if (temp + rem < r)
            {
                System.out.print("-1");
                return;
            }
            Sk = Sk - a[i];
            k = k - 1;
        }

        // If there is some remaining
        // sum to distribute
        if (Sk > 0)
        {
            System.out.print("-1");
            return;
        }

        // If there are elements remaining
        // to distribute i.e. (n - k)
        if (len != 0)
        {
            k = n - len;
            for (int i = len; i < n; i++)
            {

                // Divide the remaining sum into
                // n-k elements
                temp = diff / k;
                rem = diff % k;
                if (temp + rem >= l && temp + rem <= r)
                {
                    a[i] = temp;
                }
                else if (temp + rem > r)
                {
                    a[i] = r;
                }
                else if (temp + rem < r)
                {
                    System.out.print("-1");
                    return;
                }
                diff = diff - a[i];
                k = k - 1;
            }
            if (diff != 0)
            {
                System.out.print("-1");
                return;
            }
        }

        // Print the distribution
        for (int i = 0; i < n; i++)
        {
            System.out.print(a[i] + " ");
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5, k = 3, l = 1,
            r = 5, S = 13, Sk = 9;

        distribution(n, k, l, r, S, Sk);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function for the distribution of the number
def distribution(n, k, l, r, S, Sk):
    a = [0] * n;
    len = k;
    temp, rem, s = 0, 0, 0;
    diff = S - Sk;

    for i in range(len):

        # Distribute the number
        # among k elements
        temp = Sk / k;
        rem = Sk % k;
        if (temp + rem >= l and temp + rem <= r):
            a[i] = temp;
        elif(temp + rem > r):
            a[i] = r;
        elif(temp + rem < r):
            print("-1");
            return;

        Sk = Sk - a[i];
        k = k - 1;

    # If there is some remaining
    # sum to distribute
    if (Sk > 0):
        print("-1");
        return;

    # If there are elements remaining
    # to distribute i.e. (n - k)
    if (len != 0):
        k = n - len;
        for i in range(len, n):

            # Divide the remaining sum into
            # n-k elements
            temp = diff / k;
            rem = diff % k;
            if (temp + rem >= l and temp + rem <= r):
                a[i] = temp;
            elif(temp + rem > r):
                a[i] = r;
            elif(temp + rem < r):
                print("-1");
                return;

            diff = diff - a[i];
            k = k - 1;

        if (diff != 0):
            print("-1");
            return;

    # Print the distribution
    for i in range(n):
        print(int(a[i]), end=" ");

# Driver code
if __name__ == '__main__':
    n, k, l, r, S, Sk = 5, 3, 1, 5, 13, 9;

    distribution(n, k, l, r, S, Sk);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function for the distribution of the number
    static void distribution(int n, int k, int l,
                            int r, int S, int Sk)
    {
        int []a = new int[n];
        int len = k, temp, rem;
        int diff = S - Sk;

        for (int i = 0; i < len; i++)
        {

            // Distribute the number
            // among k elements
            temp = Sk / k;
            rem = Sk % k;
            if (temp + rem >= l && temp + rem <= r)
            {
                a[i] = temp;
            }
            else if (temp + rem > r)
            {
                a[i] = r;
            }
            else if (temp + rem < r)
            {
                Console.Write("-1");
                return;
            }
            Sk = Sk - a[i];
            k = k - 1;
        }

        // If there is some remaining
        // sum to distribute
        if (Sk > 0)
        {
            Console.Write("-1");
            return;
        }

        // If there are elements remaining
        // to distribute i.e. (n - k)
        if (len != 0)
        {
            k = n - len;
            for (int i = len; i < n; i++)
            {

                // Divide the remaining sum into
                // n-k elements
                temp = diff / k;
                rem = diff % k;
                if (temp + rem >= l && temp + rem <= r)
                {
                    a[i] = temp;
                }
                else if (temp + rem > r)
                {
                    a[i] = r;
                }
                else if (temp + rem < r)
                {
                    Console.Write("-1");
                    return;
                }
                diff = diff - a[i];
                k = k - 1;
            }
            if (diff != 0)
            {
                Console.Write("-1");
                return;
            }
        }

        // Print the distribution
        for (int i = 0; i < n; i++)
        {
            Console.Write(a[i] + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 5, k = 3, l = 1,
            r = 5, S = 13, Sk = 9;

        distribution(n, k, l, r, S, Sk);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function for the distribution of the number
function distribution(n, k, l, r, S, Sk)
{
    let a = new Array(n);
    let len = k, temp, rem, s;
    let diff = S - Sk;
    for (let i = 0; i < len; i++) {
        // Distribute the number
        // among k elements
        temp = Sk / k;
        rem = Sk % k;
        if (temp + rem >= l && temp + rem <= r) {
            a[i] = temp;
        }
        else if (temp + rem > r) {
            a[i] = r;
        }
        else if (temp + rem < r) {
            document.write("-1");
            return;
        }
        Sk = Sk - a[i];
        k = k - 1;
    }

    // If there is some remaining
    // sum to distribute
    if (Sk > 0) {
        document.write("-1");
        return;
    }

    // If there are elements remaining
    // to distribute i.e. (n - k)
    if (len) {
        k = n - len;
        for (let i = len; i < n; i++) {
            // Divide the remaining sum into
            // n-k elements
            temp = diff / k;
            rem = diff % k;
            if (temp + rem >= l && temp + rem <= r) {
                a[i] = temp;
            }
            else if (temp + rem > r) {
                a[i] = r;
            }
            else if (temp + rem < r) {
                document.write("-1");
                return;
            }
            diff = diff - a[i];
            k = k - 1;
        }
        if (diff) {
            document.write("-1");
            return;
        }
    }

    // Print the distribution
    for (let i = 0; i < n; i++) {
        document.write(a[i] + " ");
    }
}

// Driver code

let n = 5, k = 3, l = 1, r = 5, S = 13, Sk = 9;

distribution(n, k, l, r, S, Sk);
</script>
```

**Output:** 

```
3 3 3 2 2
```