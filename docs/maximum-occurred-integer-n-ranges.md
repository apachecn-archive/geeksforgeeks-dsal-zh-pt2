# n 个范围内出现的最大整数

> 原文:[https://www . geeksforgeeks . org/maximum-apparent-integer-n-ranges/](https://www.geeksforgeeks.org/maximum-occurred-integer-n-ranges/)

给定形式为 **L** 和 **R** 的 **n** 范围，任务是找出所有范围内出现的最大整数。如果存在多个这样的整数，打印最小的一个。
0 < = L <sub>i</sub> ，R<sub>I</sub>T16】1000000。
**举例:**

```
Input : L1 = 1 R1 = 15
        L2 = 4 R2 = 8
        L3 = 3 R3 = 5
        L3 = 1 R3 = 4
Output : 4

Input : L1 = 1 R1 = 15
        L2 = 5 R2 = 8
        L3 = 9 R3 = 12
        L4 = 13 R4 = 20
        L5 = 21 R5 = 30
Output : 5
Numbers having maximum occurrence i.e 2  are 5, 6,
7, 8, 9, 10, 11, 12, 13, 14, 15\. The smallest number
among all are 5.
```

### 朴素方法:-时间复杂度 O(N*M)

我们穿越了所有的山脉。然后，对于每个范围，我们计算频率，制作哈希表或哈希表，存储每个项目。然后你穿越其他范围，增加每个项目的频率。频率最高的项目就是我们的答案。但是这个解决方案需要时间，假设有 N 个范围，如果 M 是任何范围内元素的最大数量，那么它需要 O(N*M)个时间。哈希表的插入、搜索和删除时间复杂度为 O(1)。因此，您可以在哈希表中插入每一项，并在 O(1)中插入其频率。

### 高效**方法:-时间复杂度 O(N +最大)**

如果范围是固定的，比如说(0 <= Li，Ri < 1000000)，我们可以以更好的时间复杂度做到这一点。这里的诀窍是，我们不想走遍每一个范围的每一个元素。我们只想遍历所有范围，我们想使用前缀求和技术来解决这个问题。

我们创建一个向量/数组列表/数组。向量中的所有值都由零初始化(使用向量或数组列表来避免额外的行。c++或中的 memset()。java 中的 fill()。所以我们要做的是循环遍历每个范围，并标记每个范围开始的存在。我们简单地做这个 **arr[L[i]]++** 。我们还通过从 **arr[R[i+1]]** 中减去一来标记这个范围的结束。

正如我之前讨论的，我们将每个范围的开始标记为一个。

所以如果我做一个前缀求和，如果我标记开头，所有的值都会在这个元素之后加 1。现在我们只想增加到数组的末尾。我们不想增加其他元素。

> 假设，
> 
> L[] = {1，2，3}，R[] = {3，5，7}
> 
> 1.对于这个行 arr[L[i]]++数组变成{0，1，1，1，0，0，0，0，…}
> 
> 2.对于这个行 arr[R[I+1]]–数组变成{0，1，1，1，-1，0，-1，0，-1，1，-1，…}
> 
> 3.当我们做前缀求和时，数组变成{0，1，2，3，2，2，1，1，0…}

当我们做前缀求和时，我们会让(1)之后的元素的和增加 1，因为我标记了开头。现在我不希望这个增量发生在(3)之后的元素上。所以如果范围是 1，2，3，1，2，3 的值应该只加 1，或者它们的频率应该加 1。

这就是为什么我们降低 arr[R[i+1]]的值。这样，在这个范围结束后的元素的值减去 1。这就是当我要做前缀时，我们如何消除增加值的影响。

所以当我要做前缀的时候，我只是要增加范围之后的每个值，因为我只想在范围内增加。这就是这个算法的思想。

## C++

```
// C++ program to find maximum occurred element in
// given N ranges.
#include <bits/stdc++.h>
#define MAX 1000000
using namespace std;

// Return the maximum occurred element in all ranges.
int maximumOccurredElement(int L[], int R[], int n)
{
    // Initialising all element of array to 0.
    int arr[MAX];
    memset(arr, 0, sizeof arr);

    // Adding +1 at Li index and substracting 1
    // at Ri index.
    int maxi=-1;
    for (int i = 0; i < n; i++) {
        arr[L[i]] += 1;
        arr[R[i] + 1] -= 1;
        if(R[i]>maxi){
            maxi=R[i];
        }
    }

    // Finding prefix sum and index having maximum
    // prefix sum.
    int msum = arr[0],ind;
    for (int i = 1; i < maxi+1; i++) {
        arr[i] += arr[i - 1];
        if (msum < arr[i]) {
            msum = arr[i];
            ind = i;
        }
    }

    return ind;
}

// Driven Program
int main()
{
    int L[] = { 1, 4, 9, 13, 21 };
    int R[] = { 15, 8, 12, 20, 30 };
    int n = sizeof(L) / sizeof(L[0]);

    cout << maximumOccurredElement(L, R, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum occurred
// element in given N ranges.
import java.io.*;

class GFG {

    static int MAX = 1000000;

    // Return the maximum occurred element in all ranges.
    static int maximumOccurredElement(int[] L, int[] R, int n)
    {
        // Initialising all element of array to 0.
        int[] arr = new int[MAX];

        // Adding +1 at Li index and
        // substracting 1 at Ri index.
        int maxi=-1;
        for (int i = 0; i < n; i++) {
            arr[L[i]] += 1;
            arr[R[i] + 1] -= 1;
            if(R[i]>maxi){
            maxi=R[i];
           }
        }

        // Finding prefix sum and index
        // having maximum prefix sum.
        int msum = arr[0];
        int ind = 0;
        for (int i = 1; i < maxi+1; i++) {
            arr[i] += arr[i - 1];
            if (msum < arr[i]) {
                msum = arr[i];
                ind = i;
            }
        }

        return ind;
    }

    // Driver program
    static public void main(String[] args)
    {
        int[] L = { 1, 4, 9, 13, 21 };
        int[] R = { 15, 8, 12, 20, 30 };
        int n = L.length;
        System.out.println(maximumOccurredElement(L, R, n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find maximum occurred
# element in given N ranges.

MAX = 1000000

# Return the maximum occurred element
# in all ranges.
def maximumOccurredElement(L, R, n):

    # Initialising all element of array to 0.
    arr = [0 for i in range(MAX)]

    # Adding +1 at Li index and substracting 1
    # at Ri index.
    for i in range(0, n, 1):
        arr[L[i]] += 1
        arr[R[i] + 1] -= 1

    # Finding prefix sum and index
    # having maximum prefix sum.
    msum = arr[0]
    for i in range(1, MAX, 1):
        arr[i] += arr[i - 1]
        if (msum < arr[i]):
            msum = arr[i]
            ind = i
    return ind

# Driver Code
if __name__ == '__main__':
    L = [1, 4, 9, 13, 21]
    R = [15, 8, 12, 20, 30]
    n = len(L)

    print(maximumOccurredElement(L, R, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find maximum
// occurred element in given N ranges.
using System;

class GFG {

    static int MAX = 1000000;

    // Return the maximum occurred element in all ranges.
    static int maximumOccurredElement(int[] L, int[] R, int n)
    {
        // Initialising all element of array to 0.
        int[] arr = new int[MAX];

        // Adding +1 at Li index and
        // substracting 1 at Ri index.
        for (int i = 0; i < n; i++) {
            arr[L[i]] += 1;
            arr[R[i] + 1] -= 1;
        }

        // Finding prefix sum and index
        // having maximum prefix sum.
        int msum = arr[0];
        int ind = 0;
        for (int i = 1; i < MAX; i++) {
            arr[i] += arr[i - 1];
            if (msum < arr[i]) {
                msum = arr[i];
                ind = i;
            }
        }

        return ind;
    }

    // Driver program
    static public void Main()
    {
        int[] L = { 1, 4, 9, 13, 21 };
        int[] R = { 15, 8, 12, 20, 30 };
        int n = L.Length;
        Console.WriteLine(maximumOccurredElement(L, R, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum occurred
// element in given N ranges.
$MAX = 1000000;

// Return the maximum occurred element
// in all ranges.
function maximumOccurredElement($L, $R, $n)
{

    // Initialising all element
    // of array to 0.
    $arr = array();
    for($i = 0; $i < $n; $i++)
    {
        $arr[] = "0";
    }

    // Adding +1 at Li index and subtracting 1
    // at Ri index.
    for ($i = 0; $i < $n; $i++)
    {
        $arr[$L[$i]] += 1;
        $arr[$R[$i] + 1] -= 1;
    }

    // Finding prefix sum and index
    // having maximum prefix sum.
    $msum = $arr[0];

    for ($i = 1; $i <$n; $i++)
    {
        $arr[$i] += $arr[$i - 1];
        if ($msum < $arr[$i])
        {
            $msum = $arr[$i];
            $ind = $i;
        }
    }
    return $ind;
}

// Driver Code
$L = array(1, 4, 9, 13, 21);
$R = array(15, 8, 12, 20, 30);
$n = count($L);

echo maximumOccurredElement($L, $R, $n);

// This code is contributed by
// Srathore
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find maximum
    // occurred element in given N ranges.

    let MAX = 1000000;

    // Return the maximum occurred element in all ranges.
    function maximumOccurredElement(L, R, n)
    {
        // Initialising all element of array to 0.
        let arr = new Array(MAX);
        arr.fill(0);

        // Adding +1 at Li index and
        // substracting 1 at Ri index.
        for (let i = 0; i < n; i++) {
            arr[L[i]] += 1;
            arr[R[i] + 1] -= 1;
        }

        // Finding prefix sum and index
        // having maximum prefix sum.
        let msum = arr[0];
        let ind = 0;
        for (let i = 1; i < MAX; i++) {
            arr[i] += arr[i - 1];
            if (msum < arr[i]) {
                msum = arr[i];
                ind = i;
            }
        }

        return ind;
    }

    let L = [ 1, 4, 9, 13, 21 ];
    let R = [ 15, 8, 12, 20, 30 ];
    let n = L.length;
    document.write(maximumOccurredElement(L, R, n));

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(n + MAX)

**锻炼:**争取 0 < = L <sub>i</sub> ，R<sub>I</sub>T19】= 1000000000。(提示:使用 stl 贴图)。
**相关文章:**[m 范围增量运算后数组中的最大值](https://www.geeksforgeeks.org/maximum-value-array-m-range-increment-operations/)
本文由 **KaaL-EL** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。