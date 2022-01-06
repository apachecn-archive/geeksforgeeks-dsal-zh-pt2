# 给定数组按升序排序所需的最小跳转次数| Set-2

> 原文:[https://www . geesforgeks . org/最小跳转次数-按升序对给定数组进行排序所需的次数-集合-2/](https://www.geeksforgeeks.org/minimum-number-of-jumps-required-to-sort-the-given-array-in-ascending-order-set-2/)

给定两个 [<u>数组</u>](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和**jump【】**，每个长度 **N** ，其中**jump【I】**表示数组**arr【】**中的 **i** <sup>第</sup>个元素可以向前移动的索引数，任务是找到所需的最小跳转次数，使得数组按升序排序

*   *数组 **arr[]** 的所有元素都是不同的。*
*   *跳跃时，数组元素可以重叠(即位于同一索引上)。*
*   *数组元素可以移动到超过* [*数组大小的指数*](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/)

**示例:**

> **输入:** arr[] = {3，1，2}，jump[ ] = {1，4，5}
> **输出:** 3
> **解释:** *以下序列需要最小数量的跳转才能按升序对数组进行排序:*
> *Jump 1: arr[0]跳转 1 ( = jump[0])索引到索引 1。*
> *跳转 2: arr[0]跳转 1 ( =跳转[0])索引到索引 2。*
> *跳转 3: arr[0]跳转 1 ( =跳转[0])索引到索引 3。*
> *因此，所需的最小操作次数为 3 次。*
> 
> **输入:** arr[] = {3，2，1}，jump[ ] = {1，1，1}
> **输出:** 6
> **解释:** *以下序列需要最小数量的跳转才能按升序对数组进行排序:*
> *Jump 1: arr[0]跳转 1 ( = jump[0])索引到索引 1。*
> *跳转 2: arr[0]跳转 1 ( =跳转[0])索引到索引 2。*
> *跳转 3: arr[0]跳转 1 ( =跳转[0])索引到索引 3。*
> *跳转 4: arr[1]跳转 1 ( =跳转[0])索引到索引 2。*
> *跳转 5: arr[1]跳转 1 ( =跳转[0])索引到索引 3。*
> *跳转 6: arr[0]跳转 1 ( =跳转[0])索引到索引 4。*
> *因此，所需的最小操作次数为 6 次*。

**方法:**这个问题的[集-1](https://www.geeksforgeeks.org/minimum-number-of-jumps-required-to-sort-the-given-array-in-ascending-order/) 中提到了求解的天真方法。为了确定每个元素的跳跃次数，需要借助[地图](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。对于当前元素，确定将按排序顺序出现的前一个元素，然后确定将当前元素放在该元素之后所需的跳转次数。遵循以下步骤:

*   存储地图中每个元素的当前位置。
*   将元素按排序顺序存储在集合中。
*   按排序顺序找出当前元素与其前一个元素的位置差异。然后用差除以当前一跳的长度，求出所需的跳数。
*   把这个数加到最后的答案上。
*   返回最终答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum required jumps
int minJumps(
    vector<int> arr, vector<int> jump, int N)
{
    int temp[N];
    for (int i = 0; i < N; i++)
        temp[i] = arr[i];
    sort(temp, temp + N);
    unordered_map<int, int> a;
    for (int i = 0; i < N; i++)
    {
        a[arr[i]] = i;
    }
    int ans = 0;
    int x = 1, y = 0;
    while (x < N)
    {
        if (a[temp[x]] <= a[temp[y]])
        {
            int jumps = ceil((a[temp[y]] - a[temp[x]] + 1) / jump[a[temp[x]]]);

            ans += jumps;
            a[temp[x]] = a[temp[x]] + jumps * jump[a[temp[x]]];
        }
        x++;
        y++;
    }
    return ans;
}

// Driver code
int main()
{
    int N = 3;
    vector<int> arr = {3, 2, 1};
    vector<int> jump = {1, 1, 1};

    cout << (minJumps(arr, jump, N));
    return 0;
}

// This code is contributed by lokeshpotta20.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.io.*;
import java.util.*;

class GFG {
    // Function to return minimum required jumps
    public static int minJumps(
        int arr[], int jump[], int N)
    {
        int temp[] = new int[N];
        for (int i = 0; i < N; i++)
            temp[i] = arr[i];
        Arrays.sort(temp);
        HashMap<Integer, Integer> a = new HashMap<>();
        for (int i = 0; i < N; i++) {
            a.put(arr[i], i);
        }
        int ans = 0;
        int x = 1, y = 0;
        while (x < N) {
            if (a.get(temp[x]) <= a.get(temp[y])) {
                int jumps = (int)Math.ceil(
                    (float)(a.get(temp[y])
                            - a.get(temp[x])
                            + 1)
                    / jump[a.get(temp[x])]);
                ans += jumps;
                a.put(temp[x],
                      a.get(temp[x])
                          + jumps
                                * jump[a.get(temp[x])]);
            }
            x++;
            y++;
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 3;
        int arr[] = { 3, 2, 1 };
        int jump[] = { 1, 1, 1 };

        System.out.println(minJumps(arr, jump, N));
    }
}
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return minimum required jumps
public static int minJumps(int[] arr, int[] jump, int N)
{
    int[] temp = new int[N];
    for(int i = 0; i < N; i++)
        temp[i] = arr[i];

    Array.Sort(temp);
    Dictionary<int, int> a = new Dictionary<int, int>();

    for(int i = 0; i < N; i++)
    {
        a[arr[i]] = i;
    }

    int ans = 0;
    int x = 1, y = 0;
    while (x < N)
    {
        if (a[temp[x]] <= a[temp[y]])
        {
            int jumps = (int)Math.Ceiling(
                (float)(a[temp[y]] - a[temp[x]] + 1) /
                   jump[a[temp[x]]]);

            ans += jumps;
            a[temp[x]] = a[temp[x]] + jumps * jump[a[temp[x]]];
        }
        x++;
        y++;
    }
    return ans;
}

// Driver code
public static void Main(string[] args)
{
    int N = 3;
    int[] arr = { 3, 2, 1 };
    int[] jump = { 1, 1, 1 };

    Console.Write(minJumps(arr, jump, N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to return minimum required jumps
    const minJumps = (arr, jump, N) => {
        let temp = new Array(N).fill(0);
        for (let i = 0; i < N; i++)
            temp[i] = arr[i];
        temp.sort();
        let a = {};
        for (let i = 0; i < N; i++) {
            a[arr[i]] = i;
        }
        let ans = 0;
        let x = 1, y = 0;
        while (x < N) {
            if (a[temp[x]] <= a[temp[y]]) {
                let jumps = Math.ceil((a[temp[y]] - a[temp[x]] + 1) / jump[a[temp[x]]]);

                ans += jumps;
                a[temp[x]] = a[temp[x]] + jumps * jump[a[temp[x]]];
            }
            x++;
            y++;
        }
        return ans;
    }

    // Driver code

    let N = 3;
    let arr = [3, 2, 1];
    let jump = [1, 1, 1];

    document.write(minJumps(arr, jump, N));

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
6
```

***时间复杂度:**T3】O(N * logN)
T5】T6】辅助空间:T8】O(N)*