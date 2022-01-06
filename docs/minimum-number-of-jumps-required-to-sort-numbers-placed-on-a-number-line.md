# 对数字行上的数字进行排序所需的最小跳转次数

> 原文:[https://www . geesforgeks . org/最小跳转次数-需要对数字进行排序-放在数字线上/](https://www.geeksforgeeks.org/minimum-number-of-jumps-required-to-sort-numbers-placed-on-a-number-line/)

给定两个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **W[]** 和 **L[]** ，其中 **W[i]** 最初位于无限数线上的位置 **i** 。在每次向前跳跃中， **W[i]** 可以从其当前位置 **j** 跳到位置 **(j + L[i])** 到任意空位。任务是找到[排序数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)所需的最小前跳次数。

**示例:**

> **输入:** W[] = {2，1，4，3}，L[] = {4，1，2，4}
> **输出:** 5
> **解释:**
> 最初，2 在位置 0，1 在位置 1，4 在位置 2，3 在数字线上的位置 3 作为:2 1 4 3
> 推动数字 2 从其当前位置 0 跳到位置 4， 号码线上的排列:_ 1 4 3 2
> 按 3 号键从当前位置 3 跳到位置 7，号码线上的排列:_ 1 4 2 _ _ 3
> 按 4 号键从当前位置 2 跳到位置 8，号码线上的排列:_ 1 _ _ 2 _ _ 3 4
> 
> 因此，所需的跳跃总数为 1 + 1 + 3 = 5。
> 
> **输入:** W[] = {3，1，2}，L[] = {1，4，5 }
> T3】输出: 3

**方法:**给定的问题可以通过使用**贪婪方法**来解决，方法是最小化数组中[最小元素所需的跳转次数，该元素在每次操作中没有正确定位，并更新跳转次数。按照以下步骤解决问题:](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)

**方法:**给定的问题可以通过使用**贪婪方法**来解决，方法是最小化数组中[最小元素所需的跳转次数，该元素在每次操作中没有正确定位，并更新跳转次数。按照以下步骤解决问题:](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)

*   初始化一个变量，将**和**设为 **0** 来存储所需的最小跳跃次数。
*   [创建数组副本](https://www.geeksforgeeks.org/program-to-copy-the-contents-of-one-array-into-another-in-the-reverse-order/) **W[]** 和[将元素按排序顺序存储在数组](https://www.geeksforgeeks.org/sort-c-stl/) **arr[]** 中。
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **pos** ，存储元素**W【I】**的当前位置。
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **W[]** ，更新 **pos** 中 **W[i]** 的位置。
*   [在**【1，N–1】**范围内遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   将数组 **W[]** 中 **arr[i]** 的位置和**arr[I–1]**的位置存储在变量中，分别表示 **curr** 和 **prev** 。
    *   如果 **curr** 的值大于 **prev** ，则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)到下一次迭代。
    *   否则，迭代直到 **curr ≤ prev** 或 **curr** 已经被占用，并通过**跳转**增加 **curr** 的值，通过 **1** 增加**和**的值。
    *   将 HashMap **pos** 中**arr【I】**的位置更新为 **curr** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of jumps required to sort the array
void minJumps(int w[], int l[], int n)
{
    // Base Case
    if (n == 1) {
        cout << 0;
        return;
    }

    // Store the required result
    int ans = 0;

    // Stores the current position of
    // elements and their respective
    // maximum jump
    unordered_map<int, int> pos, jump;

    // Used to check if a position is
    // already taken by another element
    unordered_map<int, bool> filled;

    // Stores the sorted array a[]
    int a[n];

    // Traverse the array w[] & update
    // positions jumps array a[]
    for (int i = 0; i < n; i++) {

        pos[w[i]] = i;
        filled[i] = true;
        jump[w[i]] = l[i];
        a[i] = w[i];
    }

    // Sort the array a[]
    sort(a, a + n);

    // Traverse the array a[] over
    // the range [1, N-1]
    for (int curr = 1;
         curr < n; curr++) {

        // Store the index of current
        // element and its just smaller
        // element in array w[]
        int currElementPos
            = pos[a[curr]];
        int prevElementPos
            = pos[a[curr - 1]];

        if (currElementPos
            > prevElementPos)
            continue;

        // Iterate until current element
        // position is at most its just
        // smaller element position
        while (currElementPos
                   <= prevElementPos
               || filled[currElementPos]) {

            currElementPos += jump[a[curr]];
            ans++;
        }

        // Update the position of the
        // current element
        pos[a[curr]] = currElementPos;
        filled[currElementPos] = true;
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int W[] = { 2, 1, 4, 3 };
    int L[] = { 4, 1, 2, 4 };
    int N = sizeof(W) / sizeof(W[0]);
    minJumps(W, L, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

    // Function to find the minimum number
    // of jumps required to sort the array
    static void minJumps(int[] w, int[] l, int n)
    {

        // Base Case
        if (n == 1) {
            System.out.print(0);
            return;
        }

        // Store the required result
        int ans = 0;

        // Stores the current position of
        // elements and their respective
        // maximum jump
        HashMap<Integer, Integer> pos
            = new HashMap<Integer, Integer>();
        HashMap<Integer, Integer> jump
            = new HashMap<Integer, Integer>();

        // Used to check if a position is
        // already taken by another element
        HashMap<Integer, Boolean> filled
            = new HashMap<Integer, Boolean>();

        // Stores the sorted array a[]
        int[] a = new int[n];

        // Traverse the array w[] & update
        // positions jumps array a[]
        for (int i = 0; i < n; i++) {
            if (pos.containsKey(w[i]))
                pos.put(w[i], i);
            else
                pos.put(w[i], i);
            if (filled.containsKey(w[i]))
                filled.put(i, true);
            else
                filled.put(i, true);
            if (jump.containsKey(w[i]))
                jump.put(w[i], l[i]);
            else
                jump.put(w[i], l[i]);

            a[i] = w[i];
        }

        // Sort the array a[]
        Arrays.sort(a);

        // Traverse the array a[] over
        // the range [1, N-1]
        for (int curr = 1; curr < n; curr++) {

            // Store the index of current
            // element and its just smaller
            // element in array w[]
            int currElementPos = pos.get(a[curr]);
            int prevElementPos = pos.get(a[curr - 1]);

            if (currElementPos > prevElementPos)
                continue;

            // Iterate until current element
            // position is at most its just
            // smaller element position
            while (currElementPos <= prevElementPos
                   || filled.containsKey(currElementPos)
                          && filled.containsKey(
                              currElementPos)) {
                currElementPos += jump.get(a[curr]);
                ans++;
            }

            // Update the position of the
            // current element
            if (pos.containsKey(a[curr]))
                pos.put(a[curr], currElementPos);
            else
                pos.put(a[curr], currElementPos);
            if (filled.containsKey(currElementPos))
                filled.put(currElementPos, true);
            else
                filled.put(currElementPos, true);
        }

        // Print the result
        System.out.print(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] W = { 2, 1, 4, 3 };
        int[] L = { 4, 1, 2, 4 };
        int N = W.length;

        minJumps(W, L, N);
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of jumps required to sort the array
def minJumps(w, l, n):

    # Base Case
    if (n == 1):
        print(0)
        return

    # Store the required result
    ans = 0

    # Stores the current position of
    # elements and their respective
    # maximum jump
    pos = {}
    jump = {}

    # Used to check if a position is
    # already taken by another element
    filled = {}

    # Stores the sorted array a[]
    a = [0 for i in range(n)]

    # Traverse the array w[] & update
    # positions jumps array a[]
    for i in range(n):
        pos[w[i]] = i
        filled[i] = True
        jump[w[i]] = l[i]
        a[i] = w[i]

    # Sort the array a[]
    a.sort()

    # Traverse the array a[] over
    # the range [1, N-1]
    for curr in range(1, n, 1):

        # Store the index of current
        # element and its just smaller
        # element in array w[]
        currElementPos = pos[a[curr]]
        prevElementPos = pos[a[curr - 1]]

        if (currElementPos > prevElementPos):
            continue

        # Iterate until current element
        # position is at most its just
        # smaller element position
        while (currElementPos <= prevElementPos or
              (currElementPos in filled and
              filled[currElementPos])):
            currElementPos += jump[a[curr]]
            ans += 1

        # Update the position of the
        # current element
        pos[a[curr]] = currElementPos
        filled[currElementPos] = True

    # Print the result
    print(ans)

# Driver Code
if __name__ == '__main__':

    W = [ 2, 1, 4, 3 ]
    L = [ 4, 1, 2, 4 ]
    N = len(W)

    minJumps(W, L, N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum number
// of jumps required to sort the array
static void minJumps(int []w, int []l, int n)
{

    // Base Case
    if (n == 1)
    {
        Console.Write(0);
        return;
    }

    // Store the required result
    int ans = 0;

    // Stores the current position of
    // elements and their respective
    // maximum jump
    Dictionary<int,
               int> pos = new Dictionary<int,
                                         int>();
    Dictionary<int,
               int> jump = new Dictionary<int,
                                          int>();

    // Used to check if a position is
    // already taken by another element
     Dictionary<int,
                bool> filled = new Dictionary<int,
                                              bool>();

    // Stores the sorted array a[]
    int []a = new int[n];

    // Traverse the array w[] & update
    // positions jumps array a[]
    for(int i = 0; i < n; i++)
    {
        if (pos.ContainsKey(w[i]))
           pos[w[i]] = i;
        else
           pos.Add(w[i], i);
        if (filled.ContainsKey(w[i]))
           filled[i] = true;
        else
           filled.Add(i, true);
        if (jump.ContainsKey(w[i]))
           jump[w[i]] = l[i];
        else
           jump.Add(w[i], l[i]);

        a[i] = w[i];
    }

    // Sort the array a[]
    Array.Sort(a);

    // Traverse the array a[] over
    // the range [1, N-1]
    for(int curr = 1; curr < n; curr++)
    {

        // Store the index of current
        // element and its just smaller
        // element in array w[]
        int currElementPos = pos[a[curr]];
        int prevElementPos = pos[a[curr - 1]];

        if (currElementPos > prevElementPos)
            continue;

        // Iterate until current element
        // position is at most its just
        // smaller element position
        while (currElementPos <= prevElementPos ||
               filled.ContainsKey(currElementPos) &&
               filled[currElementPos])
        {
            currElementPos += jump[a[curr]];
            ans++;
        }

        // Update the position of the
        // current element
        if (pos.ContainsKey(a[curr]))
            pos[a[curr]] = currElementPos;
        else
            pos.Add(a[curr], currElementPos);
        if (filled.ContainsKey(currElementPos))
            filled[currElementPos] = true;
        else
            filled.Add(currElementPos, true);
    }

    // Print the result
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    int []W = { 2, 1, 4, 3 };
    int []L = { 4, 1, 2, 4 };
    int N = W.Length;

    minJumps(W, L, N);
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum number
// of jumps required to sort the array
function minJumps(w, l, n)
{

    // Base Case
    if (n == 1)
    {
        document.write(0);
        return;
    }

    // Store the required result
    var ans = 0;
    var i;

    // Stores the current position of
    // elements and their respective
    // maximum jump
    var pos = new Map();
    var jump = new Map();

    // Used to check if a position is
    // already taken by another element
    var filled = new Map();

    // Stores the sorted array a[]
    var a  = new Array(n);

    // Traverse the array w[] & update
    // positions jumps array a[]
    for(i = 0; i < n; i++)
    {
        pos.set(w[i], i);
        filled.set(i, true);
        jump.set(w[i], l[i]);
        a[i] = w[i];
    }

    // Sort the array a[]
    a = a.sort(function(p, q)
    {
        return p - q;
    });

    // Traverse the array a[] over
    // the range [1, N-1]
    for(curr = 1; curr < n; curr++)
    {

        // Store the index of current
        // element and its just smaller
        // element in array w[]
        var currElementPos = pos.get(a[curr]);
        var prevElementPos = pos.get(a[curr - 1]);

        if (currElementPos > prevElementPos)
            continue;

        // Iterate until current element
        // position is at most its just
        // smaller element position
        while (currElementPos <= prevElementPos ||
               filled[currElementPos])
        {
            currElementPos += jump.get(a[curr]);
            ans += 1;
        }

        // Update the position of the
        // current element
        pos.set(a[curr], currElementPos);
        filled.set(currElementPos, true);
    }

    // Print the result
    document.write(ans);
}

// Driver Code
var W = [ 2, 1, 4, 3 ];
var L = [ 4, 1, 2, 4 ];
var N = W.length;

minJumps(W, L, N);

// This code is contributed by ipg2016107

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*