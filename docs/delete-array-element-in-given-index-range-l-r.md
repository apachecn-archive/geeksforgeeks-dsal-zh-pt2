# 删除给定索引范围内的数组元素[L–R]

> 原文:[https://www . geesforgeks . org/delete-array-element-in-给定-index-range-l-r/](https://www.geeksforgeeks.org/delete-array-element-in-given-index-range-l-r/)

给定一个数组 A[]，数组的大小为 n。任务是删除数组 A[]中在给定范围 L 到 R 内的元素，这两个元素是互斥的。
**例:**

```
Input : N = 12
        A[] = { 3, 5, 3, 4, 9, 3, 1, 6, 3, 11, 12, 3}
        L = 2
        R = 7
Output : 3 5 3 6 3 11 12 3 
since A[2] = 3 but this is exclude 
A[7] =  6 this also exclude 

Input : N = 10
        A[] ={ 5, 8, 11, 15, 26, 14, 19, 17, 10, 14 }
        L = 4
        R = 6
Output :5 8 11 15 26 19 17 10 14 
```

一种**天真的方法**是删除 L 到 R 范围内有额外空间的元素。
以下是上述办法的实施情况:

## C++

```
// C++ code to delete element
// in given range
#include <bits/stdc++.h>
using namespace std;

// Delete L to R element
vector<int> deleteElement(int A[], int L, int R, int N)
{
    vector<int> B;

    for (int i = 0; i < N; i++)
        if (i <= L || i >= R)
           B.push_back(A[i]);       

    return B;
}

// main Driver
int main()
{
    int A[] = { 3, 5, 3, 4, 9, 3, 1, 6, 3, 11, 12, 3 };
    int L = 2, R = 7;
    int n = sizeof(A) / sizeof(A[0]);
    vector<int> res = deleteElement(A, L, R, n);
    for (auto x : res)
        cout << x << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Vector;

// Java code to delete element
// in given range
class GFG {
// Delete L to R element

    static Vector<Integer> deleteElement(int A[], int L, int R, int N) {
        Vector<Integer> B = new Vector<>();

        for (int i = 0; i < N; i++) {
            if (i <= L || i >= R) {
                B.add(A[i]);
            }
        }

        return B;
    }

// main Driver
    public static void main(String[] args) {
        int A[] = {3, 5, 3, 4, 9, 3, 1, 6, 3, 11, 12, 3};
        int L = 2, R = 7;
        int n = A.length;
        Vector<Integer> res = deleteElement(A, L, R, n);
        for (Integer x : res) {
            System.out.print(x + " ");
        }
    }
}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 code to delete element
# in given range

# Delete L to R element
def deleteElement(A, L, R, N):
    B = []

    for i in range(0, N, 1):
        if (i <= L or i >= R):
            B.append(A[i])

    return B

# Driver Code
if __name__ == '__main__':
    A = [3, 5, 3, 4, 9, 3, 1,
             6, 3, 11, 12, 3]
    L = 2
    R = 7
    n = len(A)
    res = deleteElement(A, L, R, n)
    for i in range(len(res)):
        print(res[i], end = " ")

# THis code is implemented by
# Surendra_Gangwar
```

## C#

```
// C# code to delete element
// in given range
using System;
using System.Collections.Generic;

class GFG
{

    // Delete L to R element
    static List<int> deleteElement(int []A,
                        int L, int R, int N)
    {
        List<int> B = new List<int>();
        for (int i = 0; i < N; i++)
        {
            if (i <= L || i >= R)
            {
                B.Add(A[i]);
            }
        }
        return B;
    }

    // Driver code
    public static void Main()
    {
        int []A = {3, 5, 3, 4, 9, 3, 1, 6,
                            3, 11, 12, 3};
        int L = 2, R = 7;
        int n = A.Length;
        List<int> res = deleteElement(A, L, R, n);
        foreach (int x in res)
        {
            Console.Write(x + " ");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to delete element
// in given range

// Delete L to R element
function deleteElement($A, $L, $R, $N)
{
    $B = array();

    for ($i = 0; $i < $N; $i++)
    {
        if ($i <= $L or $i >= $R)
            $B[] = $A[$i];
    }
    return $B;
}

// Driver Code
$A = array(3, 5, 3, 4, 9, 3, 1,
              6, 3, 11, 12, 3);
$L = 2;
$R = 7;
$n = count($A);
$res = deleteElement($A, $L, $R, $n);
for ($i = 0; $i < count($res); $i++)
echo "$res[$i] ";

// This code is implemented by
// Srathore
?>
```

## java 描述语言

```
<script>
    // Javascript code to delete element in given range

    function deleteElement(A, L, R, N) {
        let B = [];

        for (let i = 0; i < N; i++) {
            if (i <= L || i >= R) {
                B.push(A[i]);
            }
        }

        return B;
    }

    let A = [3, 5, 3, 4, 9, 3, 1, 6, 3, 11, 12, 3];
    let L = 2, R = 7;
    let n = A.length;
    let res = deleteElement(A, L, R, n);
    for(let i = 0; i < res.length; i++)
      document.write(res[i] + " ");

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3 5 3 6 3 11 12 3
```