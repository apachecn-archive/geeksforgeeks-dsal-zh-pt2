# 将二进制数组分成三等份相同的值

> 原文:[https://www . geeksforgeeks . org/将二进制数组分成三个相同值的等份/](https://www.geeksforgeeks.org/divide-binary-array-into-three-equal-parts-with-same-value/)

给定长度为 n 的数组 A，使得它只包含' **0** s '和' **1** s '。任务是将数组分成三个不同的非空部分，这样所有这些部分都代表相同的二进制值(以小数表示)。
如果可能，用 i+1 < j 返回任意[i，j]，如:
1。A[0]，A[1]，…，A[i]为**第一部分**。
2。A[i+1]，A[i+2]，…，A[j-1]为**第二部分**。
3。A[j]，A[j+1]，…，A[n- 1]为**第三部分**。
注意:三个部分都要有相等的二进制值。但是，如果不可能，则返回[-1，-1]。

**示例:**

```
Input : A = [1, 1, 1, 1, 1, 1]
Output : [1, 4]
All three parts are,
A[0] to A[1] first part,
A[2] to A[3] second part,
A[4] to A[5] third part.

Input : A = [1, 0, 0, 1, 0, 1]
Output : [0, 4]

```

**方法:**
假设 A 中的 1 的总数是 S，由于每个部分都有相同数量的 1，因此所有部分都应该有 K = S / 3 个 1。

如果 S 不能被 3 整除，即 **S % 3！= 0** ，那么任务就不可能了。

现在我们将找到**第 1 个、第 K 个、第 K+1 个、第 2K 个、第 2K+1 个和第 3K 一个**的位置。这些位置将形成 3 个区间:**【i1，J1】【I2，J2】【i3，J3】**。(如果只有 3 个 1，那么每个间隔长度为 1。)

在间隔之间，可能有一些零。第三个间隔 j3 之后的零必须包含在每个部分中:假设它们有 z 个(z =长度为(S)–J3)。

所以第一部分**【i1，J1】**，就是现在的**【i1，J1+z】**。同样，第二部分**【I2，J2】**，现在是**【I2，J2+z】**。

如果这一切其实都有可能，那么最终的答案就是**【J1+z，J2+z+1】**。

**以下是上述方法的实施。**

## C++

```
// C++ implementation of the 
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return required 
// interval answer.
vector<int> ThreeEqualParts(vector<int> A)
{
    int imp[] = {-1, -1};
    vector<int> IMP(imp, imp + 2);

    // Finding total number of ones
    int Sum = accumulate(A.begin(), 
                         A.end(), 0);

    if (Sum % 3)
    {
        return IMP;
    }

    int K = Sum / 3;

    // Array contains all zeros.
    if (K == 0)
    {
        return {0, (int)A.size() - 1};
    }

    vector<int> interval;
    int S = 0;

    for (int i = 0 ;i < A.size(); i++)
    {
        int x = A[i];
        if (x)
        {
            S += x;
            if (S == 1 or S == K + 1 or S == 2 * K + 1)
            {
                interval.push_back(i);
            }
            if (S == K or S == 2 * K or S == 3 * K)
            {
                interval.push_back(i);
            }
        }
    }

    int i1 = interval[0], j1 = interval[1],
        i2 = interval[2], j2 = interval[3],
        i3 = interval[4], j3 = interval[5];

    vector<int> a(A.begin() + i1, A.begin() + j1 + 1);
    vector<int> b(A.begin() + i2, A.begin() + j2 + 1);
    vector<int> c(A.begin() + i3, A.begin() + j3 + 1);

    // The array is in the form 
    // W [i1, j1] X [i2, j2] Y [i3, j3] Z
    // where [i1, j1] is a block of 1s, and so on.
    if (!((a == b) and (b == c)))
    {
        return {-1, -1};
    }

    // x, y, z: the number of zeros
    // after part 1, 2, 3
    int x = i2 - j1 - 1;
    int y = i3 - j2 - 1;
    int z = A.size() - j3 - 1;

    if (x < z or y < z)
    {
        return IMP;
    } 

    // appending extra zeros at end of 
    // first and second interval
    j1 += z;
    j2 += z;
    return {j1, j2 + 1}; 
}

// Driver Code
int main()
{
    vector<int> A = {1, 1, 1, 1, 1, 1}; 

    // Output required result
    vector<int> res = ThreeEqualParts(A);

    for(auto it :res)
        cout << it << " ";

    return 0;
}

// This code is contributed 
// by Harshit Saini 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the 
// above approach
import java.util.*;

class GFG
{

// Function to return required 
// interval answer.
public static int[] ThreeEqualParts(int[] A)
{
    int IMP[] = new int[]{-1, -1};

    // Finding total number of ones
    int Sum = Arrays.stream(A).sum();

    if ((Sum % 3) != 0)
    {
        return IMP;
    }

    int K = Sum / 3;

    // Array contains all zeros.
    if (K == 0)
    {
        return new int[]{0, A.length - 1};
    }

    ArrayList<Integer> interval = 
                   new ArrayList<Integer>();
    int S = 0;

    for (int i = 0 ;i < A.length; i++)
    {
        int x = A[i];
        if (x != 0)
        {
            S += x;
            if ((S == 1) || (S == K + 1) || 
                (S == 2 * K + 1))
            {
                interval.add(i);
            }
            if ((S == K) || (S == 2 * K) || 
                (S == 3 * K))
            {
                interval.add(i);
            }
        }
    }

    int i1 = interval.get(0), j1 = interval.get(1),
        i2 = interval.get(2), j2 = interval.get(3),
        i3 = interval.get(4), j3 = interval.get(5);

    int [] a = Arrays.copyOfRange(A, i1, j1 + 1);
    int [] b = Arrays.copyOfRange(A, i2, j2 + 1);
    int [] c = Arrays.copyOfRange(A, i3, j3 + 1);

    // The array is in the form
    // W [i1, j1] X [i2, j2] Y [i3, j3] Z
    // where [i1, j1] is a block of 1s, and so on.
    if (!(Arrays.equals(a, b) && 
          Arrays.equals(b, c)))
    {
        return new int[]{-1, -1};
    }

    // x, y, z: 
    // the number of zeros after part 1, 2, 3
    int x = i2 - j1 - 1;
    int y = i3 - j2 - 1;
    int z = A.length - j3 - 1;

    if (x < z || y < z)
    {
        return IMP;
    } 

    // appending extra zeros at end 
    // of first and second interval
    j1 += z;
    j2 += z;
    return new int[]{j1, j2 + 1}; 
}

// Driver Code
public static void main(String []args)
{
    int[] A = new int[]{1, 1, 1, 1, 1, 1}; 

    // Output required result
    int[] res = ThreeEqualParts(A);

    System.out.println(Arrays.toString(res));
}
}

// This code is contributed 
// by Harshit Saini 
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to return required interval answer.
def ThreeEqualParts(A):
    IMP = [-1, -1]

    # Finding total number of ones
    Sum = sum(A)

    if Sum % 3:
        return IMP

    K = Sum / 3

    # Array contains all zeros.
    if K == 0:
        return [0, len(A) - 1]

    interval = []
    S = 0

    for i, x in enumerate(A):
        if x:
            S += x
            if S in {1, K + 1, 2 * K + 1}:
                interval.append(i)
            if S in {K, 2 * K, 3 * K}:
                interval.append(i)

    i1, j1, i2, j2, i3, j3 = interval

    # The array is in the form W [i1, j1] X [i2, j2] Y [i3, j3] Z
    # where [i1, j1] is a block of 1s, and so on.
    if not(A[i1:j1 + 1] == A[i2:j2 + 1] == A[i3:j3 + 1]):
        return [-1, -1]

    # x, y, z: the number of zeros after part 1, 2, 3
    x = i2 - j1 - 1
    y = i3 - j2 - 1
    z = len(A) - j3 - 1

    if x < z or y < z:
        return IMP

    # appending extra zeros at end of first and second interval
    j1 += z
    j2 += z
    return [j1, j2 + 1]

# Driver Program
A = [1, 1, 1, 1, 1, 1]

# Output required result
print(ThreeEqualParts(A))

# This code is written by
# Sanjit_Prasad
```

## C#

```
// C# implementation of the 
// above approach
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

// Function to return required
// interval answer.
static int[] ThreeEqualParts(int[] A)
{

    int []IMP = new int[]{-1, -1};

    // Finding total number of ones
    int Sum = A.Sum();

    if ((Sum % 3) != 0)
    {
        return IMP;
    }

    int K = Sum / 3;

    // Array contains all zeros.
    if (K == 0)
    {
        return new int[]{0, A.Length - 1};
    }

    List<int> interval = new List<int>();

    int S = 0;

    for (int i = 0 ;i < A.Length; i++)
    {
        int x = A[i];
        if (x != 0)
        {
            S += x;
            if ((S == 1) || (S == K + 1) || 
                (S == 2 * K + 1))
            {
                interval.Add(i);
            }
            if ((S == K) || (S == 2 * K) || 
                (S == 3 * K))
            {
                interval.Add(i);
            }
        }
    }

    int i1 = interval[0], j1 = interval[1],
        i2 = interval[2], j2 = interval[3],
        i3 = interval[4], j3 = interval[5];

    var a = A.Skip(i1).Take(j1 - i1 + 1).ToArray();
    var b = A.Skip(i2).Take(j2 - i2 + 1).ToArray();
    var c = A.Skip(i3).Take(j3 - i3 + 1).ToArray();

    // The array is in the form 
    // W [i1, j1] X [i2, j2] Y [i3, j3] Z
    // where [i1, j1] is a block of 1s,
    // and so on.
    if (!(Enumerable.SequenceEqual(a,b) && 
          Enumerable.SequenceEqual(b,c)))
    {
        return new int[]{-1, -1};
    }

    // x, y, z: the number of zeros
    // after part 1, 2, 3
    int X = i2 - j1 - 1;
    int y = i3 - j2 - 1;
    int z = A.Length - j3 - 1;

    if (X < z || y < z)
    {
        return IMP;
    } 

    // appending extra zeros at end 
    // of first and second interval
    j1 += z;
    j2 += z;
    return new int[]{j1, j2 + 1}; 
}

// Driver Code
public static void Main()
{
    int[] A = new int[]{1, 1, 1, 1, 1, 1}; 

    // Output required result
    int[] res = ThreeEqualParts(A);

    Console.WriteLine(string.Join(" ", res));
}
}

// This code is contributed 
// by Harshit Saini 
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function to return required 
// interval answer.
function ThreeEqualParts($A)
{

    $IMP = array(-1, -1);

    // Finding total number of ones
    $Sum = array_sum($A);

    if ($Sum % 3)
    {
        return $IMP;
    }
    $K = $Sum / 3;

    // Array contains all zeros.
    if ($K == 0)
    {
        return array(0, count(A, 
                     COUNT_NORMAL) - 1);
    }

    $interval = array();
    $S = 0;

    for ($i = 0; 
         $i < count($A, COUNT_NORMAL); $i++)
    {
        $x = $A[$i];
        if ($x)
        {
            $S += $x;
            if ($S == 1 or $S == $K + 1 or
                $S == 2 * $K + 1)
            {
                array_push($interval,$i);
            }
            if ($S == $K or $S == 2 * $K or
                $S == 3 * $K)
            {
                array_push($interval, $i);
            }
        }
    }

    $i1 = $interval[0]; $j1 = $interval[1];
    $i2 = $interval[2]; $j2 = $interval[3];
    $i3 = $interval[4]; $j3 = $interval[5];

    $a = array_slice($A, $i1, $j1 - $i1 + 1);
    $b = array_slice($A, $i1, $j2 - $i2 + 1);
    $c = array_slice($A, $i1, $j3 - $i3 + 1);

    // The array is in the form  
    // W [i1, j1] X [i2, j2] Y [i3, j3] Z
    // where [i1, j1] is a block of 1s,
    // and so on.
    if (!($a == $b and $b == $c))
    {
        return array(-1, -1);
    }

    // x, y, z: the number of zeros
    // after part 1, 2, 3
    $x = $i2 - $j1 - 1;
    $y = $i3 - $j2 - 1;
    $z = count($A) - $j3 - 1;

    if ($x < $z or $y < $z)
    {
        return $IMP;
    } 

    // appending extra zeros at end 
    // of first and second interval
    $j1 += $z;
    $j2 += $z;
    return array($j1, $j2 + 1); 
}

// Driver Code
$A = array(1, 1, 1, 1, 1, 1); 

// Output required result
$res = ThreeEqualParts($A);

foreach ($res as $key => $value) 
{
    echo $value." ";
}

// This code is contributed 
// by Harshit Saini 
?>
```

**Output:**

```
1 4 
```

**时间复杂度:** O(N)，其中 N 为 s 的长度
T3】空间复杂度: O(N)