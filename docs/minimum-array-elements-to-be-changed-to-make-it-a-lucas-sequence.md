# 要更改的最小数组元素，使其成为卢卡斯序列

> 原文:[https://www . geesforgeks . org/最小数组-要更改的元素-使其成为-a-lucas-sequence/](https://www.geeksforgeeks.org/minimum-array-elements-to-be-changed-to-make-it-a-lucas-sequence/)

给定一个有 N 个不同元素的数组。任务是找到数组中要更改的元素的最小数量，使得数组包含**第 N 个** [**卢卡斯序列**](https://www.geeksforgeeks.org/lucas-numbers/) **术语**。
**注**:卢卡斯术语在数组中可以任意顺序出现。
**示例** :

> **输入** : arr[] = {29，1，3，4，5，11，18，2}
> **输出** : 1
> 5 必须改为 7，才能得到卢卡斯数列的前 N(8)项。
> 因此，需要 1 次更改
> **输入** : arr[] = {4，2，3，1}
> **输出** : 0
> 所有元素都已经是 Lucas 序列中的前 N(4)项。

**进场:**

*   在集合中插入前 N 个(输入数组的大小)卢卡斯序列项。
*   从左到右遍历数组，检查数组元素是否存在于集合中。
*   如果存在，将其从集合中移除。
*   所需的最小更改是最终剩余集的大小。

以下是上述方法的实现:

## C++

```
// C++ program to find the minimum number
// of elements to be changed in the array
// to make it a Lucas Sequence
#include <bits/stdc++.h>
using namespace std;

// Function that finds minimum changes to
// be made in the array
int lucasArray(int arr[], int n)
{
    set<int> s;

    // a and b are first two
    // lucas numbers
    int a = 2, b = 1;
    int c;

    // insert first n lucas elements to set
    s.insert(a);
    if (n >= 2)
        s.insert(b);

    for (int i = 0; i < n - 2; i++) {
        s.insert(a + b);
        c = a + b;
        a = b;
        b = c;
    }

    set<int>::iterator it;
    for (int i = 0; i < n; i++) {
        // if lucas element is present in array,
        // remove it from set
        it = s.find(arr[i]);
        if (it != s.end())
            s.erase(it);
    }

    // return the remaining number of
    // elements in the set
    return s.size();
}

// Driver code
int main()
{
    int arr[] = { 7, 11, 22, 4, 2, 1, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << lucasArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number
// of elements to be changed in the array
// to make it a Lucas Sequence
import java.util.HashSet;
import java.util.Set;

class GfG
{

    // Function that finds minimum changes
    // to be made in the array
    static int lucasArray(int arr[], int n)
    {
        HashSet<Integer> s = new HashSet<>();

        // a and b are first two lucas numbers
        int a = 2, b = 1, c;

        // insert first n lucas elements to set
        s.add(a);
        if (n >= 2)
            s.add(b);

        for (int i = 0; i < n - 2; i++)
        {
            s.add(a + b);
            c = a + b;
            a = b;
            b = c;
        }

        for (int i = 0; i < n; i++)
        {
            // if lucas element is present in array,
            // remove it from set
            if (s.contains(arr[i]))
                s.remove(arr[i]);
        }

        // return the remaining number of
        // elements in the set
        return s.size();
    }

    // Driver code
    public static void main(String []args)
    {

        int arr[] = { 7, 11, 22, 4, 2, 1, 8, 9 };
        int n = arr.length;

        System.out.println(lucasArray(arr, n));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python 3 program to find the minimum number
# of elements to be changed in the array
# to make it a Lucas Sequence

# Function that finds minimum changes to
# be made in the array
def lucasArray(arr, n):
    s = set()

    # a and b are first two
    # lucas numbers
    a = 2
    b = 1

    # insert first n lucas elements to set
    s.add(a)
    if (n >= 2):
        s.add(b)

    for i in range(n - 2):
        s.add(a + b)
        c = a + b
        a = b
        b = c

    for i in range(n):

        # if lucas element is present in array,
        # remove it from set
        if (arr[i] in s):
            s.remove(arr[i])

    # return the remaining number of
    # elements in the set
    return len(s)

# Driver code
if __name__ == '__main__':
    arr = [7, 11, 22, 4, 2, 1, 8, 9]
    n = len(arr)

    print(lucasArray(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the minimum number
// of elements to be changed in the array
// to make it a Lucas Sequence
using System;
using System.Collections.Generic;

class GFG
{

    // Function that finds minimum changes
    // to be made in the array
    static int lucasArray(int []arr, int n)
    {
        HashSet<int> s = new HashSet<int>();

        // a and b are first two lucas numbers
        int a = 2, b = 1, c;

        // insert first n lucas elements to set
        s.Add(a);
        if (n >= 2)
            s.Add(b);

        for (int i = 0; i < n - 2; i++)
        {
            s.Add(a + b);
            c = a + b;
            a = b;
            b = c;
        }

        for (int i = 0; i < n; i++)
        {
            // if lucas element is present in array,
            // remove it from set
            if (s.Contains(arr[i]))
                s.Remove(arr[i]);
        }

        // return the remaining number of
        // elements in the set
        return s.Count;
    }

    // Driver code
    public static void Main(String []args)
    {

        int []arr = { 7, 11, 22, 4, 2, 1, 8, 9 };
        int n = arr.Length;

        Console.WriteLine(lucasArray(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the minimum number
// of elements to be changed in the array
// to make it a Lucas Sequence

// Function that finds minimum changes to
// be made in the array
function lucasArray(arr, n)
{
    var s = new Set();

    // a and b are first two
    // lucas numbers
    var a = 2, b = 1;
    var c;

    // insert first n lucas elements to set
    s.add(a);
    if (n >= 2)
        s.add(b);

    for (var i = 0; i < n - 2; i++) {
        s.add(a + b);
        c = a + b;
        a = b;
        b = c;
    }

    for (var i = 0; i < n; i++) {
        // if lucas element is present in array,
        // remove it from set

        s.delete(arr[i])
    }

    // return the remaining number of
    // elements in the set
    return s.size;
}

// Driver code
var arr = [7, 11, 22, 4, 2, 1, 8, 9 ];
var n = arr.length;
document.write( lucasArray(arr, n));

</script>
```

**Output:** 

```
3
```