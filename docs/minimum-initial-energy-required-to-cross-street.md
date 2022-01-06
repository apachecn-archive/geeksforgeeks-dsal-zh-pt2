# 穿过街道所需的最小初始能量

> 原文:[https://www . geesforgeks . org/最小-初始-过街所需能量/](https://www.geeksforgeeks.org/minimum-initial-energy-required-to-cross-street/)

给定一个包含正数和负数的数组。该阵列表示从街道一端到另一端的检查点。正值和负值表示该检查点的能量。正数增加能量，负数减少能量。找出穿过街道所需的最小初始能量，使能量水平永远不会变成 0 或小于 0。

**<u>注:</u>** 即使我们在任何检查站都没有将能量损失到小于等于 0 的情况下成功过马路，所需的最小初始能量值也将为 1。初始检查点需要 1。

**示例:**

```
Input : arr[] = {4, -10, 4, 4, 4}
Output: 7
Suppose initially we have energy = 0, now at 1st
checkpoint, we get 4\. At 2nd checkpoint, energy gets
reduced by -10 so we have 4 + (-10) = -6 but at any 
checkpoint value of energy can not less than equals 
to 0\. So initial energy must be at least 7 because
having 7 as initial energy value at 1st checkpoint
our energy will be = 7+4 = 11 and then we can cross 
2nd checkpoint successfully. Now after 2nd checkpoint,
all checkpoint have positive value so we can cross 
street successfully with 7 initial energy.

Input : arr[] = {3, 5, 2, 6, 1}
Output: 1
We need at least 1 initial energy to reach first
checkpoint

Input : arr[] = {-1, -5, -9}
Output: 16
```

我们取初始最小能量 0，即:initMinEnergy = 0，任何检查点的能量为 currEnergy = 0。现在线性遍历每个检查点，并在每个第 I 个检查点增加能量水平，即；currengy = currengy+arr[I]。如果电流变得非正，那么我们至少需要“abs(电流)+ 1”额外的初始能量来越过这个点。因此我们更新 initMinEnergy =(initMinEnergy+ABS(currEnergy)+1)。我们还更新了 currEnergy = 1，因为我们现在有了下一个点所需的额外最小初始能量。

以下是上述想法的实现。

## C++

```
// C++ program to find minimum initial energy to
// reach end
#include<bits/stdc++.h>
using namespace std;

// Function to calculate minimum initial energy
// arr[] stores energy at each checkpoints on street
int minInitialEnergy(int arr[], int n)
{
    // initMinEnergy is variable to store minimum initial
    // energy required.
    int initMinEnergy = 0;

    // currEnergy is variable to store current value of
    // energy at i'th checkpoint on street
    int currEnergy = 0;

    // flag to check if we have successfully crossed the
    // street without any energy loss <= o at any checkpoint
    bool flag = 0;

    // Traverse each check point linearly
    for (int i=0; i<n; i++)
    {
        currEnergy += arr[i];

        // If current energy, becomes negative or 0, increment
        // initial minimum energy by the negative value plus 1.
        // to keep current energy positive (at least 1). Also
        // update current energy and flag.
        if (currEnergy <= 0)
        {
            initMinEnergy += abs(currEnergy) +1;
            currEnergy = 1;
            flag = 1;
        }
    }

    // If energy never became negative or 0, then
    // return 1\. Else return computed initMinEnergy
    return (flag == 0)? 1 : initMinEnergy;
}

// Driver Program to test the case
int main()
{
    int arr[] = {4, -10, 4, 4, 4};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << minInitialEnergy(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// initial energy to reach end

class GFG {

// Function to calculate minimum
// initial energy arr[] stores energy
// at each checkpoints on street
static int minInitialEnergy(int arr[], int n)
{
    // initMinEnergy is variable to store
    // minimum initial energy required.
    int initMinEnergy = 0;

    // currEnergy is variable to store
    // current value of energy at
    // i'th checkpoint on street
    int currEnergy = 0;

    // flag to check if we have successfully
    // crossed the street without any energy
    // loss <= o at any checkpoint
    boolean flag = false;

    // Traverse each check point linearly
    for (int i = 0; i < n; i++) {
    currEnergy += arr[i];

    // If current energy, becomes negative or 0,
    // increment initial minimum energy by the negative
    // value plus 1\. to keep current energy
    // positive (at least 1). Also
    // update current energy and flag.
    if (currEnergy <= 0) {
        initMinEnergy += Math.abs(currEnergy) + 1;
        currEnergy = 1;
        flag = true;
    }
    }

    // If energy never became negative or 0, then
    // return 1\. Else return computed initMinEnergy
    return (flag == false) ? 1 : initMinEnergy;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {4, -10, 4, 4, 4};
    int n = arr.length;
    System.out.print(minInitialEnergy(arr, n));
}
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to find minimum initial energy to
# reach end

# Function to calculate minimum initial energy
# arr[] stores energy at each checkpoints on street
def minInitialEnergy(arr):
    n = len(arr)

    # initMinEnergy is variable to store minimum initial
    # energy required
    initMinEnergy = 0;

    # currEnergy is variable to store current value of
    # energy at i'th checkpoint on street
    currEnergy = 0

    # flag to check if we have successfully crossed the
    # street without any energy loss <= 0 at any checkpoint
    flag = 0

    # Traverse each check point linearly
    for i in range(n):
        currEnergy += arr[i]

        # If current energy, becomes negative or 0, increment
        # initial minimum energy by the negative value plus 1.
        # to keep current energy positive (at least 1). Also
        # update current energy and flag.
        if currEnergy <= 0 :
            initMinEnergy += (abs(currEnergy) +1)
            currEnergy = 1
            flag = 1

    # If energy never became negative or 0, then
    # return 1\. Else return computed initMinEnergy
    return 1 if flag == 0 else initMinEnergy

# Driver program to test above function
arr = [4, -10 , 4, 4, 4]
print minInitialEnergy(arr)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to find minimum
// C# program to find minimum
// initial energy to reach end
using System;

class GFG {

// Function to calculate minimum
// initial energy arr[] stores energy
// at each checkpoints on street
static int minInitialEnergy(int []arr, int n)
{

    // initMinEnergy is variable to store
    // minimum initial energy required.
    int initMinEnergy = 0;

    // currEnergy is variable to store
    // current value of energy at
    // i'th checkpoint on street
    int currEnergy = 0;

    // flag to check if we have successfully
    // crossed the street without any energy
    // loss <= o at any checkpoint
    bool flag = false;

    // Traverse each check point linearly
    for (int i = 0; i < n; i++) {
    currEnergy += arr[i];

    // If current energy, becomes negative or 0,
    // negativeincrement initial minimum energy
    // by the value plus 1\. to keep current
    // energy positive (at least 1). Also
    // update current energy and flag.
    if (currEnergy <= 0)
    {
        initMinEnergy += Math.Abs(currEnergy) + 1;
        currEnergy = 1;
        flag = true;
    }
    }

    // If energy never became negative
    // or 0, then return 1\. Else return
    // computed initMinEnergy
    return (flag == false) ? 1 : initMinEnergy;
}

// Driver code
public static void Main()
{
    int []arr = {4, -10, 4, 4, 4};
    int n = arr.Length;
    Console.Write(minInitialEnergy(arr, n));
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// initial energy to reach end

// Function to calculate minimum
// initial energy arr[] stores
// energy at each checkpoints on street
function minInitialEnergy($arr, $n)
{
    // initMinEnergy is variable
    // to store minimum initial
    // energy required.
    $initMinEnergy = 0;

    // currEnergy is variable to
    // store current value of energy
    // at i'th checkpoint on street
    $currEnergy = 0;

    // flag to check if we have
    // successfully crossed the
    // street without any energy
    // loss <= o at any checkpoint
    $flag = 0;

    // Traverse each check
    // point linearly
    for ($i = 0; $i < $n; $i++)
    {
        $currEnergy += $arr[$i];

        // If current energy, becomes
        // negative or 0, increment
        // initial minimum energy by
        // the negative value plus 1.
        // to keep current energy
        // positive (at least 1). Also
        // update current energy and flag.
        if ($currEnergy <= 0)
        {
            $initMinEnergy += abs($currEnergy) + 1;
            $currEnergy = 1;
            $flag = 1;
        }
    }

    // If energy never became
    // negative or 0, then
    // return 1\. Else return
    // computed initMinEnergy
    return ($flag == 0) ? 1 : $initMinEnergy;
}

// Driver Code
$arr = array(4, -10, 4, 4, 4);
$n = sizeof($arr);
echo minInitialEnergy($arr, $n);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>
// Javascript program to find minimum
// initial energy to reach end

// Function to calculate minimum
// initial energy arr[] stores
// energy at each checkpoints on street
function minInitialEnergy(arr, n) {
    // initMinEnergy is variable
    // to store minimum initial
    // energy required.
    let initMinEnergy = 0;

    // currEnergy is variable to
    // store current value of energy
    // at i'th checkpoint on street
    let currEnergy = 0;

    // flag to check if we have
    // successfully crossed the
    // street without any energy
    // loss <= o at any checkpoint
    let flag = 0;

    // Traverse each check
    // point linearly
    for (let i = 0; i < n; i++) {
        currEnergy += arr[i];

        // If current energy, becomes
        // negative or 0, increment
        // initial minimum energy by
        // the negative value plus 1.
        // to keep current energy
        // positive (at least 1). Also
        // update current energy and flag.
        if (currEnergy <= 0) {
            initMinEnergy += Math.abs(currEnergy) + 1;
            currEnergy = 1;
            flag = 1;
        }
    }

    // If energy never became
    // negative or 0, then
    // return 1\. Else return
    // computed initMinEnergy
    return (flag == 0) ? 1 : initMinEnergy;
}

// Driver Code
let arr = new Array(4, -10, 4, 4, 4);
let n = arr.length;
document.write(minInitialEnergy(arr, n));

// This code is contributed
// by Saurabh Jaiswal
</script>
```

**输出:**

```
7
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。